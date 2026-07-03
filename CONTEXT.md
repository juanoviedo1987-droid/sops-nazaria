# Contexto Tecnológico: Sistema de SOPs Nazaria (v2)

## 1. Arquitectura General
- **Infraestructura:** Despliegue estático nativo en GitHub Pages (Sin intermediarios de compilación como Netlify).
- **Estructura del Proyecto:**
  - `/index.html`: Visor operativo para sucursales. Renderiza dinámicamente los botones leyendo el archivo `menu.json`. Integra lógica anti-caché mediante marcas de tiempo (`?t=`).
  - `/admin.html`: Consola de control para gestión de procesos. Posee un editor interactivo visual (`contenteditable` tipo Word) aislado bajo las reglas del CSS de la marca.
  - `/menu.json`: Manifiesto dinámico central que lista los IDs y Títulos de los SOPs activos.
  - `/sops/`: Carpeta de almacenamiento físico para los archivos HTML individuales de cada procedimiento (`p01.html`, `p02.html`, etc.).

## 2. Estándar de Diseño Estricto (P-00)
Todos los archivos alojados en `/sops/` deben estructurarse con etiquetas HTML limpias (sin wrappers externos ni markdown) respetando la jerarquía de fuentes de la familia **Inter**:
- Título Principal (20pt, #000000, Negrita): `<h1 class="sop-title-1">P-XX · Nombre</h1>`
- Títulos de Fase (14pt, #000000, Negrita, MAYÚSCULAS): `<h2 class="sop-title-2">FASE X: NOMBRE</h2>`
- Sub-bloques (12pt, #434343, Negrita): `<h3 class="sop-title-3">X. Nombre</h3>`
- Cuerpo / Viñetas (11pt, #262626, Regular): `<p class="sop-text">` o `<li class="sop-list-item">`
- Ejemplos / Alertas: `<blockquote>` con itálica y sangría de 12pt.
- Separadores: `<hr class="sop-divider">` debajo del Objetivo y al terminar cada Fase.

## 3. Biblioteca Operativa de Emojis Automáticos
- 🖥️ Dux Software | 📱 WhatsApp / Google Forms | 💳 Payway / Nave / Mercado Pago | 💵 Efectivo / Caja | 📦 Depósito / Stock / Auditorías | ✨ Atención / Fidelización de clientes.
- Cierre obligatorio de todo SOP: `<h3 class="sop-title-3">⚠ REGLAS DE ORO (Puntos Críticos de Control)</h3>` seguido de una lista donde cada ítem inicia estrictamente con ⚠ para faltas graves de caja, stock o datos.

## 4. Flujo de Integración de API en Admin
El `admin.html` conecta directamente con la API de GitHub (`PUT`) y Gemini (`models/gemini-2.5-flash`). Si el modo es `scratch`, la IA formatea texto crudo aplicando los emojis analíticamente; si es `modify`, edita el HTML existente. Si el SOP es catalogado como nuevo, el script inyecta la línea correspondiente en `menu.json` y genera el archivo físico en `/sops/`.
