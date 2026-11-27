# KamiKōbō POS · prototipo HTML/CSS (solo escritorio, mín. 1024 px)

## Estado: TERMINADO (maquetación)
- index.html, css/global.css, css/componentes.css
- pages: login, dashboard, inventario, ventas, devoluciones, compras, usuarios, perfil, historial, reportes, cierre-caja (+ su CSS en css/paginas/)
- Los 13 .js vacíos con comentario de cabecera.

## Cómo probar
- Rol: cambiar `<body data-rol="admin">` por `"operador"` en cualquier página.
- Modales, menús y vistas se abren con `:target` (enlaces `href="#id"`, cierre con `href="#cerrar"` (id que no existe: cierra sin saltar al inicio de la página)). Sin JavaScript.
- Operador en usuarios.html: se oculta el contenido admin y aparece "Acceso restringido".
- Imágenes: rutas a `assets/img/*.jpg` (carpeta vacía; se ven los `alt` sobre fondo rosa hasta añadirlas).

## Archivos .js enlazados (todos con `defer`, al final del body)
| HTML | .js |
|---|---|
| login, dashboard, perfil, historial, reportes, cierre-caja | main.js |
| inventario | main, inventario/inventario, inventario/inventarioSQL |
| ventas | main, ventas/ventas, ventas/ventasSQL |
| compras | main, compras/compras, compras/comprasSQL |
| devoluciones | main, devoluciones/devoluciones, devoluciones/devolucionesSQL |
| usuarios | main, usuarios/usuarios, usuarios/usuariosSQL |
(database/conexion.js y tablas.js no se enlazan.)

## Convenciones
- Variables en :root (global.css): --color-principal, --color-rosa-claro, --color-texto, --color-texto-suave, --color-alerta-fondo, --color-alerta-borde, --color-exito, --color-peligro, --color-borde (+ -principal-oscuro, -alerta-texto, fuentes).
- Roles: `[data-rol="admin"]` se oculta con body operador; `[data-rol="operador"]` se oculta con body admin (dos reglas con !important en componentes.css).
- Estados (global.css): .oculto, .activo, .deshabilitado, .error. Como los componentes se cargan después, hay reglas combinadas en componentes.css (`.boton.deshabilitado`, `.entrada.error`, `.pestana.activo`, `.chip.activo`, `.pagina-enlace.activo`, `.opcion.activo`, `.boton.oculto`).
- Clases en español por función, solo selectores de clase (máx. 2 niveles), sin media queries de ancho. Solo hay @media print.
- Convención de HTML: `data-id`, `data-folio`, `data-panel` y comentarios `<!-- BACKEND: ... -->` marcan dónde conecta el JS.

