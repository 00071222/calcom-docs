# Arquitectura de la funcionalidad

## Resumen

La visibilidad condicional de preguntas se implementó extendiendo el sistema
existente de "booking fields" (preguntas del formulario de reserva) de
Cal.diy, sin introducir nuevas tablas ni migraciones de base de datos.

## Componentes tocados

### 1. Esquema de datos — `packages/prisma/zod-utils.ts`

```ts
conditionalOn: z
  .object({
    parentFieldName: z.string(),
    showWhenParentHasValues: z.array(z.string()),
  })
  .optional(),
```

Este objeto vive dentro del schema Zod compartido por todos los campos de
`bookingFields`, que a su vez se guarda en la columna `Json?` existente
`EventType.bookingFields` (`packages/prisma/schema.prisma`, línea 194). No
se agregó ninguna columna ni tabla nueva.

### 2. Editor del campo — `apps/web/modules/event-types/components/tabs/advanced/FormBuilder.tsx`

- Solo se muestra para campos personalizados editables por el usuario
  (excluye campos `system` / `system-but-optional`).
- Filtra los campos candidatos a "padre" a los tipos `select`, `radio`,
  `checkbox` y `multiselect`.
- Al activarse, permite elegir el campo padre y qué valores de sus opciones
  activan la visibilidad.

### 3. Render en el formulario de reserva — `apps/web/modules/bookings/components/BookEventForm/BookingFields.tsx`

Evalúa, para cada campo con `conditionalOn`, si las respuestas actuales del
formulario satisfacen la condición:

```ts
if (field.conditionalOn) {
  const { parentFieldName, showWhenParentHasValues } = field.conditionalOn;
  const parentValue = allResponses?.[parentFieldName];
  const parentValues = Array.isArray(parentValue)
    ? parentValue
    : [String(parentValue ?? "")];
  if (!showWhenParentHasValues.some((v) => parentValues.includes(v))) {
    hidden = true;
  }
}
```

### 4. Validación server-side — `packages/features/bookings/lib/getBookingResponsesSchema.ts`

Si la condición no se cumple, el campo se **omite por completo** del ciclo
de validación de "required", antes de evaluar si el valor es obligatorio.
Esto garantiza que un campo oculto nunca bloquee un envío.

### 5. API pública v2

- `apps/api/v2/.../transformers/internal-to-api/booking-fields.ts`
- `apps/api/v2/.../transformers/api-to-internal/booking-fields.ts`

`conditionalOn` se transforma en ambas direcciones junto con el resto de
propiedades del campo, por lo que cualquier integración externa que use la
API v2 de event-types puede leer y escribir esta configuración igual que
desde el dashboard.