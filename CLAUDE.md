# CLAUDE.md — girodolares.cl
> Archivo de contexto para Claude Code. Leer completo antes de cualquier acción.
> Última actualización: 21/05/2026

---

## 1. QUÉ ES ESTE PROYECTO

**girodolares.cl** es el hub informacional y de autoridad SEO del ecosistema GiroCupo.
GiroDólares compra cupo en dólares de tarjetas de crédito y paga en pesos chilenos.
El cliente es el **vendedor** de cupo — operación entre privados en Chile.

- **Fundación:** 23 septiembre 2002
- **Clientes:** +21.000 · **Rating:** 4.9★ Google Reviews
- **Operación mínima:** USD 300
- **Tarjetas aceptadas:** Visa, Mastercard, Amex
- **Tiempo operación:** menos de 15 minutos / pago mismo día hábil

---

## 2. STACK TÉCNICO

| Capa | Tecnología |
|------|------------|
| Código | HTML5 puro + CSS + JS vanilla (sin frameworks) |
| Repo | GitHub: `GiroCupo/girodolares-web` (público) |
| Hosting | Cloudflare Pages — proyecto `girodolares-web` |
| Deploy | Automático al hacer push a `main` |
| Fuentes | Self-hosted `.woff2` en `/fonts/` |
| Validación | GitHub Actions — `.github/workflows/ai-proposal-validation.yml` |

**Deploy siempre via git push. Nunca subir ZIPs manualmente.**
**Después de cada merge a main: purgar caché en Cloudflare dashboard.**

---

## 3. ESTRUCTURA DEL REPO

```
girodolares-web/
├── index.html                          ← Home (Tier A — Golden Page)
├── robots.txt
├── sitemap.xml
├── _redirects
├── .htmlvalidate.json
├── apple-touch-icon.png
├── favicon-512.png
├── favicon.ico
│
├── fonts/                              ← Self-hosted, no tocar
│   ├── cormorant-garamond-v21-latin-500.woff2
│   ├── cormorant-garamond-v21-latin-italic.woff2
│   ├── cormorant-garamond-v21-latin-regular.woff2
│   ├── dm-sans-v17-latin-500.woff2
│   └── dm-sans-v17-latin-regular.woff2
│
├── cupo-en-dolares/index.html          ← Pillar page (Tier A)
├── quienes-somos/index.html
├── politica-de-privacidad/index.html
├── terminos-y-condiciones/index.html
│
├── blog/
│   ├── index.html
│   ├── precio-cupo-dolares-chile/index.html
│   ├── conviene-vender-cupo-dolares/index.html
│   ├── tarjetas-con-mas-cupo-dolares/index.html
│   ├── como-vender-cupo-dolares-paso-a-paso/index.html
│   ├── que-es-cupo-en-dolares/index.html
│   ├── como-vender-cupo-dolares-tarjeta/index.html
│   └── vender-cupo-dolares-chile/index.html
│
├── cupo-en-dolares-santiago/index.html
├── cupo-en-dolares-providencia/index.html
├── cupo-en-dolares-las-condes/index.html
├── cupo-en-dolares-concepcion/index.html
├── cupo-en-dolares-antofagasta/index.html
├── cupo-en-dolares-la-serena/index.html
├── cupo-en-dolares-temuco/index.html
├── cupo-en-dolares-iquique/index.html
├── cupo-en-dolares-vina-del-mar/index.html
└── cupo-en-dolares-puerto-montt/index.html

⚠️  IGNORAR: agente/m6.html — legacy, no usar
⚠️  PENDIENTE: crear cupo-en-dolares-arica/ y cupo-en-dolares-talca/
```

---

## 4. DESIGN SYSTEM

```css
/* Colores */
--navy:       #0B1628
--navy-mid:   #112040
--gold:       #C9A84C
--gold-light: #E8C96A
--cream:      #F7F2E8

/* Tipografía */
Títulos:  Cormorant Garamond (serif) — self-hosted
Cuerpo:   DM Sans (sans) — self-hosted

/* Reglas de layout */
Header: SOLO logo + CTA "Cotizar ahora" → WhatsApp. SIN nav links.
WhatsApp flotante: bottom-right en TODAS las páginas sin excepción.
```

---

## 5. ZONAS SAGRADAS — NUNCA MODIFICAR

Estos valores son intocables. Si un cambio los afecta, detener y consultar.

| Elemento | Valor |
|----------|-------|
| GTM ID | `GTM-N622PKXV` |
| GA4 Measurement ID | `G-5MQM4R0Z52` |
| GA4 Property ID | `311192682` |
| Web3Forms key | `82fa11e9-11dc-46c4-947d-2195d4c94229` |
| Form recipient | `girodolares@gmail.com` |
| Form subject | `Nueva cotización — GiroDólares.cl` |
| WhatsApp | `+56963026000` (wa.me/56963026000) |
| Teléfono | `+56232108299` |
| Email | `info@girodolares.cl` |
| Canonical tags | No modificar estructura de URLs |

**Verificar antes de cualquier PR que estos valores siguen intactos.**

---

## 6. CLASIFICACIÓN DE PÁGINAS (TIERS)

| Tier | Páginas | Límite diff | Reglas extra |
|------|---------|-------------|--------------|
| **A — Golden** | `index.html`, `cupo-en-dolares/` | 40 líneas/PR | Soak 24h en preview, visual testing obligatorio |
| **B — SEO** | `blog/*`, `cupo-en-dolares-{ciudad}/*` | 100 líneas/PR | Workflow estándar |
| **B — Info** | `quienes-somos/`, `politica-de-privacidad/`, `terminos-y-condiciones/` | 100 líneas/PR | Workflow estándar |

