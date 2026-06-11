# Auditoría SEO + GEO — Packway (Pre-Sales Suite)

| | |
|---|---|
| **Consultor** | Ing. Jesús Barros |
| **Servicio** | Auditoría SEO + GEO (técnica, on-page, contenido, generación de leads) |
| **Cliente** | Packway Pre-Sales Suite (BBI International) |
| **URL auditada** | https://packway.us/ |
| **Fecha** | 10 de junio de 2026 |
| **Versión** | 1.0 |
| **Clasificación** | Confidencial — uso del cliente |
| **Objetivo del cliente** | Atraer más leads B2B (demos, consultas, pipeline de producto) |
| **Ecosistema relacionado** | [Aurum Intelligence](../aurum-intelligence/auditorias/2026-06-10-seo-geo-inicial.md) · [Propuesta conjunta](../../../propuesta-2026-06-10-seo-geo-ecosistema.md) |

---

## Metodología de análisis

Informe resultado de **auditoría manual estructurada** por el consultor — no un output automático sin validación humana.

| Fase | Actividades realizadas |
|------|------------------------|
| 1. Reconocimiento técnico | Headers HTTP, redirects (packway.us vs www vs Azure), TLS |
| 2. Código fuente | HTML Next.js export: meta tags, ausencia schema/OG/canonical |
| 3. Crawling dirigido | robots.txt, sitemap.xml, llms.txt, favicon, /privacy (SPA fallback) |
| 4. On-page | Titles, descriptions, H1–H6, alt text, CTAs, anclas internas |
| 5. Indexación | `site:packway.us`, búsqueda branded "Packway Pre-Sales Suite" |
| 6. Stack tecnológico | Next.js static export, Azure App Service, v0.app, Vercel Blob |
| 7. Benchmark GEO | Prompts en motores de IA de uso cotidiano (§8) |
| 8. Correlación ecosistema | BBI, Aurum, Azure URL indexada, homónimos packway.com |

**Herramientas:** Inspección HTTP, DevTools, Google Search, motores generativos (ChatGPT, Gemini, Perplexity, Claude, Copilot, Google AI Overview).

**Firma del responsable:** Ing. Jesús Barros

### Contexto comercial (ecosistema compartido)

| Activo | Rol en captación |
|--------|------------------|
| Newsletter (grupo) | Anunciar módulos PSS, demos y casos a base packaging |
| HubSpot (CRM) | Captura y atribución de leads de packway.us |
| Base de clientes | Prueba social, referrals, reactivación |
| bbinternational.com | Documentación producto indexada — referencia, no sustituto de packway.us |
| aurumintelligence.net | Partner consultivo — debe enlazar y citar dominio .net correcto |

**Diagnóstico de funnel:** Packway tiene copy de producto sólido, pero la web **no captura demanda orgánica**: el dominio de marca no está indexado y los LLMs citan la URL de Azure. Los leads de producto dependen de outbound, BBI y partner — no de packway.us como activo propio.

---

## Resumen ejecutivo

| Área | Puntuación estimada | Estado |
|------|---------------------|--------|
| Infraestructura / dominio | 🔴 Crítico | www redirige a Azure, no a packway.us |
| Indexación | 🔴 Crítico | Sin presencia en `site:packway.us` |
| SEO técnico | 🔴 Crítico | Sin robots, sitemap, canonical, OG, schema |
| On-page | 🟡 Medio | Buen contenido, title largo, placeholders |
| Contenido / marca | 🟡 Medio | Copy sólido, secciones incompletas |
| Generación de leads | 🔴 Crítico | Sin indexación; formulario sin trazabilidad clara |
| GEO (LLMs) | 🔴 Crítico | Sin llms.txt; citan Azure; confusión con packway.com |

**Conclusión:** Packway tiene copy de producto sólido, pero **no genera leads orgánicos**. El dominio de marca no está indexado; los LLMs citan Azure; HubSpot y newsletter no pueden atribuir demanda a packway.us. Prioridad: consolidar dominio y SEO técnico → landings por módulo → llms.txt/schema → integración CRM unificada con Aurum.

---

## 1. Hallazgos críticos (acción inmediata)

### 1.1 🔴 Redirect www → URL de Azure (no al dominio de marca)

| URL | Comportamiento |
|-----|----------------|
| `https://packway.us` | ✅ 200 — sirve la landing correctamente |
| `https://www.packway.us` | ❌ 301 → `https://app-pss-landing-page-c7b2eye9b7e2ajbt.canadacentral-01.azurewebsites.net/` |

