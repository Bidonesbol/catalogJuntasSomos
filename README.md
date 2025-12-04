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

