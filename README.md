# Documentación para Desarrolladores

¡Bienvenido a nuestro proyecto Obsidian Vault! Esta documentación te guiará a través del proceso de configuración y contribución a este proyecto.

## Requisitos Previos

Antes de comenzar, asegúrate de tener instalado lo siguiente en tu sistema:
- [GitHub Desktop](https://desktop.github.com/)
- [Obsidian](https://obsidian.md/download)

## Primeros Pasos

### 1. Clonar el Repositorio usando GitHub Desktop

1. Abre GitHub Desktop
2. Haz clic en "File" > "Clone Repository"
3. Selecciona "URL" e ingresa: `https://github.com/spyro-esserweb/obsidian-vault.git`
4. Elige tu ruta local
5. Haz clic en "Clone"

### 2. Configurar Obsidian

1. Abre Obsidian
2. Haz clic en "Abrir carpeta como bóveda"
3. Navega hasta la carpeta del repositorio clonado
4. Selecciona la carpeta y haz clic en "Abrir"

### 3. Conceptos Básicos de la Interfaz de Obsidian

1. **Descripción General de la Interfaz**
   - Barra lateral izquierda: Explorador de archivos y búsqueda
   - Barra lateral derecha: Propiedades, enlaces retroactivos y enlaces salientes
   - Área central: Panel de editor/vista previa

2. **Funciones Esenciales**
   - Crear nueva nota: Clic en "Nueva nota" o Ctrl/Cmd + N
   - Crear nueva carpeta: Clic derecho en explorador > "Nueva carpeta"
   - Enlazar notas: Usa `[[` para crear enlaces internos
   - Modo vista previa: Clic en icono de vista previa o Ctrl/Cmd + E
   - Vista de grafo: Clic en icono de grafo en la barra lateral

3. **Plugins Recomendados**
   - Explorador de archivos
   - Búsqueda
   - Cambio rápido
   - Vista de grafo
   - Enlaces retroactivos
   - Vista previa de página

## Trabajando con GitHub Desktop

### Flujo de Trabajo Diario

1. **Antes de Comenzar a Trabajar**
   - Abre GitHub Desktop
   - Haz clic en "Fetch origin" para obtener cambios recientes
   - Haz clic en "Pull origin" si hay cambios disponibles

2. **Creando una Rama**
   - Haz clic en "Current Branch"
   - Haz clic en "New Branch"
   - Nombra tu rama (ej., "feature/nueva-documentacion")
   - Haz clic en "Create Branch"

3. **Realizando Cambios**
   - Haz tus cambios en Obsidian
   - Regresa a GitHub Desktop
   - Revisa los cambios en la pestaña "Changes"
   - Escribe un resumen y descripción
   - Haz clic en "Commit to [nombre-rama]"

4. **Subiendo Cambios**
   - Haz clic en "Push origin" para subir tus cambios
   - Para ramas nuevas: Haz clic en "Publish branch"

5. **Creando Pull Requests**
   - Haz clic en "Create Pull Request"
   - Revisa tus cambios en GitHub
   - Añade descripción y revisores
   - Envía el pull request

### Mejores Prácticas

1. **Organización de la Bóveda**
   - Mantén las notas relacionadas en carpetas apropiadas
   - Usa convenciones de nombres consistentes
   - Crea enlaces significativos entre notas

2. **Prácticas de Git**
   - Fetch y pull antes de comenzar a trabajar
   - Crea mensajes de commit significativos
   - Mantén los commits enfocados y atómicos
   - Revisa tus cambios antes de hacer commit

3. **Colaboración**
   - Documenta cambios significativos
   - Usa pull requests para cambios mayores
   - Discute cambios con miembros del equipo
   - Revisa pull requests de otros

## Consejos y Trucos de Obsidian

1. **Atajos de Teclado**
   - Ctrl/Cmd + O: Abrir cambio rápido
   - Ctrl/Cmd + P: Abrir paleta de comandos
   - Ctrl/Cmd + Clic: Abrir nota en nuevo panel
   - Ctrl/Cmd + G: Abrir vista de grafo

2. **Características de Markdown**
   - Encabezados: Usa # para diferentes niveles
   - Listas: Usa - o * para viñetas
   - Tareas: Usa - [ ] para casillas
   - Bloques de código: Usa ``` para código cercado

3. **Características Avanzadas**
   - Etiquetas: Usa #nombre-etiqueta
   - Alias: Añade en frontmatter YAML
   - Notas incrustadas: Usa ![[nombre-nota]]
   - CSS personalizado: Edita en configuración de apariencia

## Solución de Problemas

### Problemas Comunes

1. **Problemas de Sincronización en GitHub Desktop**
   ```
   - Haz clic en Repository > Remove
   - Vuelve a clonar el repositorio
   - Reinicia tu rama a origin
   ```

2. **Problemas con la Bóveda de Obsidian**
   - Recargar app: Ctrl/Cmd + R
   - Reconstruir caché: Ajustes > Sincronización > Forzar sincronización completa
   - Verificar permisos de archivos

3. **Conflictos de Fusión**
   - Usa la herramienta de fusión integrada de GitHub Desktop
   - Abre archivos con conflictos en tu editor de texto
   - Resuelve conflictos manualmente
   - Haz commit de los cambios resueltos

## ¿Necesitas Ayuda?

Si encuentras problemas o tienes preguntas:
1. Consulta esta documentación
2. Revisa la [Ayuda de Obsidian](https://help.obsidian.md)
3. Consulta la [Documentación de GitHub Desktop](https://docs.github.com/es/desktop)
4. Contacta a los miembros del equipo
5. Crea un issue en el repositorio de GitHub

---
*Última actualización: 21 de enero de 2025*
