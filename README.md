# 🛍️ JuntasSomos — Catálogo Web

Este proyecto es un **catálogo web simple y ligero**, optimizado para compartirse en redes sociales (Facebook, Instagram, WhatsApp). No requiere servidor ni backend — funciona 100% con HTML, CSS y JavaScript.

Permite:
- Ver productos con imágenes
- Seleccionar variantes
- Añadir productos al carrito
- Enviar pedidos directamente por **WhatsApp**
- Marcar productos o variantes como **agotados** mediante flags simples (`soldOut: true/false`)

---

## 📁 Estructura del proyecto

```
catalogJuntasSomos/
│
├── index.html          # Página principal con todo el código
├── README.md           # Este archivo
└── images/             # Carpeta con las imágenes del catálogo
```

Todos los estilos, scripts y lógica del carrito están embebidos en `index.html` para facilitar despliegue.

---

## 🧩 Cómo funcionan los productos

Todos los productos están definidos dentro de un arreglo:

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

---

# 🟥 Control de Inventario con Flags `soldOut`
El catálogo soporta dos niveles de control:

---

## 1️⃣ **Producto agotado (nivel global)**

Si deseas que **todo el producto** aparezca agotado:

```js
soldOut: true
```

### Efectos:
- En el catálogo: aparece un botón gris **“Agotado”**
- No muestra “Ver” ni “Agregar rápido”
- No permite abrir el modal del producto
- No permite añadir variantes al carrito

---

## 2️⃣ **Variante agotada (nivel específico)**

Cada variante también puede marcarse como agotada:

```js
soldOut: true
```

### Efectos:
- En el modal: la variante aparece como  
  **`Variante · Bs X (AGOTADO)`**
- La opción se deshabilita automáticamente
- “Agregar al carrito” verifica que no esté agotada
- “Agregar rápido” evita variantes agotadas

### Comportamiento automático:
Si **todas las variantes** están agotadas, el sistema considera el producto **completo** como agotado.

---

# 🎨 Estado visual de “Agotado”

Los productos agotados muestran un botón:

```css
.btn-soldout {
  background: rgb(130,131,131);
  border-color: rgb(130,131,131);
  cursor: not-allowed;
  box-shadow: none;
}
```

Con la etiqueta:

```
Agotado
```

El color del texto se mantiene igual que los otros botones.

---

# 📦 Carrito y WhatsApp

El usuario puede:
- Añadir productos y variantes
- Ver el total
- Quitar ítems
- Añadir notas
- Seleccionar departamento
- Enviar el pedido vía WhatsApp

WhatsApp usa:

```js
const WHATSAPP_NUMBER = "591XXXXXXXXX";
```

Solo actualiza ese número y todo funciona automáticamente.

---

# 🚀 Cómo actualizar inventario o productos

### Para marcar un producto agotado:
```js
soldOut: true
```

### Para marcar una variante agotada:
```js
soldOut: true
```

### Para añadir o cambiar imágenes:
Reemplaza archivos en:  
```
/images/
```

### Para modificar precios o nombres:
Edita el `products[]` directamente en `index.html`.

---

# 🌐 Publicación / Hosting

Puedes hostear el catálogo gratuitamente en:

### **GitHub Pages (recomendado)**
- Gratis, rápido y sin anuncios.
- Publicación automática desde la rama `main`.

Si deseas, puedo configurarlo por ti.

---

# 🛠️ Futuras mejoras posibles
- Filtros por categoría
- Buscador de productos
- Código QR para compartir
- Panel de administración con Google Sheets
- Banner de ofertas temporales
- Animación de carrito

---

## ✔️ Estado actual del proyecto
- Catálogo funcional  
- Carrito funcional  
- WhatsApp integrado  
- Control de inventario con flags funcionando  
- Interfaz completamente responsiva  
- Lista para publicar

---  

## 📘 Guías adicionales

### 🆕 Cómo agregar un producto nuevo (paso a paso)

1. Abre `index.html`.
2. Localiza el arreglo `const products = [ ... ]`.
3. Copia cualquier bloque de producto existente y pégalo debajo.
4. Cambia:
   - `id`: debe ser único  
   - `name`: nombre del producto  
   - `description`: texto descriptivo  
   - `baseImage`: imagen principal dentro de `/images/`  
   - `soldOut`: normalmente `false`  
5. Edita la lista `variants` según necesites.
6. Guarda el archivo y recarga la página.

**Ejemplo mínimo:**
```js
{
  id: "nuevo-producto",
  name: "Mi Producto Nuevo",
  description: "Descripción corta...",
  baseImage: "images/mi-producto.jpg",
  soldOut: false,
  variants: [
    {
      id: "nuevo-std",
      name: "Mi Producto Nuevo (Var. Estándar)",
      price: 100,
      image: "images/mi-producto-std.jpg",
      soldOut: false
    }
  ]
}
```

---

### 🧩 Cómo agregar una nueva variante a un producto

1. Dentro del arreglo `products`, ubica el producto al que quieres agregar otra variante.
2. Ve a su lista `variants: [ ... ]`.
3. Añade un nuevo objeto de variante.

**Ejemplo:**
```js
variants: [
  {
    id: "pins-var1",
    name: "Pin Diseño A",
    price: 15,
    image: "images/pins-var1.jpg",
    soldOut: false
  },
  {
    id: "pins-var4",
    name: "Pin Diseño D",
    price: 15,
    image: "images/pins-var4.jpg",
    soldOut: false
  }
]
```

**Reglas importantes:**
- Cada variante debe tener un `id` único.
- Si marcas `soldOut: true`, aparecerá como agotada automáticamente.
- La imagen debe existir en `/images/`.

---

### 🖼️ Cómo actualizar o reemplazar imágenes

1. Asegúrate de que la imagen nueva tenga el nombre correcto.
2. Colócala dentro de la carpeta:

```
/images/
```

3. Si cambiaste el nombre del archivo, también debes actualizarlo en `index.html`:
   - `baseImage` del producto
   - `image` de cada variante

**Ejemplo antes:**
```js
image: "images/pins-var1.jpg"
```

**Ejemplo después (si renombraste la imagen):**
```js
image: "images/pins-var1-new.jpg"
```

4. Guarda y recarga la página para ver el cambio.

---

