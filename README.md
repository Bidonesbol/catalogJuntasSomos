# 🛍️ JuntasSomos — Catálogo Web

Este proyecto es un **catálogo web simple, rápido y sin backend**, ideal para compartirse en redes sociales (Facebook, Instagram, WhatsApp).  
Funciona 100% con HTML, CSS y JavaScript y puede desplegarse fácilmente con GitHub Pages.

Permite:
- Ver productos y variantes
- Marcar productos o variantes como agotados
- Añadir ítems al carrito
- Seleccionar departamento y notas
- Enviar pedidos directamente por **WhatsApp**
- Medir interacción mediante **Google Analytics 4 (GA4)**

---

## 📁 Estructura del proyecto

```
catalogJuntasSomos/
│
├── index.html          # Página principal con lógica, estilos y catálogo
├── README.md           # Este archivo
└── images/             # Carpeta con imágenes del catálogo y logotipo
```

Todo el funcionamiento del catálogo está embebido en `index.html` para facilitar despliegue y edición.

---

# 🧩 Definición de productos

Los productos están definidos en un arreglo dentro de `index.html`:

```js
const products = [
  {
    id: "taza11",
    name: "Taza 11 oz",
    description: "...",
    baseImage: "images/taza11-main.jpg",
    soldOut: false,
    variants: [
      {
        id: "taza11-std",
        name: "Taza 11 oz",
        price: 60,
        image: "images/taza11-std.jpg",
        soldOut: false
      }
    ]
  }
];
```

### Control de inventario (flags `soldOut`)
- **Producto agotado:** `soldOut: true` a nivel de producto  
- **Variante agotada:** `soldOut: true` dentro de `variants[]`  
- Si **todas** las variantes están agotadas, el producto entero se muestra como agotado.

---

# 🛒 Carrito y envío por WhatsApp

El usuario puede:
- Añadir/quitar productos
- Ver el total calculado automáticamente
- Añadir notas
- Seleccionar departamento
- Enviar el pedido a un número configurable de WhatsApp:

```js
const WHATSAPP_NUMBER = "591XXXXXXXXX";
```

---

# 🌐 Publicación

### GitHub Pages (recomendado)
- Gratis  
- Sin anuncios  
- Actualización automática al hacer push  

---

# 📘 Guías de edición

## ➕ Añadir un nuevo producto

1. Abre `index.html`
2. Busca `const products = [ ... ]`
3. Copia un bloque existente y ajusta:
   - `id`
   - `name`
   - `description`
   - `baseImage`
   - `variants[]`

Ejemplo mínimo:

```js
{
  id: "nuevo-producto",
  name: "Mi Producto Nuevo",
  description: "...",
  baseImage: "images/mi-producto.jpg",
  soldOut: false,
  variants: [
    {
      id: "nuevo-std",
      name: "Variante Estándar",
      price: 100,
      image: "images/mi-producto-std.jpg",
      soldOut: false
    }
  ]
}
```

---

## ➕ Añadir una variante a un producto existente

Insertar un nuevo objeto dentro de `variants[]`:

```js
{
  id: "pins-var4",
  name: "Nuevo diseño",
  price: 15,
  image: "images/pins-var4.jpg",
  soldOut: false
}
```

---

## 🖼️ Reemplazar imágenes

1. Colocar la imagen en `/images/`
2. Actualizar la referencia en:
   - `baseImage`
   - `image` de la variante
3. Recargar la página

---

# 📊 Google Analytics 4 (GA4)

El catálogo implementa analíticas completas mediante GA4.  
Se usa el script oficial `gtag.js` y una función auxiliar:

```js
function trackEvent(name, params = {}) {
  if (typeof gtag === "function") {
    gtag("event", name, params);
  }
}
```

### 📌 Eventos principales integrados
- `view_product_detail`
- `quick_add_product`
- `add_to_cart`
- `open_cart`
- `remove_from_cart`
- `clear_cart`
- `open_image_zoom`
- `scroll_to_section`
- `click_social_link` — clics en Facebook o Instagram del pie de página
- `send_order_whatsapp` — **evento de conversión principal**

Todos los eventos incluyen parámetros relevantes (product_id, variant_id, quantity, department, etc).

### 🧪 Vista en tiempo real
En GA4:  
**Reports → Realtime → Event count by Event name**

---

# ✔️ Estado actual
- Catálogo funcional  
- Carrito y WhatsApp operativos  
- Control de inventario funcionando  
- Interfaz responsiva  
- GA4 integrado  
- Listo para publicación

---

# 🔗 Enlaces sociales
El pie de página incluye enlaces a las redes de La Chiflería:
- Facebook  
- Instagram

Estos clics también están instrumentados con GA4.

---

# 📐 Registro de pedidos en Google Sheets

El catálogo ahora registra cada pedido enviado por WhatsApp en una hoja de cálculo de Google Sheets.  
Esto permite a la organización llevar control manual de ventas, pagos y entregas.

## 🧾 ¿Qué datos se registran?

Cada pedido genera automáticamente un **Order ID** único y guarda:

- `order_id`
- `created_at`
- `name` (si el usuario lo ingresó)
- `department`
- `estimated_total`
- `items_count`
- `cart_json` (lista completa de productos y variantes)

La hoja también incluye columnas para uso interno:

- `status` → Pendiente / Pagado / Entregado / Cancelado  
- `notes` → Observaciones internas  

## 🔧 ¿Cómo funciona?

1. Cuando el usuario presiona **Enviar pedido por WhatsApp**, el sistema:
   - Genera un `order_id`
   - Construye un objeto con toda la información del carrito
   - Envía esta información al endpoint de Google Apps Script mediante `fetch()`
   - Sigue abriendo WhatsApp normalmente (aunque el registro falle)

2. El Apps Script recibe el JSON y agrega una nueva fila en la hoja `Orders`.

## 🌐 Endpoint configurado

El endpoint activo es:

```
https://script.google.com/macros/s/AKfycbwgX1knveA1LtFKzIM6nOOw6qI4P8lrdXzD6a_1_lpDQq_R7_COMLguGDRFH9P4B5aVeA/exec
```

## 📎 Ventajas del sistema

- No requiere backend propio  
- Funciona con GitHub Pages  
- Permite administración manual de pedidos  
- Cada pedido queda vinculado por ID al mensaje enviado por WhatsApp  

---