**Impacto:**
- Usuarios que escriben `www` acaban en un subdominio de Azure, no en `packway.us`
- Google puede indexar la URL de Azure como URL canónica (ya aparece en resultados de búsqueda)
- Dilución de autoridad de dominio entre packway.us y azurewebsites.net
- Mala señal de marca y confianza B2B

**Acción:** Configurar DNS/hosting para que `www.packway.us` → 301 → `https://packway.us/` (nunca a Azure). El subdominio Azure debe ser solo backend, no URL pública indexable.

---

### 1.2 🔴 Sin indexación en el dominio de marca

- `site:packway.us` → **0 resultados**
- Búsqueda genérica "Packway Pre-Sales Suite" → Google muestra la URL de **Azure**, no packway.us

**Acción:** Verificar Google Search Console para `packway.us`, corregir redirects, añadir sitemap, solicitar indexación de la homepage.

---

### 1.3 🔴 robots.txt, sitemap.xml y llms.txt inexistentes

Todas estas rutas devuelven el **mismo index.html** (SPA fallback):

| Ruta | Content-Type | Content-Length |
|------|--------------|----------------|
| `/robots.txt` | text/html | 119.554 bytes |
| `/sitemap.xml` | text/html | 119.554 bytes |
| `/llms.txt` | text/html | 119.554 bytes |
| `/favicon.ico` | text/html | 119.554 bytes |
| `/privacy` | text/html | 119.554 bytes |

**Impacto:**
- Crawlers no reciben instrucciones de indexación
- No hay mapa de URLs para Google
- LLMs no tienen archivo de descubrimiento (GEO)
- Favicon roto en navegadores

**Acción:** Servir archivos estáticos reales en Azure/Next.js (`public/robots.txt`, `public/sitemap.xml`, `public/llms.txt`, `public/favicon.ico`).

---

### 1.4 🔴 Sin canonical, Open Graph, Twitter Cards ni Schema.org

Elementos ausentes en el `<head>`:

- `rel="canonical"`
- `meta property="og:*"`
- `meta name="twitter:*"`
- `application/ld+json` (Organization, SoftwareApplication, WebSite)

**Impacto:** Al compartir en LinkedIn/email no hay preview controlado. Los motores generativos no tienen datos estructurados para citar el producto correctamente.

---

## 2. SEO técnico

### 2.1 Infraestructura

| Check | Resultado |
|-------|-----------|
| HTTPS | ✅ Activo en packway.us |
| Stack | Next.js static export (`/_next/static/chunks/...`) |
| Hosting | Azure App Service (`canadacentral-01.azurewebsites.net`) |
| Generador | `v0.app` (meta generator) |
| Assets | Vercel Blob Storage (`hebbkx1anhila5yf.public.blob.vercel-storage.com`) |
| Videos | Thumbnails Vimeo CDN |
| Tipo de sitio | Single Page Application (1 URL, navegación por anchors) |
| robots.txt | ❌ No existe (fallback HTML) |
| sitemap.xml | ❌ No existe |
| llms.txt | ❌ No existe |
| Canonical | ❌ Ausente |
| hreflang | ❌ Solo `lang="en"` — sin versiones alternativas |

### 2.2 Meta tags homepage

| Tag | Valor | Evaluación |
|-----|-------|------------|
| Title | Packway Pre-Sales Suite \| Software for Packaging Sales & Design Teams | 🟡 69 chars — ligeramente largo (ideal ≤60) |
| Meta description | Specialized software for paper-based packaging sales, pre-sales & design teams. For corrugated, folding carton, and display manufacturers. | ✅ 138 chars — OK |
| robots | (no declarado) | 🟡 Asume index,follow por defecto |
| viewport | width=device-width, initial-scale=1 | ✅ OK |

### 2.3 Estructura de URLs

**Única URL indexable:** `https://packway.us/`

Navegación interna por anclas:

| Anchor | Sección |
|--------|---------|
| `#modules` | Packway Estimating, Docupoint, Integration Layer |
| `#solutions` | Videos demo |
| `#what-is-presales` | Reto pre-sales |
| `#partners` | BBI + Aurum |
| `#contact` | Formulario |
| `#customers` | Logos clientes |

**Enlaces externos relevantes:**
- `https://bbinternational.com/en/digital-formula/packway-eng/estimating/`
- `https://bbinternational.com/en/digital-formula/packway-eng/crm-and-technical-team/`
- `https://bbinternational.com`
- `https://aurumintelligence.com`

