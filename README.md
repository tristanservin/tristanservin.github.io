# App QR de Inventario

Aplicación web estática para **generar**, **escanear** y **gestionar** registros de productos por QR usando `localStorage`.

## Mejoras implementadas (priorizadas)

1. **Estabilidad de escaneo**
   - Se añadió un control anti-duplicado por ID + ventana de enfriamiento (`cooldown`) para evitar lecturas repetidas del mismo QR en segundos consecutivos.
   - Se protege el flujo de procesamiento con un estado interno para que dos callbacks cercanos no dupliquen la carga de datos.

2. **Robustez de datos en `localStorage`**
   - Lectura segura con parseo validado del schema de registro.
   - Si hay datos corruptos/invalidos, se omiten y limpian automáticamente al renderizar lista.
   - Visualización de aviso con contador de registros inválidos depurados.

3. **Seguridad del DOM y eventos**
   - Se eliminaron manejadores `onclick` inline.
   - Toda la interacción de botones usa `addEventListener`.
   - La lista se construye con nodos del DOM y contenido escapado para reducir superficie de inyección.

4. **Accesibilidad básica**
   - Mensajes dinámicos principales (`scanMsg`, `listaMsg`) con `aria-live="polite"`.

## Estado de roadmap funcional

### Sincronización
- **Prioridad alta (siguiente fase):** pasar de almacenamiento local a backend compartido (Firebase, Supabase, Google Sheets API o endpoint propio) para multi-dispositivo en tiempo real.

### Export / Import
- **Prioridad alta:** exportar JSON/CSV local y permitir importación validada para respaldo/migración.

### Edición de registros
- **Prioridad media-alta:** agregar modo edición de producto/origen/función/destino/nota con historial de cambios.

### Filtros y búsqueda
- **Prioridad media:** filtros por estado (pendiente/recibido), fecha, texto libre e ID.

### Accesibilidad
- **Prioridad media:** mejorar navegación con teclado, foco visible, contraste y etiquetas ARIA adicionales.

### Trazabilidad
- **Prioridad alta:** registrar eventos (creación, edición, recepción, borrado), usuario responsable y timestamp para auditoría.

## Desarrollo local

Solo abre `index.html` en navegador moderno con HTTPS si vas a usar cámara (o sirviendo localmente con certificado).  
La app depende de:
- `html5-qrcode`
- `qrcodejs`
