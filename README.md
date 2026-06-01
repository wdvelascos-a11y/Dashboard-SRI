# Reporte Comprobantes SRI — Mensual

Dashboard web que procesa **comprobantes electrónicos XML del SRI Ecuador** (facturas, notas de crédito, notas de débito, retenciones recibidas/emitidas, liquidaciones de compra) y genera un reporte mensual con KPIs, gráficos dinámicos y exportación CSV.

**100 % en el navegador del cliente.** Los XMLs nunca salen del computador — no hay servidor, no hay base de datos, no hay analytics.

---

## Características

- 📂 **Drag-and-drop** de archivos o selección de carpeta completa
- 🔍 Filtros por **RUC**, **año** y **mes**
- 📊 **8 KPIs** del periodo (compras, ventas, IVA neto, retenciones, NC/ND)
- 📈 **4 gráficos** interactivos (tipos de documento, bases IVA, tendencia diaria, top proveedores)
- 📋 **7 tablas** ordenables y buscables por categoría
- 💾 **Exportación CSV** por categoría (compatible Excel, encoding UTF-8 BOM)
- 🔒 **Privacidad total**: nada se sube a internet

---

## Deploy en GitHub Pages

### Opción A — Repo nuevo

```bash
# 1. Crea un repo en GitHub (ej. dashboard-sri)
# 2. Clónalo localmente:
git clone https://github.com/TU_USUARIO/dashboard-sri.git
cd dashboard-sri

# 3. Copia index.html (y este README.md) en la raíz
# 4. Commit y push:
git add .
git commit -m "Initial commit"
git push
```

Luego en GitHub:
1. **Settings** → **Pages**
2. **Source**: `Deploy from a branch`
3. **Branch**: `main` / `(root)` → **Save**
4. Espera ~1 minuto. Tu dashboard estará en:
   `https://TU_USUARIO.github.io/dashboard-sri/`

### Opción B — Subir directo desde el navegador

1. En GitHub, crea un repo nuevo `dashboard-sri`
2. Haz click en **uploading an existing file**
3. Arrastra `index.html` y `README.md`
4. **Commit changes**
5. Activa GitHub Pages como en la Opción A paso 4

---

## Cómo usar (para clientes)

1. Abre el enlace que te compartieron (`https://...github.io/dashboard-sri/`)
2. **Arrastra los XMLs** del SRI a la zona de carga (o selecciona una carpeta)
3. Opcionalmente ingresa tu **RUC** para filtrar solo tus comprobantes
4. Selecciona **año y mes** del periodo a declarar
5. Click **Procesar**
6. Revisa KPIs, gráficos y tablas
7. Descarga el CSV de cada categoría desde su pestaña

---

## Estructura de XMLs soportados

El dashboard procesa cualquier XML autorizado del SRI Ecuador:

| Tipo | codDoc | Hoja en reporte |
|------|--------|-----------------|
| Factura | 01 | Facturas Compras / Ventas |
| Nota de Crédito | 04 | N. Crédito |
| Nota de Débito | 05 | N. Débito |
| Comprobante de Retención | 07 | Retenciones Recibidas / Emitidas |
| Liquidación de Compra | 03 | Liq. Compras |

Soporta:
- IVA 0 %, 5 %, 8 %, 12 %, 13 %, 14 %, 15 %, Exento, No Objeto
- Sujeto retenido y agente de retención (detección automática por RUC del cliente)
- Múltiples formas de pago por documento
- Detalles con CDATA del nodo `<comprobante>`

---

## Personalización

El logo y nombre del despacho contable se pueden cambiar editando el bloque `<div class="brand">` en `index.html`:

```html
<div class="brand">
  <div class="logo">DV</div>
  <h1>Despacho Contable David Velasco</h1>
  <span class="tag">Reporte SRI Mensual</span>
</div>
```

Los colores se controlan con CSS variables al inicio de `<style>`:

```css
:root {
  --navy: #002060;   /* primario */
  --gold: #c9a227;   /* acento */
}
```

---

## Privacidad y seguridad

- **0 datos enviados a servidores externos.** Todo el parseo XML, cálculos y gráficos ocurren en el navegador del usuario.
- Las únicas peticiones externas son **Chart.js**, **Grid.js** y su CSS desde jsDelivr (CDN público) — solo carga de librerías, no envío de datos.
- La configuración (RUC, último periodo seleccionado) se guarda en `localStorage` del navegador del usuario.
- No hay cookies, no hay tracking, no hay analytics.

Si quieres bloquear por completo cualquier petición externa, descarga `chart.umd.js`, `gridjs.umd.js` y el CSS de Grid.js, e inclúyelos junto a `index.html` cambiando los `<script src="...">` por rutas relativas.

---

## Licencia

Uso libre para fines profesionales contables en Ecuador.

---

**Autor**: David Velasco · Contador / Analista financiero