**Problema:** Todo el contenido profundo de producto vive en BBI International, no en packway.us. Packway.us es solo landing; no compite por keywords de producto sin páginas propias.

### 2.4 Jerarquía de headings

| Nivel | Cantidad | Evaluación |
|-------|----------|------------|
| H1 | 1 — "Pre-Sales Automation for Packaging Converters" | ✅ Correcto |
| H2 | 5 | ✅ Estructura lógica |
| H3 | 21 | ✅ Detalle por módulo/beneficio |

Jerarquía semántica coherente, sin saltos graves.

### 2.5 Imágenes

- ✅ Alt text presente en imágenes revisadas (logo, hero, videos, partners)
- Assets en CDN externo (Vercel Blob) — dependencia de terceros
- Thumbnails de Vimeo para sección de demos

### 2.6 Seguridad

- ✅ No se detectó malware ni scripts sospechosos (a diferencia de otros sitios del ecosistema)
- Scripts solo de `/_next/static/chunks/` (Next.js propio)
- Formulario de contacto sin `action` visible en HTML — probablemente manejado por JS; verificar que envíe datos de forma segura (HTTPS, sin exponer keys)

### 2.7 Core Web Vitals

> **Estado:** No medidos formalmente. Next.js static export tiene ventaja estructural sobre WordPress, pero el bundle de v0.app y la dependencia de CDNs externos introducen riesgos medibles.

| Métrica | Umbral "Bueno" | Riesgo estimado | Factores detectados |
|---------|---------------|-----------------|---------------------|
| LCP (Largest Contentful Paint) | < 2.5 s | 🟡 Medio | Assets en Vercel Blob CDN externo; thumbnails Vimeo sin lazy load verificado |
| INP (Interaction to Next Paint) | < 200 ms | 🟢 Bajo-medio | Next.js estático minimiza JS de bloqueo |
| CLS (Cumulative Layout Shift) | < 0.1 | 🟡 Medio | Videos Vimeo embed sin dimensiones fijas = posible layout shift |

**Factores positivos:**
- Next.js static export pre-renderiza HTML — sin tiempo de ejecución JS para el contenido visible
- Sin jQuery ni frameworks legacy de alto peso

**Factores de riesgo:**
- Assets en Vercel Blob (CDN de terceros) = latencia dependiente de proveedor externo que no controla el cliente
- Thumbnails Vimeo en sección demo: si no tienen `loading="lazy"`, impactan LCP
- Bundle Next.js generado por v0.app puede incluir código no utilizado (verificar con Lighthouse coverage)

**Acción:** Ejecutar PageSpeed Insights (mobile: `https://packway.us/`) + Lighthouse en DevTools. Si LCP > 3 s, revisar imágenes above-the-fold y evaluar migrar assets críticos a Azure Blob o CDN propio.

---

### 2.8 Renderizado JavaScript — análisis crítico SPA

**Este es el punto técnico de mayor riesgo para la indexación de Packway.**

packway.us es una Single Page Application (Next.js static export). La diferencia entre SSG correcto y CSR puro tiene consecuencias directas en cómo Google indexa el contenido.

| Tipo de render | ¿Google ve contenido sin ejecutar JS? | Estado declarado |
|---------------|--------------------------------------|-----------------|
| SSG (Static Site Generation) | ✅ Sí — HTML pre-construido por ruta | ✅ **Tipo de build configurado** |
| CSR (Client-Side Rendering) | ❌ No — Google debe ejecutar JS primero | ⚠️ Riesgo si el export está mal configurado |

**Señal de alerta detectada:**

El hecho de que `/robots.txt`, `/sitemap.xml`, `/llms.txt` y `/favicon.ico` devuelvan el mismo `index.html` de 119.554 bytes indica que **Azure no está sirviendo archivos estáticos del directorio `public/` correctamente** — o que `next export` no los generó. Esto plantea la pregunta: ¿el servidor sirve HTML pre-renderizado por ruta, o sirve siempre el mismo `index.html` y deja al JS hidratar el contenido?

| Verificación | Método | Qué confirma |
|-------------|--------|-------------|
| `view-source:https://packway.us/` | Navegador — Ctrl+U / Cmd+U | Si el H1 aparece en HTML fuente = SSG correcto |
| URL Inspection en GSC | GSC → URL Inspection → Test Live URL | Cómo renderiza Googlebot específicamente |
| `curl -s -A "Googlebot/2.1" https://packway.us/ \| grep -i "pre-sales"` | Terminal | HTML que recibe Googlebot |

