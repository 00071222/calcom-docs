# Preguntas condicionales en formularios de reserva

Esta guía explica cómo configurar una pregunta que solo aparece cuando una
respuesta anterior lo justifica, por ejemplo, en un formulario de citas
médicas.

## Requisitos previos

- Debes tener acceso de administrador/host al tipo de evento (event type)
  que quieres editar.
- Debe existir ya un campo de tipo **selección**, **radio**, **casillas
  (checkbox)** o **selección múltiple** que sirva como "pregunta padre".
  Solo estos tipos pueden usarse como condición.

## Paso a paso

### 1. Entra a la configuración del tipo de evento

- Ve a **Event Types**
- Selecciona el evento (por ejemplo, "Consulta médica
general") 
- Ve a la pestaña **Advanced**

### 2. Crea o edita la pregunta que dependerá de otra

En la sección **Booking questions**, agrega una nueva pregunta o edita una
existente (por ejemplo: "¿A qué es alérgico/a?").

### 3. Activa la visibilidad condicional

Dentro del editor de la pregunta, marca la casilla:

> ☑ **Show this field conditionally**

Esto solo aparece para preguntas personalizadas (no para campos del sistema
como nombre o correo).

### 4. Elige la pregunta "padre" y los valores que la activan

1. En **Show when field...**, selecciona la pregunta previa que actuará
   como condición (por ejemplo: "¿Tiene alguna alergia?").
2. En **Has value**, marca cuáles de las opciones de esa pregunta deben
   estar seleccionadas para que la nueva pregunta aparezca (por ejemplo:
   "Sí").

### 5. Guarda los cambios

Haz clic en **Add**. La pregunta condicional ya no será obligatoria por
defecto para el asistente si nunca llega a mostrarse.

## Ejemplo aplicado: formulario de citas médicas

| Pregunta | Tipo | Condición |
|---|---|---|
| ¿Tiene alguna alergia? | Select (Sí / No) | Siempre visible |
| ¿A qué es alérgico/a? | Texto | Visible solo si la anterior = "Sí" |
| ¿Toma algún medicamento actualmente? | Select (Sí / No) | Siempre visible |
| ¿Cuál(es)? | Texto | Visible solo si la anterior = "Sí" |

Con esta configuración, un asistente que responde "No" a ambas preguntas
iniciales nunca ve las preguntas de seguimiento, y su reserva no se bloquea
por "campos requeridos" que nunca llegó a ver.