## Vocabulario de clases (definido en componentes.css salvo indicación)
| Grupo | Clases |
|---|---|
| Layout | .contenedor, .contenido, .fila, .columna, .rejilla-tarjetas (dashboard.css), .rejilla-kpis, .rejilla-productos, .rejilla-chips, .rejilla-formulario (-tres, -cuatro), .rejilla-con-panel, .panel-lateral, .barra-filtros, .pagina-dividida (login.css), .rejilla-perfil (perfil.css) |
| Estructura | .encabezado(-simple), .logo(-rojo), .buscador, .menu-usuario, .boton-menu, .menu-lateral, .fondo-oscuro, .pie-pagina, .ruta-navegacion, .titulo-pagina, .subtitulo-pagina, .encabezado-pagina, .seccion-titulo, .panel-titulo |
| Tarjetas/datos | .tarjeta(-rosa, -titulo), .caja-rosa, .indicador(-numero, -texto, -columna, -destacado), .insignia(-disponible, -agotado, -activa, -inactiva), .chip(-categoria), .tarjeta-producto, .producto-cabecera/-imagen/-cuerpo/-meta/-nombre/-precio/-pie/-existencias, .linea-dato, .avatar |
| Botones | .boton, .boton-secundario, .boton-peligro, .boton-enlace, .boton-ancho, .boton-pequeno, .grupo-botones, .grupo-botones-venta, .grupo-acciones |
| Formularios | .formulario, .campo, .campo-ancho, .etiqueta, .entrada, .area-texto, .selector, .texto-ayuda, .texto-error, .caja-archivo, .grupo-opciones, .opcion |
| Tablas | .tabla-contenedor, .tabla, .fila-alterna, .fila-seleccionada, .fila-total, .tabla-pie, .enlace-fila, .texto-derecha, .texto-izquierda |
| Modales/vistas | .modal, .modal-contenido, .modal-ancho, .modal-cabecera, .modal-titulo, .modal-cerrar, .modal-acciones, .modal-detalle/-imagen/-datos, .vista (pantalla completa con :target) |
| Avisos | .alerta, .alerta-error, .alerta-exito, .alerta-informacion, .alerta-titulo |
| Pestañas/paginación | .pestanas, .pestana, .panel-pestana, .paginacion, .pagina-enlace |
| Tickets/impresión | .ticket(-marca, -titulo, -centrado, -separador, -linea, -total), .fila-ticket, .acciones-ticket, .firma, .linea-firma, .solo-impresion, .no-imprimir, .cabecera-impresion, .titulo-impresion, .linea-roja, .nota-formato |
| Texto | .texto-peligro, .texto-exito, .texto-principal |

## Decisiones tomadas
- "Venta confirmada", tickets, comprobante de devolución, "Compra confirmada" y los formularios/confirmaciones de usuarios son `.vista` (cubren la página bajo el encabezado y se abren con :target); no repiten el pie de página.
- Fechas AAAA-MM-DD HH:MM; venta V-000128 con fecha 2026-11-23 14:35 (el PDF mostraba 20/06/2026 en un lugar y 23/11/2026 en otro).
- Historial usa rojo/rosa en lugar del verde del mockup.
- Reportes: el panel "Devoluciones" no está en el PDF; sus datos están inferidos del panel "Mov. por usuario". Los 6 paneles llevan cabecera/firma/"Página 1 de 1" solo para impresión.
- Inventario: solo existen los 5 modales pedidos; un enlace "Consultar producto inactivo" permite abrir el último sin JS.
- Cierre de caja: estado "pendiente" visible y estado "conciliado" oculto; botón "Confirmar cierre de caja" oculto.
- Header sin buscador (todas excepto inicio, perfil, inventario, usuarios) usa `.encabezado-simple`.

## Etapa 2 (ventanas emergentes y correcciones)
- Inventario: modales `modal-agregar-listo`, `-incompleto`, `-duplicado`, `modal-consultar-nuevo`, `modal-editar-nuevo`, `modal-cambios-guardados` + tarjeta FIG-009 oculta (estado 9 productos, la activa el JS).
- Ventas: `modal-codigo`, `modal-cantidad`, `error-codigo/-inactivo/-existencias/-cantidad/-carrito-vacio`, panel "Probar validaciones" y "Simular lectura".
- Todos los modales caben en 1024×768 sin deslizar (ancho 520 px). Las 11 `.vista` llevan pie compacto.
- Dashboard: número 01-04, ícono (assets/icons/*.svg) y hueco de imagen difuminada. Encabezado: logo junto a la hamburguesa.
- devoluciones.css: selector de 3 niveles sustituido por `.motivo-devolucion`.
- Siguen necesitando deslizar (son páginas completas): `compra-confirmada`, `devolucion-confirmada`.

## Se dejó fuera a propósito
Diseño móvil/responsivo, JavaScript y SQL, "Ejemplo Operador" del login y los estados de error de Devoluciones/Compras/Usuarios.

## Verificación hecha
Cada clase usada en los HTML existe en algún CSS; cada `<script src>` y `<link>` apunta a un archivo existente; capturas revisadas a 1280 px.