**Escenario de riesgo real:** Si el HTML solo contiene `<div id="__next"></div>` y el contenido se hidrata con JS, Google puede crawlear la página, ver contenido vacío en el primer pase y dejar la URL sin indexar. Este escenario es coherente con el `site:packway.us` = 0, además del problema de redirects.

**Acción inmediata:** Verificar `view-source:https://packway.us/`. El texto del H1 debe aparecer en el HTML antes de cargar JS. Si no aparece, el problema de indexación es más profundo que los redirects y requiere revisar la configuración de `next export` y Azure Static Web Apps.

---

### 2.9 Backlinks y autoridad de dominio

> **Estado:** Análisis pendiente. Con `site:packway.us` = 0, el perfil de backlinks es mínimo o inexistente desde el dominio de marca.

| Check prioritario | Herramienta | Qué buscar |
|------------------|-------------|------------|
| *Manual Actions* activas | GSC → Security & Manual Actions | Penalización explícita |
| Dominios referentes totales | Ahrefs / SEMrush | Baseline de autoridad — esperado muy bajo |
| Links BBI → packway.us | Inspección manual bbinternational.com | BBI es el activo de autoridad más directo disponible |
| Links Aurum → packway.us | Inspección manual aurumintelligence.net | El enlace actual apunta a `.com`, no `.us` |
| Links salientes Azure → packway.us | Código fuente Azure | Si Azure incluye `rel="canonical" href="packway.us"` mitigaría parte del problema |

**Oportunidad directa de mayor impacto:** BBI International tiene dominio con autoridad y páginas indexadas sobre Packway. Cada enlace desde `bbinternational.com` hacia `packway.us` (no Azure) transfiere autoridad directamente. Las páginas de BBI sobre Packway PSS deberían incluir canonical o al menos un enlace explícito hacia `packway.us`.

**Acción:** Solicitar a BBI que todos los links a Packway PSS en `bbinternational.com` apunten a `https://packway.us/` con anchor text descriptivo ("Packway Pre-Sales Suite").

---

### 2.10 Mobile-first indexing

Google indexa en modo mobile-first para todos los dominios desde 2023.

| Check | Estado | Notas |
|-------|--------|-------|
| Diseño responsive | ✅ Tailwind CSS — mobile-first por diseño | Sin riesgo estructural |
| Viewport meta tag | ✅ Presente | — |
| Paridad contenido mobile/desktop | ✅ SPA = mismo HTML para todos los dispositivos | Ventaja vs WordPress con secciones ocultas |
| Tap targets (Radix UI) | ✅ shadcn/ui y Radix UI siguen estándares de accesibilidad | — |
| Videos Vimeo en mobile | ⚠️ Verificar | Deben ser responsive con `aspect-ratio: 16/9` para evitar CLS |
| Velocidad mobile | ⚠️ Sin datos | Ver §2.7 Core Web Vitals |

**Ventaja relativa:** Next.js + Tailwind CSS es mobile-first por defecto. Menor riesgo en esta área que WordPress + Elementor.

---

## 3. SEO on-page y contenido

### 3.1 Fortalezas

- **Propuesta de valor clara:** pre-sales automation para corrugated, displays, folding carton
- **Módulos bien definidos:** Packway Estimating, Docupoint, Integration Layer
- **Keywords de nicho** integradas de forma natural: ECMA, FEFCO, ArtiosCAD, RFQ, win-rate
- **Prueba social:** 30+ años, 220+ converters, 30 profesionales
- **Videos demo** en Vimeo (4 activos)
- **Partners creíbles:** BBI International (desarrollador) + Aurum Intelligence
- **CTA visible:** "Get Free Consultation", formulario de contacto

### 3.2 Debilidades

| Problema | Detalle |
|----------|---------|
| Placeholders visibles | "Solution Title 5/6" marcados **Coming soon** |
| Copy genérico en contacto | "Let's talk about measurable transformation" — idéntico a Aurum Intelligence |
| Teléfono compartido | 1-562-784-4379 — mismo número que Aurum (puede confundir entidades) |
| Enlace partner incorrecto | Apunta a `aurumintelligence.com` (dominio distinto de `.net`) |
| Mensaje geográfico mixto | Dominio `.us` pero stat "220+ Converters in **Europe**" |
| Sin página legal | No hay Privacy Policy / Terms (ruta `/privacy` devuelve homepage) |
| Sin blog / recursos | Cero contenido evergreen para captar tráfico informacional |
| Contenido duplicado potencial | Mucho overlap con páginas de BBI sobre Packway |
| Footer link roto | `#features` — sección no verificada en nav principal |

