# Cal.diy — Preguntas Condicionales

Este sitio documenta el fork académico de **Cal.diy** (la edición
community/open-source de Cal.com) que añade soporte de **visibilidad
condicional de preguntas** en los formularios de reserva (booking forms).

## ¿Qué es esta funcionalidad?

Permite que un campo personalizado del formulario de reserva solo se muestre
al asistente cuando una respuesta previa cumple cierta condición. Por
ejemplo, en un formulario de citas médicas:

> "¿Tiene alguna alergia?" → si la respuesta es **Sí**, aparece una segunda
> pregunta: "¿A qué es alérgico/a?"

Si la respuesta es **No**, la segunda pregunta nunca se muestra ni se exige.

## Cómo está organizada esta documentación

- **[Guía de usuario](user-guide/conditional-questions.md)** — para quien
  configura formularios de reserva (por ejemplo, el administrador de una
  clínica). No requiere conocimientos técnicos.
- **Documentación técnica** — para quien necesita instalar, correr o extender
  el proyecto:
    - [Instalación y entorno](technical/installation.md)
    - [Arquitectura de la funcionalidad](technical/architecture.md)
    - [Referencia de API](technical/api-reference.md)
- **[Licencia de la documentación](license.md)**

## Origen del proyecto

Este fork forma parte de [Cal.diy](https://github.com/calcom/cal.diy), la edición
100% open-source (licencia MIT) de Cal.com. Todo lo que no se documenta aquí
(integraciones de calendario, videollamadas, etc.) se mantiene sin cambios;
consulta la documentación oficial de Cal.diy para esas partes.
