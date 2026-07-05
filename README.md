# Documentación de Cal.diy

Este repositorio contiene la documentación oficial e independiente de **Cal.diy**, un sistema de programación de citas y calendario de código abierto adaptado para la comunidad.

La versión en producción de este sitio está desplegada automáticamente en **GitHub Pages**.

---

## 🔗 Proyecto Original

Este sitio de documentación complementa al repositorio principal del proyecto, el cual se aloja y mantiene en **Codeberg**:
👉 **[Repositorio Principal Cal.diy en Codeberg](https://codeberg.org/Josstsx/cal-aca.diy)**

---

## 🚀 Cómo levantar el proyecto en local

Esta documentación está construida utilizando **Next.js** y **Nextra** (un framework estático de alto rendimiento para documentación).

### Requisitos previos

Asegúrate de tener instalado **Node.js** (versión 18 o superior) en tu sistema.

### 1. Instalar dependencias

Se recomienda utilizar **pnpm** para gestionar las dependencias de este repositorio. Instálalas ejecutando en la raíz:

```bash
pnpm install
```

### 2. Ejecutar el servidor de desarrollo

Para iniciar el servidor local con recarga en vivo (hot-reload) y soporte experimental de Turbopack:

```bash
pnpm run dev
```

El sitio estará disponible para visualizar en tu navegador en:  
👉 **[http://localhost:3000](http://localhost:3000)**

### 3. Compilar para producción (Build estático)

Para compilar la aplicación, generar la exportación HTML estática (`out/`) e indexar el buscador con `pagefind`:

```bash
pnpm run build
```

Este comando generará la carpeta `/out` con todos los recursos listos para ser servidos estáticamente.

---

## 🛠️ Despliegue (GitHub Pages)

Este repositorio está configurado con **GitHub Actions** para compilar y desplegar automáticamente la documentación en cada actualización.

*   El archivo de configuración del flujo de trabajo se encuentra en [deploy.yml](file:///.github/workflows/deploy.yml).
*   **Nota de Configuración:** Si utilizas la URL por defecto de GitHub Pages (`https://tu-usuario.github.io/tu-repositorio/`), asegúrate de descomentar y editar la línea `basePath` en [next.config.mjs](file:///next.config.mjs):
    ```javascript
    basePath: '/tu-repositorio',
    ```