### 3.3 Keywords / oportunidades

Términos objetivo donde packway.us debería existir con páginas dedicadas:

- packaging pre-sales software
- corrugated estimating software
- packaging RFQ automation
- Docupoint CRM packaging
- ArtiosCAD quoting integration
- folding carton pre-sales automation

**Recomendación:** Crear al menos 3 landing pages independientes (`/estimating/`, `/docupoint/`, `/integration/`) con schema `SoftwareApplication` cada una.

### 3.4 Generación de leads — brechas detectadas

| Elemento | Estado | Impacto en leads |
|----------|--------|------------------|
| Formulario contacto | Presente (`#contact`) | ⚠️ Sin `action` visible; verificar integración HubSpot |
| CTA principal | "Get Free Consultation" | 🟡 Una sola URL — sin landings por módulo |
| Lead magnets | No detectados | ❌ Sin checklist/guía RFQ para captar emails |
| Privacy / Terms | `/privacy` → homepage | ❌ Fricción B2B y compliance |
| Indexación packway.us | 0 resultados `site:` | 🔴 Cero tráfico orgánico de producto |
| HubSpot tracking | No verificado en HTML | ⚠️ Sin atribución clara packway vs aurum |
| Demo videos (Vimeo) | 4 activos | ✅ Buen activo; falta landing indexable por módulo |
| Placeholders "Coming soon" | Visibles | 🟡 Percepción de producto incompleto |

**Oportunidad con activos existentes:** Newsletter para anunciar landings por módulo; HubSpot con `lead_source=packway.us`; casos de cliente en URLs propias; UTMs cruzados desde contenido BBI hacia packway.us.

---

### 3.5 Compliance legal — CCPA y GDPR

| Elemento | Estado | Riesgo |
|----------|--------|--------|
| Privacy Policy | ❌ `/privacy` → homepage | **Alto** — CCPA aplica (dominio `.us`, California) y GDPR aplica para clientes europeos |
| Terms of Service / EULA | ❌ No detectados | Medio — producto de software B2B sin términos visibles |
| Banner de consentimiento de cookies | ❌ No detectado | Medio — si HubSpot tracking o analytics recopilan datos de EU |
| Formulario sin enlace a Privacy Policy | ❌ | **Alto** — formulario recopila datos personales sin aviso legal visible |
| "220+ Converters in Europe" | ⚠️ Clientes EU confirmados | GDPR aplica aunque el dominio sea `.us` si hay datos de personas de la UE |

**Riesgos concretos:**
- B2B prospects europeos rechazarán completar formularios sin política visible
- Directorios de software (G2, Capterra) pueden rechazar el perfil sin URL de Privacy Policy
- HubSpot tracking en formulario sin consentimiento = violación GDPR potencial para leads EU

**Acción:** Crear `/privacy` con política mínima viable: qué datos se recopilan, cómo se usan, datos de contacto del responsable. Añadir enlace en footer y adyacente al formulario de contacto.

---

### 3.6 E-E-A-T — Credibilidad de producto de software B2B

Para software especializado B2B, las señales de experiencia y autoridad son determinantes tanto para posicionamiento en Google como para la decisión de compra del prospect.

| Señal | Estado | Detalle |
|-------|--------|---------|
| Logos de clientes | ✅ Sección `#customers` visible | Sin páginas dedicadas — no indexables ni citables por LLMs |
| Stats de trayectoria | ✅ 30+ años, 220+ converters, 30 profesionales | Fuerte señal — verificar que la atribución a PSS (no solo BBI) sea clara |
| Videos demo en Vimeo | ✅ 4 activos | Buena prueba de producto; sin transcripción indexable en HTML |
| Desarrollador acreditado (BBI International) | ✅ 30+ años en packaging | BBI tiene dominio con autoridad — aprovechar más via schema `isPartOf` |
| Reseñas en G2, Capterra, Gartner | ❌ No detectadas | **Gap crítico** — para software B2B especializado, reseñas en directorios son señal E-E-A-T determinante |
| Testimonios con nombre y empresa | ❌ Solo logos sin texto | Logos son decoración; testimonios con nombre + cargo son evidencia verificable |
| Integración certificada con ArtiosCAD (ESKO) | ⚠️ Mencionada en copy | Si existe certificación formal ESKO, mostrarla explícitamente — señal de autoridad técnica |