**Default si no está clasificado: Tier A (más conservador).**

---

## 7. FLUJO DE TRABAJO CON CLAUDE CODE

```
1. Asegurarse de estar en main actualizado
   git checkout main && git pull

2. Crear branch con naming convention
   git checkout -b ai/proposal-[slug-corto]

3. Hacer los cambios en los archivos

4. Verificar que las Zonas Sagradas están intactas

5. Commit
   git add [archivos específicos]
   git commit -m "tipo: descripción corta"

6. Push
   git push origin ai/proposal-[slug-corto]

7. Crear PR
   gh pr create --title "descripción" --body "..." --label "ai-proposal"

8. STOP — esperar aprobación humana de Herny
   No hacer merge. No hacer deploy. No continuar.
```

### Naming de branches
```
ai/proposal-[slug]
Ejemplo: ai/proposal-mejora-faq-providencia
```

### Naming de commits
```
feat: nueva página o sección
fix: corrección de bug o error
seo: optimización de meta tags, H1, schema
content: actualización de contenido editorial
style: cambios de CSS sin afectar funcionalidad
```

---

## 8. REGLAS DE LINKING (NO NEGOCIABLES)

| Regla | Detalle |
|-------|---------|
| GD → satélites | **PROHIBIDO** |
| Satélite → satélite | **PROHIBIDO** |
| Satélite → GD | Solo como CTA editorial en cuerpo. Nunca en footer ni menú |
| Anchor text exacto keyword en satélite→GD | **PROHIBIDO** |
| GD blog → cupodolares.cl | Permitido como CTA editorial |

---

## 9. REGLAS SEO Y CONTENIDO

- Lenguaje: español chileno formal (no rioplatense, no neutro)
- Mercado: Chile exclusivamente
- Nicho YMYL: datos financieros solo con fuente verificada. Si no hay fuente, no incluir el dato.
- No mencionar competidores por nombre
- No urgencia falsa sin dato real
- No duplicar contenido entre sitios del ecosistema
- Schema permitidos: `FinancialService`, `FAQPage`, `Article`, `BreadcrumbList`, `HowTo`
- Schema prohibido: `Dataset`

### Datos operativos verificados (usar literal)
- Operación mínima: USD 300
- Tiempo: menos de 15 minutos
- Pago: mismo día hábil
- Desde: 2002
- Tarjetas: Visa, Mastercard, Amex
- Dirección: Av. Hernando de Aguirre 128-904, Suite #02, Providencia, Santiago

---

## 10. CONTENIDO PENDIENTE

### Blog (próximos según calendario)
- `blog/riesgos-vender-cupo-dolares/` — Mes 3-4 (YMYL, requiere fuentes)
- `blog/implicancias-tributarias-sii/` — Mes 3-4 (YMYL legal, requiere validación humana)

### Páginas nuevas
- `cupo-en-dolares-arica/index.html` — pendiente crear
- `cupo-en-dolares-talca/index.html` — pendiente crear
- `bancos-cupo-dolares-chile/index.html` — Mes 2 (schema: Article+FAQPage+ItemList, NO Dataset)

### Optimizaciones pendientes
- Fix CSS desktop: contenido ocupa solo 50% izquierdo en pantallas anchas (index.html)
- Interlinking interno: blog ↔ pillar ↔ ciudades
- Fotos oficina: 2 placeholders vacíos en index.html
- Agregar Protected DOM Regions en páginas Tier A
- Crear `_data/tiers.json`

---

## 11. ECOSISTEMA COMPLETO (repos relacionados)

| Repo | Dominio | Rol |
|------|---------|-----|
| `GiroCupo/girodolares-web` | girodolares.cl | **Este repo** — hub informacional |
| `GiroCupo/cupodolares-web` | cupodolares.cl | Motor de conversión |
| `GiroCupo/vendocupo-web` | vendocupo.cl | Satélite leads |
| `GiroCupo/ventadecupo-web` | ventadecupo.cl | Satélite leads |
| `GiroCupo/cambiocupo-web` | cambiocupo.cl | Satélite leads |
| `GiroCupo/cambiarcupo-web` | cambiarcupo.cl | Satélite leads |
| `GiroCupo/github-proxy` | api.girodolares.cl | Worker CF — orquestación AI |
| `GiroCupo/.github` | — | Docs canónicos + workflows reutilizables |

---

## 12. HERRAMIENTAS EXTERNAS (Claude Code no controla)

Estos sistemas viven fuera del repo. Claude Code puede sugerir cambios pero no ejecutarlos:

- **Google Analytics 4** — propiedad `311192682`
- **Google Tag Manager** — contenedor `GTM-N622PKXV`
- **Google Search Console** — girodolares.cl verificada
- **Cloudflare** — DNS, CDN, Pages, cache
- **Web3Forms** — formulario de contacto
- **Telegram** — alertas del Worker (`@Girocupo_alerts_bot`)

---

## 13. CHECKLIST PRE-PR

Antes de crear cualquier PR, verificar:

```
□ ¿Estoy en un branch ai/proposal-* (nunca en main)?
□ ¿El diff respeta el límite de líneas del Tier?
□ ¿GTM-N622PKXV sigue presente e intacto?
□ ¿Web3Forms key sigue igual?
□ ¿WhatsApp +56963026000 sigue presente?
□ ¿Canonical tags sin cambios?
□ ¿<h1> presente y no vacío?
□ ¿<meta name="description"> presente?
□ Si Tier A: ¿avisar a Herny para revisión visual en mobile y desktop?
□ ¿Ningún link nuevo apunta de GD hacia satélites?
```

---

*Documento mantenido en `GiroCupo/girodolares-web/CLAUDE.md`*
*Para cambios en este archivo: PR con label `docs`*
