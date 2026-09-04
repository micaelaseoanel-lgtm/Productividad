# Propuestas de mejora — Mi Productividad

Estado: **propuestas sin decidir, ninguna implementada todavía.** Esto es un brainstorm hecho por
Claude (chat) a pedido de Micaela, agrupado por esfuerzo estimado. Antes de implementar cualquiera,
confirmar con ella cuál quiere trabajar primero — no asumir prioridad.

## Rápidas / bajo riesgo

- Separar visualmente en la vista "Hoy": vencidas / de hoy / próximas (hoy se ven todas mezcladas)
- Botón "posponer 1 día" por tarea (evita editar la fecha a mano)
- Buscador de texto simple sobre todas las tareas
- Niveles de prioridad (alta/media/baja) con orden automático
- Exportar/importar el estado como JSON (backup manual). **Importante**: hoy el estado vive solo en
  `localStorage` del navegador/dispositivo — sin esto, borrar caché o cambiar de celular implica
  perder todos los datos.

## Esfuerzo medio

- Tareas recurrentes (diaria/semanal/mensual) — hoy cada tarea es un evento único, sin repetición
- Subtareas / checklist dentro de una tarea
- Vista semanal, intermedia entre "Hoy" y el calendario mensual
- Reordenar tareas manualmente (drag) dentro de un mismo día
- Resumen/estadísticas semanales: completadas vs. pendientes, cumplimiento de objetivos (☀️)

## Grandes / con incertidumbre técnica a validar antes de prometer

- **Notificaciones de vencimiento**: posible con Service Worker + Notification API, pero sin backend
  las notificaciones "programadas" son poco confiables en navegador (depende de que el navegador siga
  corriendo, o de Periodic Background Sync, con soporte desparejo entre navegadores). Validar
  factibilidad real antes de comprometerse con esto.
- **Sincronización entre dispositivos**: hoy es 100% local. Implica sumar backend o algún servicio de
  sync — es un cambio de arquitectura, no un ajuste incremental.
- Modo oscuro (estético, no funcional — menor prioridad real que las anteriores)

## Fuera de alcance (confirmado con Micaela)

- Control de gastos / plata: se evaluará como proyecto aparte más adelante, no mezclar en esta app.
