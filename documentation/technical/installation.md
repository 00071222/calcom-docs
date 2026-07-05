# Instalación y entorno

Esta guía permite levantar el proyecto desde cero, de forma reproducible,
para desarrollo o revisión.

!!! warning "Uso recomendado"
    Este fork hereda la recomendación oficial de Cal.diy: está pensado para
    uso personal/académico y no para producción sin una revisión de
    seguridad adicional.

## Versiones exactas usadas en este proyecto

| Herramienta | Versión requerida |
|---|---|
| Node.js | >= 18.x |
| Yarn | >= 4.12.0 (definido en `packageManager` de `package.json`) |
| npm | >= 7.0.0 |
| PostgreSQL | >= 13.x |

Estas versiones están declaradas en el campo `"engines"` y
`"packageManager"` de `package.json` en la raíz del repositorio.

## 1. Clonar el repositorio (este fork)

```bash
git clone --branch feat/conditional-questions-11900 \
https://codeberg.org/Josstsx/cal-aca.diy.git
```

## 2. Instalar dependencias

```bash
yarn install
```

## 3. Configurar variables de entorno

```bash
cp .env.example .env
```

Genera y agrega las claves obligatorias:

```bash
# Cookie encryption key
openssl rand -base64 32   # → NEXTAUTH_SECRET

# Clave de cifrado (32 bytes para AES256)
openssl rand -base64 24   # → CALENDSO_ENCRYPTION_KEY
```

Copia también `DATABASE_URL` a `.env.appStore` si vas a habilitar apps del
App Store.

## 4. Base de datos

!!! info "Sin migraciones nuevas"
    La funcionalidad de preguntas condicionales **no requiere ninguna
    migración de Prisma**: se almacena dentro de la columna JSON existente
    `EventType.bookingFields`. Los pasos de esta sección son los mismos que
    para cualquier instalación estándar de Cal.diy.

En desarrollo:

```bash
yarn workspace @calcom/prisma db-migrate
```

Opción rápida con Docker (levanta Postgres + usuarios de prueba):

```bash
yarn dx
```

Credenciales de prueba creadas por `yarn dx`:

| Email | Contraseña | Rol |
|---|---|---|
| `free@example.com` | `free` | Usuario gratuito |
| `pro@example.com` | `pro` | Usuario Pro |
| `admin@example.com` | `ADMINadmin2022!` | Administrador |

## 5. Levantar el proyecto

```bash
yarn dev
```

Abre `http://localhost:3000`.

## 6. Verificar la funcionalidad de preguntas condicionales

1. Inicia sesión con cualquier usuario de prueba.
2. Ve a **Event Types**, un evento, pestaña **Advanced**.
3. Agrega o edita una pregunta personalizada y activa
   **Show this field conditionally** (ver la
   [guía de usuario](../user-guide/conditional-questions.md)).
4. Reserva ese tipo de evento como asistente para comprobar que el campo
   aparece/desaparece según la respuesta previa.

## Ejecutar la documentación localmente

Este sitio se genera con **MkDocs** + el tema **Material** (ambos FOSS).

```bash
pip install mkdocs mkdocs-material

# Desde donde está mkdocs.yml
mkdocs serve
```

Esto ejecuta el sitio en `http://127.0.0.1:8000` con recarga automática.

Para generar el sitio estático usar:

```bash
mkdocs build
```

Esto genera una carpeta `site/` con HTML listo para desplegar.