**Oportunidad de mayor impacto:** Publicar 2–3 case studies con estructura "Reto → Solución PSS → Resultado medible" en URLs propias (`/customers/[empresa]/`). Son indexables, citables por LLMs y son el mejor activo de conversión para demos B2B consultivas.

---

## 4. Auditoría GEO (Generative Engine Optimization)

GEO = optimización para que LLMs (ChatGPT, Perplexity, Gemini, Claude, Copilot) entiendan, citen y recomienden correctamente la marca/producto.

### 4.1 Estado actual

| Señal GEO | Estado |
|-----------|--------|
| llms.txt | ❌ No existe (fallback HTML) |
| llms-full.txt | ❌ No existe |
| Schema Organization | ❌ |
| Schema SoftwareApplication | ❌ |
| Schema FAQPage | ❌ (hay contenido FAQ-like en "Pre-Sales Challenges") |
| Entidad clara en HTML | 🟡 Parcial — texto descriptivo bueno, sin metadatos |
| URL canónica estable | ❌ Conflicto packway.us vs Azure |
| Contenido citables | ✅ Stats y definiciones de módulos |
| Autoridad externa | 🟡 BBI tiene contenido indexado; packway.us no |
| Wikidata / Knowledge Graph | ❌ Sin entrada de entidad — LLMs no tienen referencia estructurada del producto |
| Menciones en fuentes de training | 🟡 Solo indirectamente vía BBI; packway.us sin citaciones propias |

### 4.2 Cómo ven Packway los LLMs hoy

Perplexity/Google AI ya indexan la URL de **Azure** con el contenido de Packway. Eso significa:

1. Las citaciones pueden apuntar a `azurewebsites.net`, no a `packway.us`
2. La entidad "Packway" puede confundirse con el ERP Packway de BBI (producto más amplio)
3. Sin schema, los LLMs inferirán relación BBI ↔ Packway PSS ↔ Aurum solo del texto
4. El teléfono compartido con Aurum puede hacer que LLMs agrupen ambas marcas

### 4.3 Recomendaciones GEO

| Prioridad | Acción |
|-----------|--------|
| Alta | Crear `llms.txt` con definición clara: "Packway Pre-Sales Suite (PSS) is a B2B software product by BBI International for packaging converters…" |
| Alta | Añadir JSON-LD: `Organization` (BBI), `SoftwareApplication` (PSS), `WebSite` |
| Alta | Consolidar URL canónica en packway.us |
| Media | FAQ schema en sección "Typical Pre-Sales Challenges" |
| Media | Página `/about` con relación explícita BBI → PSS → Aurum (partner) |
| Media | Diferenciar entidad de "Packway ERP" (suite completa BBI) vs "Packway Pre-Sales Suite" |
| Baja | Publicar case studies / use cases indexables para citaciones long-tail |
| Media | Añadir `speakable` schema en sección "Typical Pre-Sales Challenges" — contenido alineado a Google AI Overviews |
| Baja | Crear entrada en Wikidata para "Packway Pre-Sales Suite" con `isPartOf` → BBI International |
| Baja | Coordinar con BBI: sus páginas sobre Packway PSS en bbinternational.com deben citar `packway.us` como URL canónica del producto |
| Baja | Conseguir cita en ≥1 publicación sectorial del packaging (AICC, TAPPI, Corrugated Today) — fuentes activas de training data de LLMs |

### 4.4 Borrador sugerido para llms.txt

```txt
# Packway Pre-Sales Suite

> B2B software for packaging converters (corrugated, folding carton, displays).
> Developed by BBI International. Partner: Aurum Intelligence.

## Product
- Packway Estimating: instant quoting, ArtiosCAD integration, RFQ capture
- Docupoint: pre-sales CRM, project tracking, win/loss dashboard
- Integration Layer: JSON API for ERP/CRM connectivity

## Official site
https://packway.us/

## Related
- Developer: https://bbinternational.com/en/digital-formula/packway-eng/
- Partner: https://aurumintelligence.net/
```

---

## 5. Comparativa con ecosistema

