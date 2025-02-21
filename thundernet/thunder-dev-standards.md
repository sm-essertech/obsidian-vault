# Estandares de desarrollo
En este documento se enlistan las pautas a seguir para mantener un estandar para el desarrollo y mantenimiento de los sistemas de Thundernet.

## Índice
- [Idiomas](#idiomas)
- [Git / Github](#git/github)
	- [Nomenclatura de repositorios](#nomenclatura%20de%20repositorios)
	- [Ramas](#ramas)
		- [Protección de ramas](#protección%20de%20ramas)
	- [Commits](#commits)
		- [Tipos](#tipos)
		- [Cambios importantes](#cambios%20importantes)
	- [Pull Requests](#pull%20requests)
		- [Resolución de conflictos](#resolución%20de%20conflictos)
	- [Archivo README](#archivo%20readme)
- Nomenclatura:
	- Variables
- [Frontend](#frontend)
- [Backend](#backend)
## Idiomas
Todo el código fuente debe ser manejado en inglés, eso incluye:
- Comentarios
	- Funciones / métodos
	- Clases
	- Archivos
	- Repositorios
	- Commits
	- Ramas
- Comandos(Ej: "npm run migrations", "make build")

Por otro lado hemos optado por mantener toda la documentación en español, ya sea hacia el usuario final o incluso en la documentación técnica. 
- Archivos README.
- Documentación API.
- Manuales de usuario.
- Videos instructivos.
## Git / Github
Los repositorios deben poder mantener un historial limpio que simplifique la lectura y el entendimiento de los cambios realizados y el avance del proyecto.

### Nomenclatura de repositorios
Los repositorios creados entro de la organización [github.com/thundernet-ca](https://github.com/thundernet-ca) deben asegurar el uso del prefijo `thunder-` a modo de determinar cada elemento de software involucrado en las actividades de servicios prestados por la empresa. Por ejemplo:
- thunder-erp
- thunder-core
- thunder-platform

### Ramas
El uso de distintas facilita el seguimiento y mantenimiento del código, un buen historial permite entender el progreso del proyecto, mantener distintos entornos separados, asegurar que llegue una cantidad mínima de errores a producción y que estos, una vez detectados, sean fáciles de parchear.

Por lo que se decide mantener un estandard basado en [Gitflow](https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow):
- __master__: Rama de producción, en esta se registran los lanzamientos de nuevas versiones.
- __develop__: Rama creada en base a `master` donde se integran todas las nuevas features.
- __feature/[name]__: Rama para creada en base a `develop` para desarrollar una nueva funcionalidad.
- __release/[version]__: Una vez hay suficientes nuevas features en `develop` para una nueva versión, se crea una rama release, la cual es usada para realizar el merge con `master`.
- __hotfix/[error]__: Rama creada en base `master` para parchear errores en producción.

__Flujo de ramas:__
- `master` Es la rama que contiene el código fuente de producción.
- `develop` Se crea en base a master. En esta rama se hace merge de las nuevas features.
- `feature/[name]` Se crea en base a develop. Se crea una rama por funcionalidad (Definidas en trello, Jira, o la herramienta de seguimiento que se esté usando).
- `release/[version]` Se crea en base develop. Cuando hay suficientes nuevas funcionalidades en develop se crea una nueva versión y se lleva a master. Una vez llevado a master se fusiona de regreso a develop y se elimina la rama.
- `hotfix/[error]` Se crea en base a master. Sirve para parchear errores urgentes encontrados en producción. 

#### Protección de ramas
- Las ramas `master` y `develop` deben estar protegidas en GitHub.
- Requerir al menos **1 aprobación** antes de mergear.
 
> Pendiente por definir

### Commits
Es importante que al leer el historial de commits sean fácil de interpretar los nuevos cambios aplicados al código fuente, por lo que se maneja el standard [conventional commits](https://www.conventionalcommits.org/en/v1.0.0/).

Cada mensaje de commit debe mantener la siguiente estrucutura:

```shell
<type>(optional scope): <description>

[optional body]

[optional footer(s)]

```

> Los mensajes de commit deben estar **en inglés**, siguiendo el estándar Conventional Commits.

#### Tipos 
Aquí hay un listado base de los tipos de commit mas usados:

- __feat__: Es usado al momento de agregar una nueva funcionalidad. Ej: `feat: add endpoint to list products`.
- __fix__: Es usado al momento de solucionar un bug. Ej: `fix(profits): solve decimals error in response`.
- __docs__: Es usado en commits que únicamente modifican la documentación. Ej: `docs: Update README`.
- __style__: Es usando en cambios que unicamente afectan la visualización del código como identación, espacios en blanco, saltos de línea. Ej: `style: run eslint command`.
- __refactor__: Un cambio en el código que no soluciona un bug ni añade una nueva funcionalidad. Ej: `refactor(router): modify users endpoints`.
- __perf__: Es usado al momento de hacer un cambio en el código para mejorar el rendimiento. Ej: `perf: get users contacts in a JOIN sql query`. 
- __test__: Es usado al momento de crear un nuevo test o editar un test ya existente. Ej: `test: add test for vendors profit calc`.
- __build__: Es usado en cambios a elementos que afectan a la compilación del programa o a dependencias externas. Ej: `build: modify make command`.
- __ci__: Es usado en cambios relacionados a la integración continua. Ej: `ci: update gh pipeline`. 
- __chore__: Usado en cambios que no modifican archivos dentro de src o tests. `chore: add bin directory to .gitignore`.
- __revert__: Es usado al momento de revertir un commit. Ej: `revert: commit c0b706ad...`.

#### Cambios Importantes
Al momento de crear cambios en el código que podrían romper versiones anteriores o que requieren de pasos extra para su despliegue es importante señalarlos con dos elementos principales:

- Usar "!" al lado de la etiqueta del tipo de commit.
- User el footer __BREAKING CHANGE__ con la descripción correspondiente del cambio y el por qué es importante.

Por ejemplo:
```shell
feat(users)!: Create user balance CRUD.

New Crud is created at endpoints /api/users/{user_id}/balance/...
- GET /: Get balance
- POST /add: Add balance amount to current balance.
- PATCH /: Update balance

BREAKING CHANGE: Run last migration is required
```

### Pull Requests
Un buen template asegura que los PRs incluyan información relevante. Aquí un ejemplo que puedes guardar en `.github/PULL_REQUEST_TEMPLATE.md`:

```markdown
## Descripción
<!--- Explica el propósito de este PR. Incluye enlaces a issues relacionados (ej: "Resuelve #123"). -->

## Cambios Propuertos
<!--- Lista los cambios técnicos principales. -->
- [ ] Nueva funcionalidad: [Describir brevemente].
- [ ] Corrección de bug: [Mencionar el issue].
- [ ] Mejora de rendimiento: [Detallar métricas afectadas].

## Checklist
- [ ] He hecho rebase de esta rama sobre `develop`.
- [ ] Los tests unitarios pasan localmente.
- [ ] Actualicé la documentación (README, Swagger, etc).
- [ ] Incluí capturas de pantalla (si aplica).

## Notas Adicionales
<!--- Comentarios para los revisores, dependencias, etc. -->
```

#### Resolución de conflictos
Si al crear un PR se detectan conflicos de tu rama actual considera resolver el conflicto con una estrategia de `git rebase`. Puedes seguir los siguientes pasos.

1. Posicionate en la rama con los cambios, en este caso usaremos feat/lorem-ipsum: `git checkout feat/lorem-ipsum`.
2. Obten los últimos cambios de la rama objetivo, en este caso usaremos develop: `git fetch origin develop`.
3. Realiza un backup de tu rama actual para preservar tus cambios: `git branch feat/lorem-impsum-backup`
4. Realiza el rebase de la rama objetivo a tu rama `git rebase origin/develop`
5. Si existe un conflicto:
	- Resuelve el conflicto.
	- Agrega los cambios: `git add`.
	- Ejecuta el rebase: `git rebase --continue`.
6. Fuerza un push de los cambios a tu rama: `git push origin feath/lorem-ipsum --force-with-lease`.
7. El conflicto debe haber desaparecido, el PR puede hacer aceptado.

### Archivo README
El archivo README es la entrada para cualquier desarrollador que se una a un proyecto, por lo que es importante que todas cuenten con la información necesaria para agilizar esa integración. Para ello el archivo debe contener:
- __Título__: Nombre del repositorio (ref: [Nomenclatura de repositorios](#nomenclatura%20de%20repositorios))
- __Shields(Opcional)__:  En proyectos grandes puede ser útil mantener a la vista datos como la versión actual del proyecto, el estado del build, la covertura de los test.
- __Descripción__: Un resumen del proyecto que explique:
	- Qué es?
	- Para qué es?
	- Cómo se relaciona con otros proyectos?
- __Tecnologías__: Un resumen visual de las tecnologías usadas.
- __Estructura del proyecto__: Definir la estructura de carpetas usada en el proyecto, explicando para que sirve cada sección. Por ejemplo:
	- _/src_: Código fuente del proyecto
		- _/models_: Definición de los modelos de la base de datos
		- _/services_: Definición de los servicios del proyecto, tales como S3, Redis.
		- ...
	- _/test_: Directorio padre de los test unitarios.

	 Opcionalmente se puede incluir un diagrama a modo de ejemplo visual mas claro de la estructura.
	 
```shell
# Ejemplo netamente referencial

thunder-backend/
├── src/
│   ├── controllers/          # Controladores de la API
│   │   └── userController.js
│   ├── services/             # Lógica de negocio
│   │   └── userService.js
│   ├── repositories/         # Acceso a la base de datos
│   │   └── userRepository.js
│   ├── models/               # Modelos de datos (ej: MongoDB, SQL)
│   │   └── User.js
│   ├── routes/               # Definición de rutas
│   │   └── userRoutes.js
│   ├── middleware/           # Middlewares (ej: autenticación, validación)
│   │   └── authMiddleware.js
│   ├── utils/                # Utilidades (ej: helpers, validadores)
│   │   └── logger.js
│   ├── config/               # Configuraciones (ej: base de datos, entorno)
│   │   └── db.js
│   └── app.js                # Punto de entrada de la aplicación
├── tests/                    # Pruebas unitarias y de integración
│   ├── unit/
│   │   └── userService.test.js
│   └── integration/
│       └── userRoutes.test.js
├── migrations/               # Migraciones de base de datos )
│   └── 20231015_create_users_table.js
├── scripts/                  # Scripts útiles (ej: despliegue, limpieza)
│   └── seedDatabase.js
├── .env                      # Variables de entorno
├── .env.example              # Plantilla de variables de entorno
├── .gitignore                # Archivos ignorados por Git
├── package.json              # Dependencias y scripts
├── README.md                 # Documentación del proyecto
└── Dockerfile                # Configuración de Docker
```
	 
- __Instalación local__: Incluir las instrucciones para poder correr el proyecto localmente. Las instrucciones deben considerar:
	- __Requerimientos__: Listado de tecnologías necesarias y sus versiones.
	- __Variables de entorno__: Adjuntar el listado de variables de entorno necesarias o en su defecto el archivo `.env.example`.
	- __Pasos__: Detallar el conjunto de pasos necesarios para ejecutar el proyecto e incluir ejemplos en el caso de ejecución de comandos. Ej:
		1. Clonar el repositorio `$ git clone https://github.com/thundernet-ca/thunder-project & cd thunder-project`
		2. Instalar las dependencias `$ pnpm install`
		3. Copiar las variables de entorno `$ cp .env.example .env`
		...
		7. Correr el proyecto `$ pnpm start:dev` 

- __Docker__: El proyecto debe contener los recursos necesarios para levantar el proyecto en docker, tales como:
	- __Archivos__: Dockerfile, docker-compose.yaml, .dockerignore
	- __Instruciones__: Ejemplos de los comandos y detalles necesarios para levantar el proyecto. Ej: "1. Levantar el proyecto ejecutando `$ docker compose -d up`"

## Frontend 

## Backend