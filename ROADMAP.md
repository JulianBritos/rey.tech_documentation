# Roadmap para el Desarrollo del Backend

## 1. Autenticación y Gestión de Usuarios

- **Registro e inicio de sesión**: Implementar autenticación con Django Rest Framework y JWT.

  - [Django Rest Framework Authentication](https://www.django-rest-framework.org/api-guide/authentication/)
  - [Simple JWT para autenticación](https://django-rest-framework-simplejwt.readthedocs.io/en/latest/)

- **Perfiles de usuario**: Gestionar roles y permisos con Django.

  - [Django Permissions y Authentication](https://docs.djangoproject.com/en/stable/topics/auth/default/)

- **Recuperación y cambio de contraseña**: Usar el sistema integrado de restablecimiento de contraseña de Django.

- **Gestión de direcciones de envío**: Crear un modelo de direcciones relacionado con el usuario.

- **Seguridad**: Configurar Django con HTTPS y protección contra ataques comunes.
  - [OWASP Security Django](https://docs.djangoproject.com/en/stable/topics/security/)

## 2. Gestión de Productos y Categorías

- **Categorías y subcategorías**: Modelos con relaciones jerárquicas.
- **Productos con variantes**: Implementar un sistema de atributos con Django ORM.
- **Stock e inventario**: Control mediante señales de Django.
- **Imágenes y descripciones**: Usar Django Storage y Pillow para manejo de imágenes.
- **Precios y descuentos**: Implementar lógica de descuentos en modelos y serializers.

## 3. Carrito de Compras y Checkout

- **Persistencia del carrito**: Asociarlo a `session_id` para usuarios no registrados.
- **Cálculo de costos**: Usar serializers para calcular totales con impuestos.
- **Métodos de envío**: Configurar opción en la API.

## 4. Gestión de Pedidos

- **Creación y seguimiento**: Implementar estados del pedido con Django ORM.
- **Estados del pedido**: Utilizar `choices` en los modelos.
- **Historial de pedidos**: Endpoint para listar pedidos del usuario.

## 5. Pagos e Integración con Pasarelas

- **Órdenes de pago**: Modelo para almacenar pagos pendientes y confirmados.
- **Integraciones**:
  - [Stripe con Django](https://stripe.com/docs/payments/checkout/accept-a-payment#django)
  - [PayPal en Django](https://developer.paypal.com/docs/checkout/integrate/)
  - [MercadoPago en Django](https://www.mercadopago.com.ar/developers/es/docs/)
- **Webhooks**: Endpoint para recibir confirmaciones de pago.

## 6. Gestión de Envíos

- **Métodos de envío configurables**: Modelos de envío.
- **Integración con servicios de envío**.
- **Tracking de envíos**.

## 7. Administración y Panel de Control

- **Django Admin**: Configurar panel de administración.
- **Dashboard con Django Rest Framework**: Crear endpoints con estadísticas.
- **Gestión de usuarios, productos y pedidos**.
- **Configuración de impuestos y divisas**.

## 8. Notificaciones y Comunicación

- **Confirmaciones por email**: Configurar `django.core.mail`.
- **Notificaciones en tiempo real**: Implementar WebSockets con Django Channels.

## 9. Opiniones y Reseñas de Productos

- **Publicación de opiniones**: Modelo y API para comentarios.
- **Moderación**: Configurar permisos para aprobación de comentarios.

## 10. Gestión de Cupones y Descuentos

- **Códigos de descuento**: Implementar generación y validación de cupones.
- **Descuentos automáticos**: Lógica en el modelo de carrito.

## 11. Configuración y Personalización del Sitio

- **Gestión de contenido estático**: Usar Django CMS o `flatpages`.
- **Temas y branding**.

## 12. Seguridad y Auditoría

- **Protección contra ataques**: Configurar `django.middleware.security.SecurityMiddleware`.
- **Logs de actividad**.
- **Control de acceso**: Definir permisos con Django Rest Framework.

---

# Roadmap para el Desarrollo del Frontend

## 1. Configuración del Proyecto

- **Inicialización con Vite o Create React App**
- **Configuración de rutas con React Router**
- **Gestor de estado: Context API o Redux Toolkit**
- **Estilización con Tailwind CSS o CSS Modules**

## 2. Vistas y Funcionalidades

### 2.1. **Inicio (`Home.jsx`)**

- Mostrar productos destacados y ofertas.
- Conexión con: `GET /api/products/list/`

### 2.2. **Página de Producto (`ProductDetail.jsx`)**

- Mostrar detalles de un producto seleccionado.
- Permitir seleccionar variantes (talla, color, etc.).
- Botón para agregar al carrito.
- Conexión con: `GET /api/products/detail/:id/`

### 2.3. **Carrito de Compras (`Cart.jsx`)**

- Mostrar productos agregados con opción de modificar cantidad o eliminar.
- Mostrar cálculo de costos, impuestos y descuentos.
- Botón para proceder al pago.
- Conexión con: `GET /api/orders/cart/`, `POST /api/orders/cart/add/`, `DELETE /api/orders/cart/remove/`

### 2.4. **Checkout (`Checkout.jsx`)**

- Formulario para datos de envío y método de pago.
- Resumen del pedido antes de confirmar.
- Conexión con: `POST /api/orders/create/`

### 2.5. **Registro y Login (`Auth.jsx`)**

- Formulario de registro y login con validación.
- Autenticación con JWT.
- Conexión con: `POST /api/users/auth/register/`, `POST /api/users/auth/login/`

### 2.6. **Perfil de Usuario (`Profile.jsx`)**

- Editar información personal y direcciones de envío.
- Ver historial de pedidos.
- Conexión con: `GET /api/users/profile/`, `PUT /api/users/profile/update/`, `GET /api/orders/user/`

### 2.7. **Administración (`AdminPanel.jsx`)**

- CRUD de productos y categorías.
- Gestión de pedidos y usuarios.
- Conexión con: `GET/POST/PUT/DELETE /api/products/`, `GET/POST/PUT/DELETE /api/products/categories/`, `GET/PUT /api/orders/`

### 2.8. **Búsqueda y Filtrado (`SearchResults.jsx`)**

- Buscar productos por nombre o categoría.
- Filtros por precio, calificación y disponibilidad.
- Conexión con: `GET /api/products/search/`

### 2.9. **Opiniones y Reseñas (`Reviews.jsx`)**

- Permitir a los usuarios dejar comentarios y calificaciones.
- Mostrar reseñas de otros clientes.
- Conexión con: `GET /api/products/reviews/:product_id/`, `POST /api/products/reviews/add/`

### 2.10. **Gestión de Envíos (`Tracking.jsx`)**

- Seguimiento del estado del pedido.
- Conexión con: `GET /api/orders/tracking/:order_id/`

### 2.11. **Gestión de Cupones (`Coupons.jsx`)**

- Aplicar códigos de descuento en el carrito.
- Conexión con: `POST /api/orders/coupons/apply/`

### 2.12. **Notificaciones y Mensajes (`Notifications.jsx`)**

- Mostrar actualizaciones de pedidos y alertas importantes.
- Conexión con WebSockets o API REST (`GET /api/users/notifications/`)

## 3. Seguridad y Autenticación

- Protección de rutas privadas con `useEffect` y `useContext`.
- Manejo seguro de tokens JWT en `localStorage` o `httpOnly cookies`.

---