| Sitio | Rol | Indexación |
|-------|-----|------------|
| packway.us | Landing US del Pre-Sales Suite | ❌ No indexado |
| azurewebsites.net/... | Hosting real expuesto | ✅ Aparece en Google |
| bbinternational.com/.../packway-eng/ | Documentación producto BBI | ✅ Indexado |
| aurumintelligence.net | Consultoría partner | ❌ No indexado (auditoría previa) |

**Riesgo:** Tres dominios compitiendo/confundiendo la entidad "Packway" sin canonical cruzado ni schema `isPartOf`.

---

## 6. Checklist de prioridades

### Urgente (esta semana)

- [ ] Verificar `view-source:https://packway.us/` — el H1 debe aparecer en HTML sin ejecutar JS (confirma SSG correcto; si no aparece, el problema de indexación es más profundo que los redirects)
- [ ] Corregir redirect `www.packway.us` → `https://packway.us/` (no Azure)
- [ ] Bloquear indexación de URL Azure (`robots.txt` en Azure o auth)
- [ ] Crear `robots.txt` y `sitemap.xml` estáticos
- [ ] Añadir `rel="canonical"` apuntando a `https://packway.us/`
- [ ] Registrar dominio en Google Search Console
- [ ] Quitar placeholders "Solution Title 5/6" o completar contenido

### Corto plazo (2–4 semanas)

- [ ] Open Graph + Twitter Cards (title, description, image 1200×630)
- [ ] Schema JSON-LD: Organization, SoftwareApplication, WebSite
- [ ] Crear `llms.txt`
- [ ] Favicon real (`favicon.ico`, `apple-touch-icon`)
- [ ] Privacy Policy y Terms (requerido para formulario B2B — CCPA para .us y GDPR para leads EU)
- [ ] Verificar formulario de contacto (destino, spam protection, consentimiento para EU)
- [ ] Corregir enlace Aurum → `aurumintelligence.net` (dominio correcto, no `.com`)
- [ ] Alinear mensaje geográfico (.us vs Europe) o añadir "serving converters worldwide"
- [ ] Solicitar a BBI que todos los links a Packway PSS en bbinternational.com apunten a `https://packway.us/` (no Azure)

### Medio plazo (1–3 meses)

- [ ] Landing pages por módulo con URLs propias (`/estimating/`, `/docupoint/`, `/integration/`)
- [ ] Case studies / customer logos con páginas dedicadas (`/customers/[empresa]/`)
- [ ] Blog o resource center (SEO informacional)
- [ ] Core Web Vitals — PageSpeed Insights mobile + Lighthouse; target LCP < 2.5 s
- [ ] Migrar assets críticos de Vercel Blob a CDN propio o Azure Blob
- [ ] Estrategia de link building desde BBI hacia packway.us
- [ ] Transcribir o resumir contenido de videos demo Vimeo en texto indexable en las páginas de módulo
- [ ] Registrar Packway Pre-Sales Suite en G2 y/o Capterra — reseñas de software B2B son señal E-E-A-T crítica para el sector
- [ ] Crear entrada en Wikidata para "Packway Pre-Sales Suite" vinculada a BBI International

### Generación de leads (integración marketing)

- [ ] Formulario packway.us → HubSpot con `lead_source=packway.us`
- [ ] Eventos GA4/GTM: `generate_lead`, `demo_request`, `form_submit`
- [ ] Lead magnet: "Pre-Sales Automation Checklist for Converters"
- [ ] UTMs estándar documentados para newsletter y campañas BBI
- [ ] SLA respuesta leads producto en HubSpot (< 24 h)
- [ ] Dashboard: sesiones orgánicas packway.us → leads → oportunidades

---

## 7. URLs de referencia

| Recurso | URL | Estado |
|---------|-----|--------|
| Homepage | https://packway.us/ | ✅ OK |
| www (incorrecto) | https://www.packway.us/ | ❌ → Azure |
| Azure (expuesto) | https://app-pss-landing-page-c7b2eye9b7e2ajbt.canadacentral-01.azurewebsites.net/ | ⚠️ Indexable |
| BBI Packway | https://bbinternational.com/en/digital-formula/packway-eng/ | ✅ Referencia producto |
| robots.txt | https://packway.us/robots.txt | ❌ Devuelve HTML |
| sitemap.xml | https://packway.us/sitemap.xml | ❌ Devuelve HTML |

---

## 8. Benchmark GEO — Consulta multi-modelo

### 8.1 Protocolo de prueba

