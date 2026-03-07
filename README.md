# Proyecto Integrador: Nivel 2 - Front 2 (React)

## Documento de Entregables Detallados

### Objetivo General de la Materia

El objetivo de esta materia es evolucionar las maquetas del Nivel 1 hacia una aplicacion SPA con React. Los estudiantes deben construir interfaces reutilizables con componentes, manejar estado y rutas, e integrar el frontend con una API REST ya construida en Spring Boot.

### Requerimientos de Entrega y Repositorio (GitHub)

La entrega final del proyecto se gestionara exclusivamente a traves de un repositorio de GitHub.

- **Flujo de trabajo (Fork):** Cada equipo debe hacer un `fork` del repositorio base original proporcionado.
- **Nombre del repositorio:** El repositorio forkeado debe tener exactamente el mismo nombre del repositorio original.
- **Nombre de carpeta interna del proyecto:** Dentro del repositorio forkeado se debe crear una carpeta con exactamente el nombre del modulo asignado (por ejemplo: `modulo-1-autenticacion-y-registro`, `modulo-2-catalogo-de-cursos`, etc. en `kebab-case`).
- **Archivo `README.md`:** El repositorio del equipo debe contener un archivo `README.md` en la raiz.
- **Contenido del `README.md`:** Debe incluir:
  - Descripcion y documentacion tecnico-funcional del modulo asignado.
  - Lista completa de integrantes del equipo (nombres y apellidos).

---

### Requerimientos Tecnicos Globales (Obligatorios)

Estos requerimientos aplican a todos los modulos y son base de evaluacion de buenas practicas.

**1. Convenciones de Nomenclatura**

- **`kebab-case`:** Uso obligatorio para carpetas, archivos y clases CSS.
- **`camelCase`:** Uso obligatorio para variables, funciones, hooks personalizados y propiedades JS.
- **`PascalCase`:** Uso obligatorio para componentes React.

**2. Estructura del Proyecto React**

- Se debe usar una estructura clara y modular.
- Estructura sugerida:

```txt
/ (raiz del proyecto)
  package.json
  README.md
  .env
/public
/src
  /app            (config global de app y rutas)
  /pages          (vistas por modulo)
  /components     (componentes reutilizables)
  /services       (consumo de API y cliente HTTP)
  /hooks          (hooks personalizados)
  /context        (estado global, si aplica)
  /utils          (helpers, validaciones, formateos)
  /assets         (imagenes, iconos, etc.)
  /styles         (estilos globales y variables)
  main.jsx
```

**3. Integracion con API Spring Boot (Fuente de Verdad)**

- El frontend debe consumir una API REST ya creada con Spring Boot.
- **No se trabaja con Spring Security en backend**, por lo tanto no se exige implementacion de OAuth/JWT o guards de token obligatorios desde backend.
- La fuente de verdad principal es la API (no `localStorage`).
- `localStorage` solo puede usarse para estado de UI o sesion simulada minima (por ejemplo, datos basicos de usuario logueado), cuando el modulo lo requiera.
- Se recomienda centralizar llamadas HTTP en `src/services` usando `fetch` o `axios`.
- La URL base de la API debe manejarse por variable de entorno (`.env`, por ejemplo `VITE_API_URL`).

**4. Librerias Permitidas y Recomendadas**

- Se permite usar `sweetalert2` para feedback de exito, error, confirmaciones y alertas de validacion.
- Si se usa React Router, debe implementarse navegacion declarativa entre vistas.
- Si se usa manejo de estado global, mantener separacion clara entre estado de UI y datos remotos.

---

### Modulo 1: Autenticacion y Registro

**Objetivo del modulo:** Validar formularios del lado del cliente y simular/integrar el flujo de inicio de sesion y registro consumiendo API, gestionando navegacion React.

**Vistas involucradas:** `Login`, `Registro`, `Recuperar`

**Lista de requerimientos:**

- [ ] Gestionar envio de formularios con React (sin recarga de pagina).
- [ ] Implementar validacion en tiempo real para confirmacion de contrasena en registro.
- [ ] Validar campos obligatorios antes de enviar al backend.
- [ ] Mostrar errores de validacion y de API en pantalla (mensajes cercanos a campos y/o alertas con `sweetalert2`).
- [ ] Aplicar estilos condicionales segun estado de validacion.
- [ ] Login: consumir endpoint de autenticacion/usuarios para verificar credenciales.
- [ ] Si login es exitoso, guardar estado de sesion minima en cliente y redirigir a vista principal.
- [ ] Registro: consumir endpoint de creacion de usuario y redirigir al login al finalizar.
- [ ] Recuperar: validar correo y mostrar mensaje generico de confirmacion (exista o no en sistema).

### Modulo 2: Catalogo de Cursos

**Objetivo del modulo:** Renderizar informacion dinamica de cursos desde API y aplicar filtros interactivos sin recargar.

