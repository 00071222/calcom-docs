# Referencia de API — `conditionalOn`

La API v2 de event types de Cal.diy expone la configuración de preguntas
condicionales igual que el resto de propiedades de un campo de
`bookingFields`. No se agregó ningún endpoint nuevo: `conditionalOn` es una
propiedad adicional dentro de los objetos de campo ya existentes en
`GET/PATCH /v2/event-types/{id}`.

## Forma del objeto

```json
{
  "name": "allergy_detail",
  "type": "text",
  "label": "¿A qué es alérgico/a?",
  "required": true,
  "conditionalOn": {
    "parentFieldName": "has_allergies",
    "showWhenParentHasValues": ["yes"]
  }
}
```

| Propiedad | Tipo | Descripción |
|---|---|---|
| `parentFieldName` | `string` | El `name` del campo que actúa como condición. Debe ser un campo de tipo `select`, `radio`, `checkbox` o `multiselect`. |
| `showWhenParentHasValues` | `string[]` | Lista de valores del campo padre que activan la visibilidad de este campo. Si el valor actual del padre coincide con alguno de estos, el campo se muestra. |

Si `conditionalOn` no está presente, el campo se comporta como siempre
(siempre visible, sujeto solo a las demás reglas existentes como `hidden` o
`hideWhenJustOneOption`).

## Archivos relevantes en el código

| Dirección | Archivo |
|---|---|
| Interno → API (respuesta de `GET`) | `apps/api/v2/src/platform/event-types/event-types_2024_06_14/transformers/internal-to-api/booking-fields.ts` |
| API → Interno (payload de `PATCH`/`POST`) | `apps/api/v2/src/platform/event-types/event-types_2024_06_14/transformers/api-to-internal/booking-fields.ts` |
| Tipos de entrada | `packages/platform/types/event-types/event-types_2024_06_14/inputs/booking-fields.input.ts` |