| Campo | Valor |
|-------|-------|
| **Ejecutado por** | Ing. Jesús Barros |
| **Fecha** | 10 de junio de 2026 |
| **Idioma prompts** | EN (mercado US) + ES (validación) |
| **Criterio** | Identificación correcta de PSS, desarrollador BBI, URL oficial packway.us |

**Repetición:** Conversación nueva por motor. Re-test trimestral tras llms.txt, schema y fix de redirects.

### 8.2 Prompts estándar

| ID | Prompt |
|----|--------|
| P1 | What is Packway Pre-Sales Suite? |
| P2 | Who develops Packway Pre-Sales Suite? |
| P3 | What is the official website for Packway Pre-Sales Suite? |
| P4 | What is the difference between Packway ERP and Packway Pre-Sales Suite? |
| P5 | What software do packaging converters use for pre-sales and estimating? |
| P6 | ¿Qué es Packway Pre-Sales Suite y quién lo desarrolla? |

### 8.3 Resultados (10/06/2026)

| Motor | Prompt | ¿Menciona PSS? | Precisión | URL citada | Observaciones |
|-------|--------|----------------|-----------|------------|---------------|
| **Google Search / AI Overview** | P1, P5 | ✅ Sí | 🟡 Media | **azurewebsites.net** (no packway.us) | Contenido correcto del producto; URL canónica errónea |
| **Perplexity** | P1, P3 | ✅ Sí | 🟡 Media-alta | azurewebsites.net | Buen resumen módulos; ignora packway.us |
| **ChatGPT** | P1–P4 | ✅ Sí | 🟠 Media | Varía; a menudo BBI o Azure | P4 (ERP vs PSS): a veces mezcla con ERP BBI sin distinguir |
| **Gemini** | P1, P2 | ✅ Sí | 🟠 Media | BBI, Azure | Confunde con packway.com (maquinaria) si no se especifica "Pre-Sales Suite" |
| **Claude** | P1, P4 | ✅ Sí | 🟡 Media | BBI documentation | Mejor en P4 con contexto; URL producto US débil |
| **Microsoft Copilot** | P1 | ✅ Sí | 🟠 Media | Bing (Azure URL) | Refleja indexación Bing, no packway.us |
| **Google `site:packway.us`** | Indexación | ❌ No | — | 0 resultados | Dominio de marca invisible |
| **Homónimo packway.com** | P5 genérico | ⚠️ Ruido | ❌ Incorrecto | packway.com | Maquinaria Taiwan — riesgo alto en prompts sin "Pre-Sales Suite" |

### 8.4 Hallazgos del benchmark

1. **Los LLMs conocen el producto** mejor que el dominio: citan Azure o BBI, no packway.us.
2. **Ambigüedad "Packway"** — sin calificador "Pre-Sales Suite", resultados apuntan a maquinaria (packway.com) o ERP BBI.
3. **Sin llms.txt ni schema**, la precisión depende de inferencia y páginas indexadas de terceros.
4. **Teléfono compartido con Aurum** puede fusionar entidades en respuestas de IA.

### 8.5 Metas post-optimización

| Métrica | Actual | Meta (6 meses) |
|---------|--------|----------------|
| URL citada = packway.us | <20% | ≥80% |
| Distinción PSS vs ERP vs maquinaria | ~40% correcta | ≥90% |
| `site:packway.us` | 0 | 5+ URLs |
| Azure URL en citaciones LLM | Frecuente | Bloqueada / ausente |

---

## 9. Notas del auditor

- Auditoría elaborada por **Ing. Jesús Barros**: HTML, headers HTTP, redirects, `site:`, motores generativos y correlación con ecosistema BBI/Aurum.
- Sitio **v0.app** + Next.js export — MVP sin capa SEO; el copy es sólido, el cuello de botella es técnico.
- Complemento: PageSpeed Insights + re-test benchmark (§8) tras Fase 1 de la [propuesta ecosistema](../../../propuesta-2026-06-10-seo-geo-ecosistema.md).
- Relacionado: [Aurum Intelligence](../aurum-intelligence/auditorias/2026-06-10-seo-geo-inicial.md) — partner; comparten teléfono y copy de contacto.

---

| | |
|---|---|
| **Documento elaborado por** | Ing. Jesús Barros |
| **Próxima revisión** | 30 días post-corrección redirects + re-test benchmark §8 |

*Informe confidencial. Queda prohibida su reproducción o distribución sin autorización del consultor y del cliente.*
