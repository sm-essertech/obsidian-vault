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
- [Frontend](#frontend)
	- [Accesibilidad](#accesibilidad)
	- [SEO](#seo)
		- [Metatags](#metatags)
	- [Rendimiento](#rendimiento)
		- [Optimización de imágenes](#optimización%20de%20imágenes)
	- [Responsividad](#responsividad)
		- [Mobile First](#mobile%20first)
	- [Gestión de estado](#gestión%20de%20estado)
		- [Estado Local](#estado%20local)
		- [Estado Global](#estado%20global)
	- [Interacción con API](#interacción%20con%20api)
		- [Axios](#axios)
		- [Hooks](#hooks)
		- [Mensajes de error](#mensajes%20de%20error)
		- [Caching](#caching)
		- [Paginación](#paginación)
		- [Optimización de peticiones](#optimización%20de%20peticiones)
	- [Pruebas E2E](#pruebas%20e2e)
        - [Cypress](#cypress)
        - [Playwright](#playwright)
        - [Buenas prácticas](#buenas%20prácticas)
	- [Herramientas para Frontend](#herramientas%20para%frontend)
		- [Lighthouse](#lighthouse)
- [Backend](#backend)
	- [API](#api)
		- [Rest](#rest)
		- [Seguridad](#seguridad)
			- [Autenticación y autorización](#autenticación%20y%autorización) 
			- [Cors](#cors)
			- [Rate Limiting](#rate%20limiting)
		- [Documentación](#documentacion)
			- [Swagger](#swagger)
			- [Postman](#postman)
		- [Manejo de errores](#manejo%20de%20errores)
			- [Códigos de HTTP](#códigos%20de%20http)
			- [Respuestas](#respuestas)
	- [Migraciones](#migraciones)
	- [Pruebas](#pruebas)
		- [TDD](#tdd)
		- [Rendimiento](#rendimiento)
			- [Herramientas](#herramientas)
			- [Estrategias](#estrategias)
			- [Tipos de prueba](#tipos%20de%20prueba)

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
Al momento de desarrollar frontend debemos tomar en cuenta que es la capa directa de interacción entre el usuario y la lógica de negocio, por lo que es necesario garantizar el rendimiento y la experiencia de uso del sistema o sitio web que se esté desarrolando, por lo que en esta sección listamos un conjuto mínimo de buenas prácticas.

### Accesibilidad
Para garantizar que la aplicación sea óptima y utilizable por personas con discapacidades es importante considerar los siguientes aspectos: 

- __Cumplimiento de las WCAG__: Adherirse a las Pautas de Accesibilidad al Contenido Web ([WCAG](https://accessibility.fiu.edu/resources/wcag/)) para garantizar que el contenido sea accesible para personas con discapacidades. Esto incluye proporcionar texto alternativo para imágenes, garantizar suficiente contraste de color y utilizar HTML semántico.
- __Atributos ARIA__: Utilizar atributos [ARIA](https://developer.mozilla.org/es/docs/Web/Accessibility/ARIA) (Aplicaciones de Internet Enriquecidas Accesibles) para mejorar la accesibilidad del contenido dinámico y los componentes de la interfaz de usuario personalizados.
- __Navegación con teclado__: Asegurarse de que todos los elementos interactivos puedan ser accedidos y operados usando un teclado.
- __Pruebas con lectores de pantalla__: Probar regularmente la aplicación con lectores de pantalla para identificar y abordar problemas de accesibilidad.
- __Pruebas de contraste de color__: Verificar que el texto y las imágenes tengan suficiente contraste de color para ser legibles.

### SEO
Aquellas plataformas de frontend que deben poder ser accedidas por los clientes deben posicionarse en los primeros resultados de búsqueda en los navegadores, por lo que es necesario que sigan las pautas principales de optimización para motores de búsqueda. Esto incluye:

- __HTML Semántico__: Utilizar etiquetas HTML semánticas para estructurar el contenido de manera que sea significativo para los motores de búsqueda. Por ejemplo: `<article>`,  `<nav>`, `<aside>`.
- __Estrucutra de la url__:  Crear URLs limpias, legibles y ricas en palabras clave.
- __Sitemap__: Enviar un mapa del sitio ([sitemap](https://developers.google.com/search/docs/crawling-indexing/sitemaps/overview?hl=es)) a los motores de búsqueda para ayudarles a rastrear e indexar el sitio de manera efectiva.
- __Squema markup__: Implementar el [marcado de esquema](https://umbraco.com/knowledge-base/schema-markup/) para proporcionar datos estructurados sobre el contenido, mejorando la comprensión de los motores de búsqueda y la visualización de fragmentos enriquecidos.

#### Metatags
Los metadatos de un sitio web son una pieza esencial para proporcionar información de nuestro sitio a los motores de busqueda, por lo que su implementación y optimización son importantes para lograr un buen posicionamiento. Algunas de las [etiquetas más usadas](https://seocrawl.com/meta-tags/) son:

__Title__ 
Es la encargada de decirle a los motores de búsqueda la idea o tema principal sobre el que trata el contenido de la página que va a rastrear y se recomienda **no excederse en 70 caracteres**. Por ejemplo: `<title>Bienvenido a thundernet</title>`.
 
 __Description__ 
 Complemento a la etiqueta Title, con la meta description le daremos una información algo más extensa a los motores de búsqueda del contenido de nuestra página. Trataremos de detallar con la mayor precisión posible el contenido que vamos a ofrecer al usuario. Ejemplo: `<meta name="description" content="El mejor proveedor de servicios de telecomuniaciones de venezuela..."/>`
 
__Etiquetas Hs: Jerarquía de encabezados__ 
Como su nombre indica, los encabezados servirán para jerarquizar y ordenar el contenido de una página, por orden de importancia (h1, h2, h3…). Se utiliza un único h1, que será el que defina el título del contenido, por ejemplo: `<h1>Sobre nosotros</h1>`

__Canonical__ 
La meta etiqueta canonical es utilizada para decir a Google cual es la página original en el caso de encontrarnos con páginas similares o idénticas. Esta etiqueta tiene una gran importancia al igual que las anteriores, ya que un incorrecto uso de la misma puede llevar a Google a pensar que la página importante es la incorrecta. [Aquí](https://seocrawl.com/canonical/) hay una guía que detalla el uso de la etiqueta.

__Alt__
A la hora de posicionarnos en Google, no debemos olvidar el posicionamiento en Google imágenes. Para esto, haremos uso de la etiqueta ALT (texto alternativo), la cual ayudará a Google a saber de qué trata nuestra imagen. Ejemplo: `<img src=”about-banner.jpg” alt=”Banner de la sección Sobre Nosotros” />`.

__Robots__
Mediante esta etiqueta, indicaremos a Google que contenido deber ser indexado y cual no, así como si los enlaces deben ser seguidos o no. Tenemos los siguientes parametros:
-  _Index_: se toma por defecto.
- _Follow_: se toma por defecto.
- _Noindex_: se tiene que especificar cuando no queremos que indexe una página.
- _Nofollow_: se tiene que especificar cuando no queremos que siga los enlaces de una página.

__Open Graph__:
Las etiquetas **Open Graph**, son un protocolo que nos permite indicar a las redes sociales que información mostrar cada vez que se comparta un enlace de nuestro sitio web. Aunque no tengan una relación directa con el SEO, sí son importantes a nivel usuario y a nivel marca, con lo que es recomendable prestarles atención ya que serán nuestra imagen en las redes sociales.

Se implementan de la siguiente manera:
```html
<meta property=”og:type” content=”website” />
<meta property=”og:title” content=”título de tu página o tu post” />
<meta property=”og:description” content=”descripción del contenido de la página” />
<meta property=”og:image” content=”enlace al archive de la imagen” />
<meta property=”og:url” content=”permalink” />
```
### Rendimiento:
Existen algunas estrategias que ya son indispensables para maximizar el rendimiento de carga de los sitiós web y sus componentes. Como mínimo debe cumplir con:

- __División del código__:  Dividir la aplicación en fragmentos más pequeños que se pueden cargar bajo demanda, reduciendo el tiempo de carga inicial.
- __Lazy Load__: Cargar imágenes y otros recursos no críticos solo cuando están a punto de entrar en el campo de visión.
- __Minificación y compresión__: Minificar archivos CSS y JavaScript para reducir su tamaño, y utilizar algoritmos de compresión como Gzip o Brotli para reducir aún más los tiempos de transferencia.
- __Caché__: Aprovechar el almacenamiento en caché del navegador y los service workers para almacenar en caché los activos estáticos y las respuestas de la API, mejorando los tiempos de carga para los usuarios que regresan.

> Cabe destacar que los frameworks actuales como [NextJS](https://nextjs.org/) ya incorporan o facilitan la implementación de estas prácticas. 
#### Optimización de imagenes
La descarga del contenido multimeda es probablemente una de las tareas más pesadas al momento de cargar un sitio web, este puede afectar gravemente a la experiencia del usuario, por lo que es importante considerar una serie de recomendaciones.

__Redimensionar y recortar__
 - Utiliza herramientas como Adobe Photoshop o Canva para redimensionar y recortar imágenes a las dimensiones necesarias para tu sitio web. Esto reduce significativamente el tamaño del archivo.
 - Si solo necesitas mostrar imágenes de hasta 1000 píxeles de ancho, no tiene sentido cargar una imagen de 4000 píxeles de ancho.

__Compresión__
- __Compresión con perdida (Lossy)__: Utiliza herramientas como [TinyPNG](https://tinypng.com/) o [Image Compressor](https://imagecompressor.com/) para comprimir imágenes con pérdida. Este método reduce el tamaño del archivo sacrificando algo de calidad visual, ideal para fotografías donde la pérdida no es perceptible.
- __Compresión sin perdida (Lossless)__: Ideal para gráficos, logotipos o imágenes con áreas de color sólido. Herramientas como [OptiPNG](https://optipng.sourceforge.net/) o [ImageOptim](https://imageoptim.com/mac) pueden comprimir sin afectar la calidad visual.  

__Formatos de imagen__
- __WebP__: Ofrece una mejor compresión que JPEG y PNG, especialmente para imágenes con texto o gráficos.
- __JPEG__: Ideal para fotografías.
- __PNG__:  Mejor para gráficos y logotipos donde se requiere transparencia.

__Eliminación de metadatos__
Utiliza herramientas para eliminar información innecesaria como la fecha de captura o la cámara utilizada, lo que reduce el tamaño del archivo sin afectar la calidad visual.

__Uso de herramientas automáticas__
Puede ser favorable integrar herramientas para automatizar los procesos de compresión, conversión y redimensión al momento de subir imágenes desde la plataforma web.

### Responsividad
Al momento de crear las vistas de las aplicaciones web, ya sea una plataforma para clientes o un sistema de uso interno, es importante que la vista pueda adaptarse de la mejor manera posible a los distintos dispositivos del usuario final, por lo que es importante siempre mantener un diseño responsivo.

Algunas de las ténicas clave de la responsibidad son:

- __Media Queries__: Utilizar media queries en CSS para aplicar diferentes estilos según las características del dispositivo, como el tamaño de la pantalla, la resolución y la orientación. Esto permite ajustar la apariencia de los elementos y la disposición del contenido para adaptarse a cada dispositivo.
- __Flexible Layouts__:  Utilizar técnicas de diseño flexible, como Flexbox y CSS Grid, para crear diseños que se adapten automáticamente al tamaño de la pantalla. Flexbox es ideal para diseños unidimensionales, mientras que CSS Grid es más adecuado para diseños bidimensionales.
- __Responsive images__: Utilizar imágenes que se adapten al tamaño de la pantalla para evitar cargar imágenes grandes en dispositivos pequeños. Esto se puede lograr utilizando el elemento `<picture>` o el atributo _srcset_ en la etiqueta `<img>`.
- __Touch Friendly design__: Asegurarse de que los elementos interactivos, como botones y enlaces, sean lo suficientemente grandes y estén espaciados adecuadamente para facilitar su uso en dispositivos táctiles. Se recomienda un tamaño mínimo de 44x44 píxeles para los objetivos táctiles.

#### Mobile First:
Hoy en día los dispositivos móviles son una parte importante de nuestras vidas, nos acompañan todo el tiempo y los usamos para resolver todas nuestra tareas cotidianas, ya sean entretenimiento, trabajo, enterarnos de noticias. 

Por parte de los desarrolladores el diseño de los sistemas a menudo tiende a centrarse en el uso de escritorio, lo cual no es algo malo, pero en situaciones donde es necesario que la aplicación pueda usarse 100% desde un dispositivo móvil pensar el diseño y desarrollo comenzando por los dispositivos de escritorio puede entorpecer la simplificación de la aplicación en una pantalla de celular.

Mobile First es una filosofía de diseño web que prioriza la creación de una excelente experiencia de usuario en dispositivos móviles antes de expandir el diseño a tabletas y computadoras de escritorio. Esto implica diseñar la aplicación primero para las limitaciones de los dispositivos móviles (pantallas más pequeñas, conexiones más lentas) y luego agregar funcionalidades y mejoras para dispositivos más grandes.

__Beneficios del mobile first__

- __Mejor experiencia del usuario en móviles__: Al diseñar primero para móviles, se asegura que la aplicación sea rápida, eficiente y fácil de usar en estos dispositivos, que suelen tener menos recursos.

- __Rendimiento Óptimo__: Priorizar el rendimiento en móviles conduce a un código más limpio y eficiente, lo que beneficia a todos los usuarios, independientemente del dispositivo que utilicen.

-  __SEO Mejorado__: Google y otros motores de búsqueda priorizan los sitios web optimizados para móviles, lo que puede mejorar el ranking en los resultados de búsqueda.

- __Mayor flexibilidad y escalabilidad__: Un diseño Mobile First es más fácil de adaptar y escalar a diferentes tamaños de pantalla y dispositivos en el futuro. 

En lineamientos generales, podemos implementar mobile first siguiendo con los pasos:

1. __Comenzar con el diseño para móviles__: Diseñar la interfaz de usuario y la experiencia del usuario teniendo en cuenta las limitaciones de los dispositivos móviles. Esto incluye priorizar el contenido esencial y simplificar la navegación.

2. __Utilizar media queries para adaptar el diseño__: Añadir media queries para adaptar el diseño a tabletas y computadoras de escritorio. Utilizar un enfoque ascendente (desde móviles hacia pantallas más grandes) para garantizar que la experiencia en móviles sea siempre la base.

3. __Optimizar el rendimiento en móviles__: Asegurarse de que la aplicación cargue rápidamente en dispositivos móviles optimizando las imágenes, minificando el código y utilizando técnicas de caché.

4. __Probar en dispositivos reales__: Probar la aplicación en una variedad de dispositivos móviles reales para asegurarse de que funciona correctamente y proporciona una buena experiencia de usuario.

### Gestión de estado
La gestión de estado se refiere a la forma en que una aplicación frontend maneja, almacena y modifica los datos que utiliza para renderizar la interfaz de usuario y responder a las interacciones del usuario. Una gestión de estado eficaz es crucial para construir aplicaciones complejas y mantenibles, especialmente aquellas que requieren interacciones dinámicas y actualizaciones en tiempo real.

Una correcta gestión del estado permite:
- __Predictibilidad__: Una buena gestión de estado hace que el comportamiento de la aplicación sea más predecible. Al centralizar y controlar el estado, es más fácil entender cómo los cambios en los datos afectan la interfaz de usuario.
- __Mantenibilidad__: Facilita el mantenimiento del código al separar la lógica de gestión de datos de la lógica de renderizado de la interfaz de usuario. Esto permite modificar o actualizar la gestión de datos sin afectar el resto de la aplicación.
- __Reusabilidad__: Permite reutilizar el estado y la lógica de gestión de estado en diferentes componentes de la aplicación, reduciendo la duplicación de código.
- __Depuración__: Simplifica la depuración al proporcionar un punto centralizado para inspeccionar y modificar el estado de la aplicación. Las herramientas de gestión de estado a menudo incluyen características que facilitan el seguimiento de los cambios en el estado a lo largo del tiempo.
- __Rendimiento__: Optimiza el rendimiento al permitir que la interfaz de usuario se actualice de manera eficiente solo cuando los datos subyacentes cambian. Esto evita actualizaciones innecesarias y mejora la velocidad de la aplicación.

#### Estado Local
El estado local se refiere a los datos que son relevantes únicamente para un componente específico y no necesitan ser compartidos con otros componentes. Se gestiona directamente dentro del componente, utilizando mecanismos como useState en React o propiedades reactivas en Vue.js.

__Cuando usar estado local?__
Estos son algunos de los casos en los que es mejor considerar usar el estado local:

- __Control de un formulario__:  Cuando un componente maneja un formulario simple y los datos solo se necesitan dentro de ese formulario.
-  __Control de la visibilidad de un modal__: Cuando un componente necesita controlar si un modal está abierto o cerrado.
- __Control de la selección en una lista__: Cuando un componente muestra una lista de elementos y necesita rastrear cuál está seleccionado.

#### Estado Global
El estado global se refiere a los datos que necesitan ser compartidos entre múltiples componentes o que requieren ser accedidos desde diferentes partes de la aplicación. Se gestiona utilizando bibliotecas de gestión de estado como Redux, Vuex, Zustand o Context API.

__Cuando usar estado global?__
Estos son algunos de los casos en los que es mejor considerar usar el estado local:

- __Datos de autenticación del usuario__: Cuando múltiples componentes necesitan conocer si el usuario está autenticado y acceder a su información (nombre, rol, permisos).
- __Configuración de la aplicación__: Cuando múltiples componentes necesitan acceder a la configuración de la aplicación (tema, idioma, ajustes regionales).
- __Carrito de compras__: Cuando múltiples componentes necesitan acceder y modificar el contenido del carrito de compras.

### Interacción con API
La interacción con APIs es fundamental en el desarrollo moderno de aplicaciones. Estas son las mejores prácticas a seguir:

#### Axios
Para realizar peticiones HTTP se recomienda usar [Axios](https://axios-http.com/) como cliente HTTP por sus ventajas:
- Interceptores para manejo global de requests/responses
- Cancelación de peticiones
- Transformación automática de datos JSON
- Protección contra XSRF
- Soporte para progreso de uploads

Configuración recomendada:

```javascript
// axios-instance.js
import axios from 'axios';

const api = axios.create({
  baseURL: process.env.API_BASE_URL,
  timeout: 10000,
  headers: {
    'Content-Type': 'application/json',
    'Accept': 'application/json'
  }
});

// Request interceptor
api.interceptors.request.use(config => {
  const token = localStorage.getItem('access_token');
  if (token) {
    config.headers.Authorization = `Bearer ${token}`;
  }
  return config;
});

// Response interceptor
api.interceptors.response.use(
  response => response,
  error => {
    if (error.response?.status === 401) {
      // Handle token refresh
    }
    return Promise.reject(error);
  }
);

export default api;
```

#### Hooks
Para React, se recomienda crear hooks personalizados para manejar las peticiones API:

```javascript
// useApi.js
import { useState, useEffect } from 'react';
import api from './axios-instance';

function useApi(url, options = {}) {
  const [data, setData] = useState(null);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState(null);

  useEffect(() => {
    const fetchData = async () => {
      try {
        const response = await api(url, options);
        setData(response.data);
      } catch (err) {
        setError(err);
      } finally {
        setLoading(false);
      }
    };

    fetchData();
  }, [url]);

  return { data, loading, error };
}

export default useApi;
```

#### Mensajes de error
Para manejo consistente de errores:
1. Crear un servicio de notificaciones
2. Mapear códigos de error HTTP a mensajes amigables
3. Loggear errores en sistema de monitoreo
4. Mostrar feedback al usuario

Ejemplo de implementación:
```javascript
// error-handler.js
const errorMessages = {
  400: 'Solicitud inválida',
  401: 'No autorizado',
  403: 'Acceso denegado',
  404: 'Recurso no encontrado',
  500: 'Error del servidor',
  default: 'Error inesperado'
};

export function handleApiError(error) {
  const status = error.response?.status;
  const message = errorMessages[status] || errorMessages.default;
  
  // Mostrar notificación al usuario
  showNotification(message, 'error');
  
  // Loggear error
  logError(error);
  
  // Lanzar error para manejo adicional
  throw error;
}
```

#### Caching
Implementar estrategias de caching para mejorar rendimiento:
- Cache en memoria para datos frecuentes
- Cache en localStorage para datos persistentes
- Cache en service workers para offline support

Ejemplo básico:
```javascript
const cache = new Map();

async function fetchWithCache(url) {
  if (cache.has(url)) {
    return cache.get(url);
  }

  const response = await api.get(url);
  cache.set(url, response.data);
  return response.data;
}
```

#### Paginación
Para manejo eficiente de grandes datasets:
- Implementar paginación del lado del servidor
- Usar infinite scroll o paginación numérica
- Prefetch de siguientes páginas

Ejemplo:
```javascript
function usePaginatedApi(url, pageSize = 10) {
  const [page, setPage] = useState(1);
  const [data, setData] = useState([]);
  const [hasMore, setHasMore] = useState(true);

  const fetchMore = async () => {
    const response = await api.get(url, {
      params: { page, pageSize }
    });
    
    setData(prev => [...prev, ...response.data]);
    setHasMore(response.data.length === pageSize);
    setPage(prev => prev + 1);
  };

  return { data, fetchMore, hasMore };
}
```

#### Optimización de peticiones
- Debounce para búsquedas
- Cancelación de peticiones duplicadas
- Throttling para evitar sobrecarga
- Uso de AbortController

Ejemplo:
```javascript
const searchController = new AbortController();

async function search(query) {
  try {
    const response = await api.get('/search', {
      params: { q: query },
      signal: searchController.signal
    });
    return response.data;
  } catch (error) {
    if (axios.isCancel(error)) {
      console.log('Request canceled');
    }
  }
}

// Cancelar petición anterior
searchController.abort();
```

### Pruebas E2E
Las pruebas End-To-End (E2E) son una técnica integral de prueba que simula escenarios de usuario del mundo real para garantizar una funcionalidad, rendimiento y experiencia de usuario perfectos en aplicaciones web, móviles y de escritorio. Estas pruebas verifican todo el flujo de una aplicación desde el inicio hasta el final, abarcando desde la interfaz de usuario hasta la manipulación de datos en la base de datos. El objetivo principal es asegurar que la aplicación funcione correctamente en todas sus partes y que las diferentes funcionalidades se integren sin problemas.

Las pruebas E2E son esenciales para detectar problemas como enlaces rotos, manejo incorrecto de datos, desalineación de elementos de la interfaz de usuario o componentes que no responden, antes de que la aplicación se lance a los usuarios reales. Además, ayudan a identificar posibles problemas de rendimiento, usabilidad y accesibilidad.

#### Cypress
Cypress es una herramienta popular para pruebas E2E que se destaca por su facilidad de uso y velocidad en la ejecución de pruebas. Ofrece una API intuitiva que facilita la creación de pruebas para desarrolladores sin experiencia previa en testing.

Posee ventajas como:

- __Facilidad de uso__: Cypress tiene una API simple y fácil de aprender.
- __Velocidad__: Ejecuta pruebas rápidamente, lo que reduce el tiempo necesario para obtener resultados.
- __Soporte para Navegadores__: Ofrece soporte para múltiples navegadores, permitiendo probar la aplicación en diferentes entornos.
- __Integración con CI/CD__: Se integra bien con herramientas de integración continua y entrega continua.

Ejemplo de uso:
```javascript
describe('My First Test', () => {
  it('Visits the app root url', () => {
    cy.visit('http://localhost:5173')
    cy.contains('h1', 'Bienvenido').should('be.visible')
  })
})
```

#### Playwright
Playwright es una herramienta moderna para pruebas E2E que permite automatizar navegadores de manera eficiente. Ofrece una API similar a Cypress pero con algunas diferencias en la implementación. Es especialmente útil para pruebas que requieren una gran cantidad de interacciones complejas con la interfaz de usuario.

Posee ventajas como:
- __Flexibilidad__: Ofrece una gran flexibilidad en la automatización de navegadores, incluyendo Chrome, Firefox y WebKit.
- __Rendimiento__: Es muy rápido en la ejecución de pruebas, comparable a Cypress.
- __Soporte para Múltiples Navegadores__: Permite probar la aplicación en diferentes navegadores simultáneamente.
- __Menor Sobrecarga de Memoria__: Consumo de memoria más eficiente en comparación con otras herramientas.

Ejemplo de uso:
```javascript
import { test, expect } from '@playwright/test';

test('navigates to and verifies MongoDB Designer URL', async ({ page }) => {
  await page.goto('http://localhost:5173');
  await page.getByRole('link', { name: 'Launch MongoDB Designer' }).click();
  await expect(page).toHaveURL('http://localhost:5173/editor.html');
});
```

#### Buenas prácticas
__1. Organización de Pruebas__
- __Estructura Modular__: Organiza las pruebas en módulos o archivos separados según la funcionalidad que se esté probando.
- __Nomenclatura Clara__: Usa nombres claros y descriptivos para los archivos y funciones de prueba.

__2. Integración Continua__
- __Automatización de Pruebas__: Integra las pruebas E2E en un ciclo de integración continua para asegurar que cada cambio en el código no rompa la funcionalidad existente.
- __Notificaciones__: Configura notificaciones para alertar a los desarrolladores sobre fallos en las pruebas.

__3. Optimización del Tiempo de Ejecución__
- __Paralelización__: Ejecuta pruebas en paralelo para reducir el tiempo total de ejecución.
- __Optimización de Código__: Asegúrate de que el código de las pruebas esté optimizado para evitar retrasos innecesarios.

__4. Mantenimiento Regular__
- __Revisión Periódica__: Revisa periódicamente las pruebas para asegurarte de que siguen siendo relevantes y efectivas.
- __Actualización de Pruebas__: Actualiza las pruebas cuando se agregan nuevas funcionalidades o se modifican las existentes.

__5. Documentación__
- __Documentación de Pruebas__: Mantén una documentación clara sobre cómo ejecutar las pruebas y qué se está probando.
- __Compartir Conocimiento__: Comparte el conocimiento sobre las pruebas entre los miembros del equipo para fomentar la colaboración.

Siguiendo estas buenas prácticas, puedes asegurar que tus pruebas E2E sean efectivas, mantenibles y contribuyan al éxito de tu proyecto.

### Herramientas para Frontend
Este espacio es usado como una recopilación de herramientas y recursos que todo desarrollador frontend debe disponer a la mano.

#### Lighthouse
[Lighthouse](https://chromewebstore.google.com/detail/lighthouse/blipmdconlkpinefehnmjammfjpmpbjk?hl=es&pli=1) es una herramienta de código abierto, automatizada, desarrollada por Google, que sirve para analizar la calidad de las páginas web. Se utiliza para auditar diferentes aspectos de una página, proporcionando informes detallados sobre:

- __Rendimiento__: Evalúa la velocidad de carga y la optimización de la página.
- __Accesibilidad__: Verifica si la página sigue las mejores prácticas para ser accesible a todos los usuarios, incluyendo aquellos con discapacidades.
- __SEO__: Analiza si la página está optimizada para ser encontrada y rankeada por los motores de búsqueda.
- __Buenas prácticas__:  Comprueba si la página sigue las mejores prácticas de desarrollo web moderno.
- __Progressive Web App(PWA)__: Si la página es una PWA, verifica si cumple con los requisitos para ser una aplicación web progresiva.

Lighthouse utiliza varias métricas para evaluar el rendimiento de una página web:
- __First Contentful Paint (FCP)__: Mide el tiempo que tarda el navegador en renderizar el primer elemento de contenido (texto, imagen, etc.) en la pantalla.
- __Largest Contentful Paint (LCP)__: Mide el tiempo que tarda en renderizarse el elemento de contenido más grande visible en la ventana gráfica.
- __Speed Index__: Mide la rapidez con la que se muestra visualmente el contenido de la página durante la carga.
- __Time to Interactive (TTI)__: Mide el tiempo que tarda la página en volverse completamente interactiva, es decir, cuando los usuarios pueden interactuar con todos los elementos de la interfaz.
- __Total Blocking Time (TBT)__: Mide el tiempo total durante el cual la página está bloqueada y no puede responder a las interacciones del usuario.
- __Cumulative Layout Shift (CLS)__: Mide la estabilidad visual de la página, es decir, cuánto cambian de posición los elementos mientras se carga la página.
## Backend
En el backend manejaremos todo lo relacionado a la lógica de negocios, por lo que involucrará a todos aquellos servicios de almacenamiento y procesamiento interno, por lo que resulta importante mantener una estructura en base a protocolos conocidos y buenas practicas.
### API
Al momento de levantar un servicio interno se debe garantizar la interacción fluida y monitoreable entre los distintos servicios y aplicaciones de software, por lo que es importante definir a profundidad los estandares en la construcción de una API.
#### Rest
Para la construcción de HTTP APIs debemos manejar los estandares de Rest. Lo que en esencia involucra:
- Nomenclatura de [endpoints](https://vicente-aguilera-perez.medium.com/las-10-mejores-pr%C3%A1cticas-para-nombrar-api-rest-endpoints-48b8bcbd1397).
	- Versionamiento: Se opta por manejar versiones en la URL. Ej: `/v1/users/`
- Uso de los métodos HTTP:
	- GET: Lectura y obtención de datos
	- POST: Escritura de datos o disparador de eventos.
	- PUT: Actualizar todo un recurso existente o crear uno nuevo si no existe. 
	- PATCH: Actualizar parcialmente un recurso existente.
	- DELETE: Eliminar un recurso existente.
- Transmisión y manipulación de datos en formato [JSON](https://www.json.org/json-en.html)
- Uso de [Estados HTTP] en las respuestas del servidor. Las comunmente usuadas son:
	- 2xx: Operación exitosa
		- 200: OK
		- 201: CREATED
	- 4xx: Errores del cliente
		- 400 - BAD REQUEST
		- 401 - UNAUTHORIZED
		- 403 - FORBIDEN
		- 404 - NOT FOUND
		- 409 - CONFLICT
	- 5xx: Errores del servidor
		- 500: INTERNAL SERVER ERROR
		
	> Mas adelante en la lectura se retoma la importancia de los estados HTTP  en el manejo de errores.
#### Seguridad
Es necesario establecer un mínimo estandard de seguridad ante el manejo de la información sensible y el acceso a la misma. Por suerte ya existen buenas practicas que nos permiten minimizar los riesgos, sin embargo es importante recordar que la seguridad es un conjunto de múltiples estrategias combinadas.

##### Autenticación y autorización
La __autenticación__ se refiere a la validación de la identidad de los usuarios o entidades que tienen acceso al sistema. Sirve como una primera capa de seguridad y de esta podemos considerar los siguientes métodos:
- [JWT]() Para el manejo de sesiones de usuarios con `access_token` de 15 minutos y `refresh_token` para mantener las sesiones activas de manera segura.
- [Bcrypt]() como algoritmo de hash para almacenar las contraseñas de usuarios de manera segura en las base de datos.
- API Keys de _32 bytes_ de longitud como mínimo en la comunicación entre servicios internos. Ej: `AH3epiBfvrHJOikRbNKuHk2jQpvrp11YVdE+knnwtIE=`. 

> __NO__ usar la clave en el ejemplo. Si necesita una nueva API Key, genere una clave nueva.

Por otro lado la __autorización__ es el proceso mediante el cual, una vez validada la identidad en el paso anterior, se valida que clase de permisos tiene y que operaciones puedes efectuar dentro del sistema. Con este fin se diseñan los sistemas con una estructura de [RBAC]() (Role Based Access Control), en el cual un usuario puede tener un rol asignado, y ese rol una serie de permisos sobre los recursos del sistema. En nuestro caso manejaremos la siguiente estrucutra:
- __Módulos__: El listado de los recursos del sistema. Ej: Nómina, Inventario, etc.
- __Permisos__: El listado de operaciones que puede ejecutar un usuario sobre un modulo:
	- __Leer(read)__: Lectura de datos. 
	- __Crear(create)__: Insertar un nuevo recurso. 
	- __Actualizar(update)__: Actualizar un recurso existente. 
	- __Actualizar propio(update_self)__: Permite actualizar recursos únicamente creados por el usuario.
	- __Eliminar(delete)__: Eliminar un recurso existente. 
	- __Eliminar propio(delete_self)__: Permite eliminar recursos únicamente creados por el usuario.
	- __Todos(all)__: Todas las operaciones son permitidas.
- __Roles__: Un rol es un titulo que agrupa un conjunto de permisos y que puede ser asignado a un usuario. Ej: administrador, ténico, contador, etc.

De modo que relación entre un rol y los permisos asignados estaría determinada por: Rol -> Modulos -> Permisos. Por ejemplo, consideremos un rol técnico(technician):

```shell
# @ = role
# * = module
# - = permission

@technician:
	* clients
		- read
	* inventory
		- read
		- update
	* tech_support
		- all
```

En este ejemplo un usuario asignado con el rol de técnico(technician) tendría permisos de lectura de la información de los clientes, sin embargo no puede crear nuevos clientes o modificar la información existente, igualmente con inventario, un ténico podría ver los elementos del inventario y actualizar la existencia de un item, sin embargo no puede crear o eliminar nuevos, por último el técnico tiene todos los permisos dentro del módulo de soporte técnico.

#### CORS
[Cross-Origin Resource Sharing](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS) es un mecanismo de seguridad implementado por los navegadores web que permite o restringe solicitudes HTTP entre diferentes orígenes (dominios, protocolos o puertos). Su objetivo es proteger a los usuarios de ataques maliciosos como el robo de datos, al garantizar que solo recursos autorizados puedan acceder a una API.

Las políticas de CORS son necesarias para asegurar un nivel de seguridad para permitir solicitudes entre dominios y evitar el acceso no autorizado, por esta razón hay un conjunto de requerimientos mínimos a configurar:

- __Origenes permitidos__: `Access-Control-Allow-Origin: https://example.thundernet.com`

- __Métodos HTTP permitidos__: `Access-Control-Allow-Methods: GET, POST, PUT, DELETE`

- __Headers permitidos__: `Access-Control-Allow-Headers: Content-Type, Authorization`

- __Permitir credenciales__: `Access-Control-Allow-Credentials: true`

Aunque CORS es necesario al levantar un proyecto en un servidor, cada configuración puede variar segun el entorno y durante el desarrollo puede ser incluso incómodo tener reglas restrictivas, por lo que es una buena práctica mantener la configuracion de las políticas en variables de entorno. Ej:

```shell
# .env file

# SERVER
HOST=0.0.0.0
PORT=8080

# CORS
CORS_ORIGIN=* # or https://example.thunder.com
CORS_METHODS=* # or GET,POST,PUT,PATCH,DELETE
CORS_HEADERS=* # or Conent-type,Authorization
CORS_CREDENTIALS=true

# ...
```

Este enfoque permite mantener una configuración distinta en multiples entornos de manera eficiente.

#### Rate Limiting

El rate limiting (límite de tasa) es un mecanismo de control que restringe el número de solicitudes que un cliente (usuario, IP, aplicación, etc.) puede realizar a una API o servicio en un período de tiempo específico. Su objetivo es prevenir el abuso, proteger contra ataques DDoS, garantizar la estabilidad del sistema y distribuir recursos de manera equitativa.

Existen varias estrategias de aplicación de rate limiting con distintos enfoques:

- __Fixed Window (Ventana Fija)__:  Limita las solicitudes a un número máximo en intervalos fijos (ej: 100 solicitudes por minuto). Si un cliente envía 100 solicitudes en el primer minuto, deberá esperar al siguiente minuto para enviar más.

- __Sliding Window (Ventana Deslizante)__: Calcula las solicitudes en una ventana de tiempo móvil (ej: últimos 60 segundos).  Si el límite es 100 solicitudes por minuto, las solicitudes se cuentan en intervalos continuos, no en bloques fijos.

- __Token Bucket (Cubeta de Tokens)__:   Los clientes consumen "tokens" (ej: 1 token por solicitud), que se reponen a una tasa fija. Un balde con 100 tokens se recarga a 1 token por segundo. Si se agotan, el cliente debe esperar.

- __Leaky Bucket (Cubeta con Fugas)__: Las solicitudes entran en un "balde" que se vacía a una tasa constante. Si el balde tiene capacidad para 100 solicitudes y una tasa de 10 solicitudes/segundo, excederlo genera rechazos.

- __Rate Limiting por IP o Usuario__:  Aplica límites basados en atributos del cliente (IP, ID de usuario, API key). Ej: 1000 solicitudes/día por usuario.

En nuestro caso optamos por la implementación de [Token Bucket](https://jgam.medium.com/rate-limiter-token-bucket-algorithm-efd86758c8ee) debido a sus ventajas, tales como:
1. __Control de rafagas__: Los clientes pueden usar tokens acumulados para picos cortos.
2. __Simplicidad__: Fácil de implementar con sistemas como Redis para almacenar tokens.

> La estrategia de rate limiting a usar puede cambiar y aun esta por definirse.


### Documentación
La documentación es una pieza esencial para el mantenimiento de un sistema de software, y la APIs no son la excepción, por suerte hoy en día existen varias tecnologías que optimizan este proceso, por lo que cada API debe contener su propia documentación interactiva que permita a otros desarrolladores interactuar fácilmente con esta.

#### Swagger
[Swagger](https://swagger.io/) es una herramienta  bastante sencilla y útil de implementar para una API por un conjunto de beneficios:
- Corre en el servidor y puede usarse desde cualquier navegador.
- Se construye a medidas que desarrollas.
- Usa estandares como la especificación [Open API](https://swagger.io/resources/open-api/).
- Permite a cualquier desarrollador como interactuar con la API en tiempo real.

Aunque ciertamente incluye algunas desventajas mencionables:
- Dificultad de lectura en APIs grandes.
- Es dificil restringir su acceso a personal autorizado unicamente.

Debido a esto es una herramienta a considerar en APIs internas y proyectos pequeños.
#### Postman
[Postman](https://www.postman.com/) es una herramienta bastante versatil y profesional que ofrece múltiples beneficios para los desarrolladores a la hora de documentar y probar las APIs, tales como:
- Permite gestinar todo un workspace, por lo que varias APIs pueden gestionarse en la misma aplicación.
- Creación de colecciones de peticiones.
- Manejo de variables de entorno.
- Ejecución de scripts.
- Configuración de pruebas.

Es una herramienta lider en el mercado con varios años de recorrido, vale la pena incluir un directorio de `collections` en los proyectos.

### Manejo de errores
El software es un ecosistema lejos de ser perfecto, aun implementando multiples estrategias de desarrollo, pruebas, arquitectura y diseño, los bugs son inevitables, por lo que la intención es detectarlos lo antes posible y reducir el impacto de aquellos que aun no han sido detectados, además los errores pueden contener información sensible del sistema, lo que puede ser explotado por agentes maliciosos, por lo que es necesario idear un plan de como lidiar con los errores.

En una API pueden suceder dos tipos de errores (sin contar errores de lógica de programación) que pueden romper con el flujo natural del sistema:

Los errores introducidos del lado del cliente:
- Envío de datos inválidos.
- Intentos de acceso a recursos sin la autorización correspondiente.
- Inteno de acceso a recursos que no existen.

Y los errores que suceden internamente en el servidor:
- Errores en la interacción o conexión con la base de datos.
- Un error provocado por no validar casos de valores NULL.

Por lo que es importante identificar un caso o el otro y tomar las acciones necesarias.

#### Códigos de HTTP
Al momento de notificar un error al frontend es importante usar los protocolos correctos para idenficiar los errores de manera sencilla. Estos son algunos casos:

- __400 - Bad Request__: Es usado cuando se recibe una petición desde el cliente que no envía todos los valores requeridos para procesar la petición. Ejemplo la ausencia del Body JSON o de un HEADER necesario en la operación
- __401 - Unauthorized__: Es usado cuando se recibe una petición a un recurso protegido y no se ha podido validar el tonen de autenticación, ya sea porque no es válido, el token haya expirado o simplemente no se ha encontrado.
- __403 - Forbiden__: Es usado cuando se recibe una petición a un recurso protegido, se ha validado el token de autenticación, sin embargo el usuario o cliente no posee los permisos para acceder a ese recurso.
- __404 - Not Found__: Es usado cuando no se ha podido encontrar algún recurso al cual se ha tratado de acceder.
- __409 - Conflict__: Es usado cuando una petición ha querido ejecutar una acción la cual podría provocar un conflicto en la base de datos o los recursos del servidor, un ejemplo claro sería cambiar un registro para adoptar el valor único de un registro ya existente. Ej: Actualizar el correo de un usuario por el correo de otro usuario en la base de datos.
- __422 - Unprocessable Entity__: Cuando se recibe una petición desde el cliente, la cual, a diferencia del error _400_, se reciben todos los datos necesarios, sin embargo no se cumplen las validaciones especificadas por el servidor, como los formatos de los datos envidados.
- __429 - Too Many Requests__: Es usado cuando se sobrepasa el límite de tasas. [Ver rate limiting](#rate%20limiting).
- __500 - Internal Server Error__: Es usuado cuando ocurre un error que no ha sido mapeado o considerado al realizar un proceso, por lo que es importante que el mensaje de error enviado al cliente no sea explícito, ya que el mensaje de lo verdaderamente ocurrido debe mostrarse en los logs del servidor o generar alguna acción de notificación al servicio ténico, mas nunca debe exponerse al cliente por motivos de seguridad.


#### Respuestas
Podemos definir un mensaje de error desde la API tomando el siguiente formato:
- __status__: integer
- __error__: 
	- __message__: string
	- __details__: string
	- __endpoint__: string
	- __timestamp__: datetime

Dentro del mensaje de error tenemos:
- __message__: Un mensaje general sobre el error ocurrido, este puede ser aprovechado por el frontend a modo de feedback para el cliente.
- __details__: Se usa a modo de completar la idea del mensaje general y este puede ser un string o un arreglo de strings.
- __endpoint__: Registro del endpoint en donde se produjo el error.
- __timestamp__: Registro del momento en que ocurre el error.

Por lo que finalmente algunos ejemplos de respuestas de errores podrían ser:
```json
{
	"status": 404,
	"error": {
		"message": "usuario no encontrado",
		"details": "no se ha encontado usuario con el correo john.doe@gmail.com",
		"endpoint": "/users?email=john.doe@gmail.com",
		"timestamp": "2023-10-15T14:30:45Z",
	}
}

{
	"status": 401,
	"error": {
		"message": "correo o contraseña inválidos",
		"details": "las credenciales enviadas son incorrectas o no existen.",
		"endpoint": "/auth/login",
		"timestamp": "2023-10-15T14:30:45Z",
	}
}

{
	"status": 500,
	"error": {
		"message": "Error al elminar usuario",
		"details": "Ha ocurrido un error inesperado durante la eliminación del usuario.",
		"endpoint": "/users/123456",
		"timestamp": "2023-10-15T14:30:45Z",
	}
}
```

### Migraciones
Las migraciones son un mecanismo esencial para gestionar la evolución del esquema de la base de datos de manera controlada y predecible. Permiten aplicar cambios al esquema (creación de tablas, adición de columnas, etc.) de forma automatizada y reversible.

- __Control de versiones__: Las migraciones deben gestionarse como código fuente, idealmente dentro del mismo repositorio del proyecto, para garantizar la coherencia entre el código de la aplicación y el esquema de la base de datos.

- __Atomicidad__: Cada migración debe ser atómica, es decir, debe representar un cambio único y lógico en el esquema. Esto facilita el seguimiento de los cambios y la reversión en caso de errores.

- __Reversibilidad__: Cada migración debe tener una operación de reversión (un "undo") que permita deshacer los cambios aplicados. Esto es fundamental para corregir errores o realizar rollbacks a versiones anteriores.

- __Nombrado descriptivo__: Los archivos de migración deben tener nombres descriptivos que indiquen el cambio que realizan. Incluir una marca de tiempo en el nombre del archivo puede ayudar a mantener un orden cronológico. Ejemplo: _20250224103000_create_users_table.sql_ (indica la creación de la tabla "users" con la fecha y hora).

- __Entorno__ : Es importante considerar el entorno de destino al crear migraciones.

- __Transacciones__: Las operaciones dentro de una migración deben ejecutarse dentro de una transacción para garantizar la consistencia de la base de datos en caso de fallos.

- __Pruebas__: Las migraciones deben probarse exhaustivamente en un entorno de desarrollo antes de aplicarse a entornos de producción.

### Pruebas
Las pruebas son una parte fundamental del desarrollo de software para garantizar la calidad, confiabilidad y correcto funcionamiento de la aplicación.

#### TDD
El Desarrollo Dirigido por Pruebas ([TDD](https://www.browserstack.com/guide/what-is-test-driven-development)) es una metodología de desarrollo en la que las pruebas unitarias se escriben antes de implementar el código de la aplicación. Este enfoque ayuda a definir claramente los requisitos y el comportamiento esperado del código desde el principio.

- __Ciclo Red-Green-Refactor__: El proceso de TDD sigue un ciclo de tres pasos:
	- __Red__: Escribir una prueba que falle (porque aún no hay código que la satisfaga).
	- __Green__: Escribir el código mínimo necesario para que la prueba pase.
	- __Refactor__: Refactorizar el código para mejorar su estructura, legibilidad y mantenibilidad, sin cambiar su comportamiento.
- __Pruebas unitarias__: El foco principal de TDD son las pruebas unitarias, que verifican el comportamiento de unidades de código individuales (funciones, métodos, clases) de forma aislada.
- __Cobertura__: Apuntar a una alta cobertura de pruebas para asegurar que la mayor parte del código esté siendo probado. Sin embargo, la cobertura no es el único indicador de la calidad de las pruebas; también es importante la calidad y relevancia de las pruebas en sí mismas.
- __Automatización__:  Las pruebas deben ser automatizadas para que puedan ejecutarse de forma rápida y repetible como parte del proceso de desarrollo e integración continua.

#### Rendimiento
Las pruebas de rendimiento son importantes para evaluar la capacidad de la aplicación para manejar la carga esperada y garantizar una experiencia de usuario óptima.

- __Identificar cuellos de botella__: Utilizar herramientas de perfilamiento y monitoreo para identificar las áreas del código que están causando problemas de rendimiento. 
- __Simular carga realista__: Diseñar pruebas que simulen la carga de usuarios y patrones de uso reales.
- __Definir métricas clave__: Establecer métricas claras para medir el rendimiento, como el tiempo de respuesta, la tasa de errores y el uso de recursos (CPU, memoria, disco).
- __Automatizar pruebas de rendimiento__: Integrar las pruebas de rendimiento en el proceso de integración continua para detectar problemas de rendimiento de forma temprana.
- __Optimizar consultas a la base de datos__: Revisar y optimizar las consultas a la base de datos para asegurar que sean eficientes y no causen cuellos de botella.
- __Implementar cache__: Utilizar mecanismos de caché para reducir la carga en la base de datos y mejorar los tiempos de respuesta.

##### Herramientas
Algunas herramientas últiles para realizar este tipo de pruebas son:

- [k6](https://youtu.be/ghuo8m7AXEM?si=4tjsqhzNm1dLygkW): Herramienta de pruebas de carga moderna, escrita en Go, con scripting en JavaScript.
- [Postman/Newman](https://learning.postman.com/docs/collections/using-newman-cli/continuous-integration/): Aunque principalmente herramientas para desarrollo y testing de APIs, Newman (la versión CLI de Postman) puede ser integrada en pipelines de automatización para ejecutar colecciones de pruebas de rendimiento.

##### Estrategias
- __Rate limiting__: Probar que el rate limiting funciona correctamente, verificando que se rechacen las solicitudes que excedan el límite configurado y que se devuelvan los códigos de error HTTP apropiados (ej., 429 Too Many Requests).

- __Filtros y paginación__:  Asegurar que los filtros aplicados a las consultas de la API funcionen de manera eficiente y que la paginación se implemente correctamente para evitar sobrecargar el servidor con grandes conjuntos de datos.

- __Validación de entrada__: Probar que la API maneje correctamente las entradas inválidas, devolviendo errores descriptivos y evitando que las entradas incorrectas causen fallos en el sistema.

- __Manejo de errores__: Verificar que la API maneje correctamente los errores inesperados, como fallos en la base de datos o servicios externos, devolviendo códigos de error HTTP apropiados y mensajes de error informativos.

- __Pruebas de seguridad__: Realizar pruebas de seguridad para detectar posibles vulnerabilidades, como inyección SQL, cross-site scripting (XSS) y otras amenazas comunes.

- __Pruebas de integración__: Verificar que la API se integre correctamente con otros sistemas y servicios, como bases de datos, colas de mensajes y otros componentes de la arquitectura.

- __Pruebas de concurrencia__: Simular múltiples usuarios accediendo a la API simultáneamente para identificar posibles problemas de concurrencia, como bloqueos o condiciones de carrera.

##### Tipos de prueba:
- __Pruebas de carga (Load testing)__: Evalúa el rendimiento del sistema bajo una carga esperada. Determina cómo se comporta el sistema en condiciones normales y verifica si cumple con los requisitos de rendimiento. 
- __Pruebas de estrés (Stress testing)__:  Lleva el sistema al límite de sus capacidades para identificar puntos de falla y cuellos de botella. Ayuda a determinar la capacidad máxima del sistema y cómo se recupera después de una falla.
- __Pruebas de pico (Spike testing):__ Simula aumentos repentinos y extremos en la carga para evaluar cómo el sistema responde a picos inesperados de tráfico.
- __Pruebas de resistencia (Soak testing)__: Prueba la estabilidad del sistema bajo una carga constante y prolongada durante un período de tiempo prolongado (ej., varias horas o días). Ayuda a identificar problemas de memoria, fugas de recursos y otros problemas que pueden surgir con el tiempo. 
