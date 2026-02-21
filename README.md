# 🧪 Desafío Técnico: API de Categorías

Este proyecto se trata de una API RESTful construida con **NestJS**, conectada a una base de datos **PostgreSQL**, y contenerizada con **Docker** para facilitar su ejecución.

<details open>
<summary>Tabla de contenidos</summary>

- [📦 Tecnologías utilizadas](#📦-tecnologías-utilizadas)
- [🚀 Requisitos previos](#🚀-requisitos-previos)
- [📂 Clonar el repositorio](#📂-clonar-el-repositorio)
- [⚙️ Configurar variables de entorno](#⚙️-configurar-variables-de-entorno)
- [🐳 Levantar el entorno con Docker](#🐳-levantar-el-entorno-con-docker)
- [🧪 Probar el endpoint /categoria/:id](#🧪-probar-el-endpoint-categoriaid)
- [🛠️ Estructura del proyecto](#🛠️-estructura-del-proyecto)

</details>

---

## 📦 Tecnologías utilizadas

| Herramienta       | Versión Exacta |
|-------------------|----------------|
| Node.js           | 18             |
| NestJS            | 11.x           |
| PostgreSQL        | 13             |
| TypeORM           | 0.3.x          |
| Docker            | 24.x           |
| Docker Compose    | 2.x            |
| Joi               | 17.x           |

---

## 🚀 Requisitos previos

Asegúrate de tener instaladas las siguientes herramientas en tu sistema:

- [Docker](https://www.docker.com/products/docker-desktop/) (versión 24.x)
- [Docker Compose](https://docs.docker.com/compose/) (versión 2.x o superior)
- [Git](https://git-scm.com/)
- *(Opcional)* [Postman](https://www.postman.com/) o `curl` para probar los endpoints.

> 🛑 **No es necesario tener Node.js ni instalar una base de datos local. Todo se ejecuta dentro de contenedores.**

---

## 📂 Clonar el repositorio

```bash
git clone https://github.com/JesusCruz22/nestjs-api-categories.git
cd nestjs-api-categories
```

---

## ⚙️ Configurar variables de entorno
Copia el archivo de ejemplo:

```bash
cp .env.example .env
```

El archivo .env debe quedar así:
```env
DATABASE_HOST=db
DATABASE_PORT=5432
DATABASE_USER=postgres
DATABASE_PASSWORD=postgres
DATABASE_NAME=api_categorias
DATABASE_SYNCHRONIZE=true
```

⚠️ No es necesario modificar estos valores si usarás Docker, ya que están alineados con el docker-compose.yml.

---

## 🐳 Levantar el entorno con Docker
Desde la raíz del proyecto, ejecuta:

```bash
docker-compose up --build
```
Esto:
- Construirá las imágenes necesarias
- Iniciará un contenedor para la base de datos PostgreSQL (db)
- Iniciará un contenedor para la API NestJS (api_categories)
- Precargará datos de ejemplo en la base de datos

🕓 La primera vez puede tardar unos minutos.

---

## 📖 Documentación interactiva (Swagger)

Esta API cuenta con documentación interactiva generada automáticamente con Swagger.

- Una vez que la API esté corriendo (usando Docker), accede a:

  [http://localhost:3000/api](http://localhost:3000/api)

- Desde ahí podrás:
  - Ver y probar todos los endpoints disponibles
  - Consultar los esquemas de respuesta y parámetros

---

## 🧪 Probar el endpoint /categoria/:id
Puedes probar la API de dos formas:

✅ Opción 1: Usando curl (línea de comandos)
```bash
curl http://localhost:3000/categoria/1
```

Respuesta esperada:

```json
{
  "id": 1,
  "nombre": "Neumáticos"
}
```

Si pruebas con un ID que no existe:

```bash
curl http://localhost:3000/categoria/99
```

Respuesta:

```json
{
  "error": "Categoría no encontrada"
}
```

✅ Opción 2: Usando Postman
Abre Postman (de preferencia la versión de escritorio).

Crea una nueva solicitud con el método GET.

Usa la siguiente URL:

```bash
http://localhost:3000/categoria/1
```

Haz clic en Send.

Si todo está funcionando, deberías ver la misma respuesta que con curl.

❗ Si recibes un error ECONNREFUSED, asegúrate de que los contenedores estén en ejecución (docker-compose ps) y que no haya otro servicio ocupando el puerto 3000.

---

## 🛠️ Estructura del proyecto

```bash
src/
├── app.module.ts               → Módulo principal
├── main.ts                     → Punto de entrada de la aplicación
├── categoria/
│   ├── entities/
│   │   └── categoria.entity.ts → Definición de la entidad Categoria
│   ├── categoria.module.ts     → Módulo de categoría
│   ├── categoria.service.ts    → Lógica de negocio
│   └── categoria.controller.ts → Controlador y rutas
├── env.schema.ts               → Validación del archivo .env
.env.example                    → Variables de entorno de ejemplo
Dockerfile                      → Imagen de la API
docker-compose.yml              → Orquestador de servicios
package.json                    → Dependencias de Node.js
tsconfig.json                   → Configuración de TypeScript

```
---