**Vistas involucradas:** `Cursos`, `Categorias`

**Lista de requerimientos:**

- [ ] Cargar cursos consumiendo endpoint de cursos al montar la vista.
- [ ] Renderizar tarjetas de cursos con componentes React.
- [ ] Implementar estado de carga, estado vacio y manejo de error de consumo.
- [ ] Implementar filtro por categoria sin recargar la pagina.
- [ ] Al cambiar filtro, actualizar listado renderizado en tiempo real.
- [ ] (Opcional avanzado) Mostrar contador por categoria.

### Modulo 3: Gestion de Inscripciones

**Objetivo del modulo:** Implementar flujo de inscripcion entre vistas, sincronizando estado con API.

**Vistas involucradas:** `DetalleCurso`, `ProcesoInscripcion`, `MisCursos`, `Confirmacion`

**Lista de requerimientos:**

- [ ] Desde detalle, permitir iniciar inscripcion del curso seleccionado.
- [ ] En proceso de inscripcion, cargar datos completos del curso desde API.
- [ ] Confirmar inscripcion consumiendo endpoint de inscripciones (POST).
- [ ] Redirigir a vista de confirmacion al finalizar inscripcion.
- [ ] En "Mis Cursos", renderizar tabla/listado dinamico de cursos del usuario.
- [ ] Si no hay usuario en sesion simulada, mostrar estado vacio o mensaje de acceso.

### Modulo 4: Asistencia y Evaluaciones

**Objetivo del modulo:** Renderizar tablas dinamicas desde API para calificaciones y asistencias, aplicando estilos condicionales.

**Vistas involucradas:** `MisCalificaciones`, `HistorialAsistencia`

**Lista de requerimientos:**

- [ ] Consumir endpoints de calificaciones y asistencias del usuario.
- [ ] Renderizar filas dinamicas con componentes de tabla/lista.
- [ ] Si no existe sesion simulada, mostrar estado vacio sin romper la app.
- [ ] Aplicar estilo condicional cuando asistencia sea "Ausente" o "Tardanza".

### Modulo 5: Perfil del Colaborador (HV)

**Objetivo del modulo:** Consultar y actualizar datos de perfil usando API, incluyendo cambios de seguridad.

**Vistas involucradas:** `Perfil`, `EditarPerfil`, `Seguridad`

**Lista de requerimientos:**

- [ ] Validar sesion simulada antes de consultar perfil.
- [ ] Mostrar datos del usuario en vista de perfil.
- [ ] Precargar formulario de edicion con datos actuales.
- [ ] Actualizar perfil consumiendo endpoint correspondiente (PUT/PATCH).
- [ ] En seguridad, validar contrasena actual y confirmacion de nueva contrasena.
- [ ] Actualizar contrasena consumiendo endpoint de seguridad.
- [ ] Mostrar feedback de exito/error (preferiblemente con `sweetalert2`).

### Modulo 6: Comunicaciones Internas

**Objetivo del modulo:** Gestionar anuncios desde frontend consumiendo API para listar y crear contenido.

**Vistas involucradas:** `Anuncios`, `CrearAnuncio`

**Lista de requerimientos:**

- [ ] Listar anuncios desde endpoint de anuncios.
- [ ] Renderizar listado dinamico en React.
- [ ] Capturar y validar formulario de creacion de anuncio.
- [ ] Crear anuncio via API (POST) con campos minimos: `titulo`, `contenido`, `fecha`.
- [ ] Mostrar confirmacion al usuario y limpiar formulario.
- [ ] Al volver al listado, el nuevo anuncio debe verse reflejado.

### Modulo 7: Dashboard Analitico

**Objetivo del modulo:** Implementar dashboard por secciones/tabs y mostrar metricas calculadas desde datos de API.

**Vista involucrada:** `Dashboard`

**Lista de requerimientos:**

- [ ] Estructurar dashboard con navegacion por tabs o secciones.
- [ ] Definir estado inicial con primera seccion activa.
- [ ] Implementar logica para mostrar/ocultar contenido por seccion.
- [ ] Gestionar clases de estado activo en tabs/botones.
- [ ] Consultar datos necesarios desde API para metricas.
- [ ] Calcular y pintar metricas (por ejemplo: total usuarios, total cursos, total inscripciones).

---

## Criterios de Evaluacion Sugeridos

- Cumplimiento funcional del modulo asignado.
- Calidad del codigo React (componentizacion, reutilizacion y organizacion).
- Correcta integracion con API Spring Boot.
- Manejo de estados de carga/error/empty.
- Validaciones de formularios y feedback al usuario (`sweetalert2` u otro mecanismo claro).
- Navegacion y experiencia de usuario sin recargas innecesarias.
- Buenas practicas de Git y documentacion en `README.md`.

## Integrantes

- [ ] Nombre Apellido
- [ ] Nombre Apellido
- [ ] Nombre Apellido