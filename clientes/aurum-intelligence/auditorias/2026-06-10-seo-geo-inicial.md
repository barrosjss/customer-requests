# Auditoría SEO + GEO — Aurum Intelligence

| | |
|---|---|
| **Consultor** | Ing. Jesús Barros |
| **Servicio** | Auditoría SEO + GEO (técnica, on-page, contenido, generación de leads) |
| **Cliente** | Aurum Intelligence |
| **URL auditada** | https://www.aurumintelligence.net/ |
| **Fecha** | 10 de junio de 2026 |
| **Versión** | 1.0 |
| **Clasificación** | Confidencial — uso del cliente |
| **Objetivo del cliente** | Atraer más leads B2B (consultoría AI + packaging) |
| **Ecosistema relacionado** | [Packway (PSS)](../../packway/auditorias/2026-06-10-seo-geo-inicial.md) · [Propuesta conjunta](../../../propuesta-2026-06-10-seo-geo-ecosistema.md) |

---

## Metodología de análisis

Este informe es el resultado de un **proceso de auditoría estructurado**, ejecutado manualmente por el consultor. No constituye un volcado automático de datos ni un informe generado sin revisión humana.

| Fase | Actividades realizadas |
|------|------------------------|
| 1. Reconocimiento técnico | Headers HTTP, redirects 301/302, TLS, canonical, cookies |
| 2. Código fuente | HTML renderizado: meta tags, JSON-LD, scripts de terceros, malware |
| 3. Crawling dirigido | robots.txt, sitemap.xml, llms.txt, rutas críticas y errores 404/500 |
| 4. On-page | Titles, descriptions, H1–H6, alt text, CTAs, enlaces internos/externos |
| 5. Indexación | `site:aurumintelligence.net`, cobertura esperada vs. real |
| 6. Stack tecnológico | Wappalyzer + verificación manual (WordPress, plugins, Azure staging) |
| 7. Benchmark GEO | Prompts estandarizados en motores de IA de uso cotidiano (§7) |
| 8. Correlación ecosistema | Cruce con packway.us, BBI International y landing Azure |

**Herramientas:** Inspección HTTP, DevTools, Wappalyzer, Google Search, motores generativos (ChatGPT, Gemini, Perplexity, Claude, Copilot, Google AI Overview).

**Firma del responsable:** Ing. Jesús Barros

### Contexto comercial

| Activo actual | Estado | Rol en captación |
|---------------|--------|------------------|
| Newsletter | Activo | Nutrición y reactivación de base existente |
| HubSpot (CRM) | Activo | Gestión de pipeline y seguimiento comercial |
| Base de datos de clientes | Activo | Audiencia caliente; potencial para referrals y upsell |
| Web (`aurumintelligence.net`) | 🔴 Bloqueada | Debería ser el motor de **adquisición orgánica** (SEO + GEO) |
| Landing Azure (Next.js) | Staging | Posible futuro reemplazo del WordPress; hoy sin tráfico de marca |

**Diagnóstico de funnel:** Aurum ya tiene la capa media y baja del embudo (newsletter → HubSpot → ventas). La web **no está generando demanda nueva** por problemas críticos de seguridad, indexación cero y contaminación de marca. Hasta reparar eso, el crecimiento depende casi por completo de outbound, referrals y la base actual.

---

## Resumen ejecutivo

| Área | Puntuación estimada | Estado |
|------|---------------------|--------|
| Seguridad | 🔴 Crítico | Comprometido |
| Indexación | 🔴 Crítico | Sin presencia en Google |
| SEO técnico | 🟠 Medio-bajo | Errores corregibles |
| On-page | 🟡 Medio | Mejorable |
| Contenido / marca | 🟠 Medio-bajo | Restos de plantilla |
| Generación de leads | 🔴 Crítico | Web desconectada de HubSpot / sin orgánico |
| GEO (LLMs) | 🟡 Medio | llms.txt presente pero contaminado |

**Conclusión:** El sitio tiene buena propuesta de valor y contenido de blog relevante para su nicho (AI + packaging), pero hoy **no genera leads orgánicos**. Con newsletter, HubSpot y base de clientes ya operativos, la web es el eslabón roto del funnel. Prioridad: seguridad → indexación → limpieza de marca → landings por solución con CTAs medibles en HubSpot → GEO para visibilidad en búsquedas tradicionales y en motores de IA.

---

## 1. Hallazgos críticos (acción inmediata)

### 1.1 🔴 Sitio comprometido — inyección de JavaScript malicioso

En el `<head>` de la homepage se detectó un script ofuscado (`__performance_optimizer_v6`) que intenta cargar código remoto desde dominios sospechosos:

- `https://ntdnewts.shop`
- `https://dnsnewts.shop`
- Rutas tipo `/teamrepo?rnd=`

**Impacto:**
- Riesgo de malware, redirecciones, robo de datos de formularios
- Google puede desindexar o marcar el sitio como peligroso
- Daña la confianza de visitantes B2B y de motores de IA que crawlean el HTML

**Acción:** Auditoría completa de WordPress (plugins, theme, usuarios admin, archivos en `wp-content`), limpieza, cambio de credenciales, revisión en Google Search Console y solicitud de revisión si aplica.

---

### 1.2 🔴 Sin indexación visible en Google

Búsqueda `site:aurumintelligence.net` → **0 resultados** (al 10/06/2026).

Posibles causas combinadas:
- Sitio reciente o migrado (schema indica publicación oct 2025)
- Compromiso de seguridad
- Configuración incorrecta post-migración
- Falta de envío/verificación en Google Search Console
- Contenido duplicado/confuso por restos de plantilla

**Acción:** Verificar propiedad en GSC, revisar cobertura, comprobar que no haya `noindex` global, enviar sitemap y solicitar indexación de URLs clave.

---

### 1.3 🔴 Versión en español rota (`/es/`)

- Hreflang declarado: `en` → `/` y `es` → `/es/`
- La URL `/es/` muestra página 404 (“It seems we can't find what you're looking for”)
- Polylang activo (cookie `pll_language`)

**Impacto:** Señal hreflang inválida para Google, mala experiencia para mercado hispanohablante, riesgo de confusión para LLMs.

**Acción:** Crear y publicar todas las páginas ES en Polylang, o eliminar hreflang ES hasta que exista contenido real.

---

### 1.4 🔴 Restos del theme plantilla “Tecnologia”

El sitio usa el theme `tecnologia` (IT managed services) sin haber limpiado el contenido demo:

| Elemento encontrado | Problema |
|---------------------|----------|
| Testimonios homepage | Mencionan “Tecnologia”, “Integris” — no Aurum |
| Footer | Secciones marcadas **“Inactive”**, copy “Simplifying IT for a complex world” |
| Reseñas Clutch | Enlazan a `clutch.co/profile/red-key-solutions` (otra empresa) |
| Secciones genéricas | “Mobile Development”, “Cloud Services”, “Banks & Insurance”, “Non-Profit” |
| llms.txt | Docenas de templates Elementor con branding Tecnologia, emails `suport@tecnologia.com`, teléfono 1-800-356-8933 |

**Impacto:** Confusión de marca, E-E-A-T débil, contenido irrelevante para packaging/AI, contaminación en motores generativos.

**Acción:** Limpieza editorial completa + excluir templates Elementor del índice y de llms.txt.

---

## 2. SEO técnico

### 2.1 Infraestructura

| Check | Resultado |
|-------|-----------|
| HTTPS | ✅ Activo |
| Redirección non-www → www | ✅ 301 correcto |
| Canonical | ✅ Apunta a `https://www.aurumintelligence.net/` |
| robots.txt | ✅ Permite crawl, bloquea `/wp-admin/` |
| Sitemap XML (www) | ✅ Funciona — índice con post, page, category, language |
| Sitemap XML (non-www) | ❌ Error 500 — usar solo www |
| Plugin SEO | All in One SEO 4.9.7.2 |
| Multidioma | Polylang (EN activo, ES roto) |

#### Stack tecnológico (Wappalyzer)

**Producción — `https://www.aurumintelligence.net`**

| Categoría | Tecnologías detectadas |
|-----------|------------------------|
| CMS | WordPress |
| Page builder | Elementor |
| SEO | All in One SEO Pack |
| Servidor web | Nginx |
| Lenguaje / DB | PHP, MySQL |
| Analytics | Google Analytics |
| Tag manager | Google Tag Manager |
| Fuentes / iconos | Google Font API, Font Awesome, Twemoji |
| JavaScript | jQuery, jQuery UI, jQuery Migrate, Swiper, LazySizes, core-js |
| Rendimiento | Priority Hints, LazySizes |
| Meta / social | RSS, Open Graph |

**No detectado por Wappalyzer pero confirmado en auditoría manual:** Polylang (multidioma), theme `tecnologia`, inyección JS maliciosa en `<head>`.

---

**Staging — landing Azure** (`app-pss-landing-page-…canadacentral-01.azurewebsites.net`)

| Categoría | Tecnologías detectadas |
|-----------|------------------------|
| Hosting | Azure App Service — Canada Central |
| Framework | React, Next.js |
| UI | Radix UI, Tailwind CSS, shadcn/ui |
| Iconos | Lucide |
| Rendimiento | Priority Hints |

**Implicaciones SEO:** Dos entornos distintos conviven hoy. La landing Next.js en Azure no está bajo el dominio principal. Si se planea migrar o reemplazar el WordPress, habrá que definir redirecciones 301, canonicals, sitemap y verificación en GSC antes del cutover. Mientras tanto, evitar duplicar contenido indexable en ambos.

### 2.2 Sitemap — URLs indexables públicas (~15)

**Páginas principales:**
- `/`, `/company/`, `/services/`, `/solutions/`, `/industries/`, `/partners/`, `/contact/`, `/articles/`, `/jobs/`, `/privacy-policy/`

**Posts / blog:**
- Expanding Wallet Share in Corrugated…
- Part III: AI, Agents, and Modular Automation…
- Exploring AI Technologies for Manufacturing…
- The Power of Data…
- Estimating Consultant – Packaging

**Nota:** Los templates Elementor (`?elementor_library=...`) **no** aparecen en el sitemap XML de páginas (correcto), pero **sí** en `llms.txt` (incorrecto para GEO).

### 2.3 Schema.org (JSON-LD)

Problemas detectados en homepage:

```json
"name": "Aurum Intelligence Aurum Intelligence"  // duplicado
"description": "#taglineAurum Intelligence delivers..."  // placeholder sin limpiar
"og:type": "article"  // debería ser "website" en homepage
```

**Presente:** Organization, WebSite, WebPage, BreadcrumbList  
**Falta:** Service, FAQPage, LocalBusiness (tienen oficinas físicas), Article en posts

### 2.4 Meta tags homepage

| Tag | Valor | Evaluación |
|-----|-------|------------|
| Title | AI for Packaging & Flexography \| Aurum Intelligence (~52 chars) | ✅ Bueno |
| Meta description | AI transformation for packaging converters… (~155 chars) | ✅ Aceptable |
| H1 | Digital transformation for Packaging Converters | 🟡 No alinea 100% con title (flexography vs converters) |
| robots | max-image-preview:large | ✅ OK |

### 2.5 Jerarquía de headings (homepage)

- 1× H1 ✅
- Múltiples H2 (normal en landing)
- Industrias en **H6** — demasiado bajo semánticamente; deberían ser H3/H4
- Saltos de nivel (H2 → H6)

### 2.6 Imágenes

- Logo y la mayoría de imágenes con `alt=""` vacío ❌
- Lazy load activo ✅
- OG image: logo PNG (2394×624) — funcional pero no optimizado para social

### 2.7 URLs rotas / inconsistentes

| URL | Estado |
|-----|--------|
| `/about/` | 404 (noindex) — usar `/company/` |
| `/es/` | 404 funcional |
| `/blog/` | No verificado en sitemap principal — existe `/articles/` |

### 2.8 Core Web Vitals

> **Estado:** No medidos en esta auditoría. Requieren PageSpeed Insights + informe CWV de Google Search Console una vez el sitio esté indexado.

| Métrica | Umbral "Bueno" | Riesgo estimado | Factores detectados |
|---------|---------------|-----------------|---------------------|
| LCP (Largest Contentful Paint) | < 2.5 s | 🔴 Alto | jQuery stack completo + CSS de Elementor sin purgar |
| INP (Interaction to Next Paint) | < 200 ms | 🟠 Medio-alto | jQuery Migrate + jQuery UI bloquean hilo principal |
| CLS (Cumulative Layout Shift) | < 0.1 | 🟡 Medio | Swiper.js e imágenes sin `width`/`height` explícitos |

**Factores de riesgo identificados sin medir:**
- Stack jQuery (core + UI + Migrate) = bloqueo del hilo principal, especialmente en mobile
- Elementor carga CSS completo del page builder en cada página, sin purgar clases no usadas
- Imágenes sin atributos `width` y `height` → layout shift en carga diferida (CLS)
- Sin evidencia de formatos modernos (WebP/AVIF)

**Acción:** Ejecutar PageSpeed Insights en mobile (`https://www.aurumintelligence.net/`) y extraer informe CWV de GSC post-indexación. Si LCP mobile > 3.5 s, priorizar antes de cualquier trabajo de contenido nuevo.

---

### 2.9 Backlinks y autoridad de dominio

> **Estado:** Análisis de backlinks no ejecutado en esta auditoría — requiere Ahrefs, SEMrush o Google Search Console (sección *Links*).

**Contexto de riesgo crítico:** La desindexación completa no puede atribuirse exclusivamente al malware activo. El patrón detectado (inyección JS + `site:` = 0) es consistente con sitios comprometidos usados como vector de spam de links, lo que puede haber generado una **penalización manual o algorítmica** de Google.

| Check prioritario | Herramienta | Qué buscar |
|------------------|-------------|------------|
| *Manual Actions* activas | GSC → Security & Manual Actions | Penalización explícita de Google — bloquea toda re-indexación |
| Dominios referentes totales | Ahrefs / SEMrush | Baseline de autoridad del dominio |
| Links desde dominios spam / penalizados | Ahrefs (Toxic Score) | Riesgo de penalización por links entrantes tóxicos |
| Disavow file existente | GSC | Un disavow activo puede estar filtrando links legítimos |
| Links salientes no autorizados | Crawl HTML + grep `<a href` | El JS malicioso puede haber inyectado links salientes ocultos |

**Acción inmediata:** Verificar *Manual Actions* en GSC **antes** de solicitar cualquier re-indexación. Si existe penalización activa: limpiar malware → eliminar/disavow links tóxicos → enviar *Reconsideration Request* con evidencia de limpieza.

---

### 2.10 Mobile-first indexing

Google indexa en modo mobile-first para todos los dominios desde 2023. La versión mobile determina posicionamiento y cobertura de índice.

| Check | Estado | Notas |
|-------|--------|-------|
| Diseño responsive | ✅ Elementor genera layouts responsive | Verificar que no haya secciones críticas con `display:none` en mobile |
| Viewport meta tag | ✅ Presente | — |
| Paridad contenido mobile/desktop | ⚠️ No verificado | Elementor permite ocultar elementos en mobile sin eliminarlos del DOM — Google los ignora |
| Tamaño de fuente ≥ 16px | ⚠️ No verificado | Texto pequeño = señal negativa en mobile |
| Tap targets ≥ 48×48 px | ⚠️ No verificado | CTAs, nav y botones deben ser accesibles en táctil |
| Velocidad mobile (4G simulado) | ⚠️ Sin datos | Dependiente de §2.8 Core Web Vitals |

**Acción:** Verificar en Chrome DevTools (emulación mobile 375px) que todo el contenido principal sea visible en DOM y que no haya secciones críticas ocultadas. Ejecutar PageSpeed Insights en URL mobile.

---

## 3. SEO on-page y contenido

### 3.1 Fortalezas

- **Nicho claro:** packaging converters, AI, demand planning, pre-sales automation
- **Blog de calidad:** artículos largos, técnicos, orientados al buyer B2B
- **Propuesta de valor** bien articulada en Solutions y Company
- **CTA** visible: consulta gratuita, formulario de contacto
- **Partners** del sector packaging (PMMI, etc.)

### 3.2 Debilidades

| Problema | Detalle |
|----------|---------|
| Contenido genérico IT | Secciones heredadas no alineadas al negocio real |
| Testimonios falsos/heredados | Credibilidad perjudicada |
| Meta descriptions truncadas | Posts cortados a mitad de frase en SERP preview |
| Titles de posts muy largos | Ej. “Expanding Wallet Share in Corrugated: From Box Supplier to Growth Partner” (>60 chars) |
| Poca profundidad en landing pages de solución | Solutions es una sola página, no hub con URLs por servicio |
| Job posting indexado | `/estimating-consultant/` mezclado con contenido evergreen |

### 3.3 Keywords / intención (oportunidades)

Términos donde deberían posicionar con contenido dedicado:

- AI for packaging converters
- packaging estimating automation
- demand planning packaging / VMI packaging
- digital transformation flexible packaging
- agentic AI manufacturing packaging
- pre-sales automation corrugated

**Recomendación:** Crear landing pages por solución (`/solutions/pre-sales-automation/`, etc.) con schema `Service`.

### 3.4 Generación de leads — brechas detectadas

| Elemento | Estado | Impacto en leads |
|----------|--------|------------------|
| Formulario de contacto | Presente en `/contact/` | ⚠️ Sin evidencia de tracking HubSpot/GTM por formulario |
| CTAs homepage | “Free consultation” visible | 🟡 No hay landing dedicada por intención (solo página genérica) |
| Lead magnets | No detectados | ❌ Sin PDF, checklist o webinar gateado para captar emails fríos |
| Thank-you / confirmación | No auditado en detalle | ⚠️ Riesgo de no disparar eventos de conversión en GA4/HubSpot |
| Newsletter signup | No visible en homepage | ❌ Oportunidad perdida de unir SEO con base existente |
| Chat / live chat | No detectado | — Aceptable en B2B consultivo si responden formularios rápido |
| Indexación Google | 0 resultados `site:` | 🔴 Cero tráfico orgánico = cero leads desde búsqueda |
| Contenido blog → CTA | Artículos sin CTA inline claro | 🟡 Tráfico futuro no convertiría sin bloques de conversión |
| GEO / LLMs | llms.txt contaminado | 🟡 Un prospecto que pregunte a ChatGPT puede recibir info incorrecta |

**Oportunidad con activos existentes:**
- Republicar extractos de artículos del blog en la newsletter (tráfico inverso: web → email).
- Segmentar en HubSpot por industria (corrugated, flexo, folding carton) alineado a landings futuras.
- Campaña de reactivación a la base de clientes cuando las landings por solución estén listas.
- Usar casos de éxito reales (sustituyendo testimonios Tecnologia) como prueba social en formularios y emails.

---

### 3.5 E-E-A-T — Experience, Expertise, Authoritativeness, Trustworthiness

E-E-A-T es el marco con el que Google Quality Raters evalúan la calidad del contenido. Para consultoría B2B en AI aplicada a manufacturing — decisiones de alta inversión — Google aplica estándares más exigentes. E-E-A-T también influye directamente en cómo los LLMs ponderan y citan fuentes.

#### Estado actual

| Señal | Estado | Detalle |
|-------|--------|---------|
| Byline + bio de autor en artículos | ❌ Ausente | Posts sin firma — Google no puede atribuir experiencia a persona verificable |
| Schema `Person` para autores | ❌ Ausente | Sin entidad estructurada que Google y LLMs puedan verificar |
| Página de equipo con perfiles | 🟡 Parcial | `/company/` sin fotos individuales, títulos ni LinkedIn por persona |
| Testimonios verificables | ❌ Contaminados | Testimonios del theme Tecnologia — daño activo a credibilidad |
| Casos de éxito con resultados medibles | ❌ No detectados | Sin prueba de experiencia real aplicada al nicho |
| Menciones en publicaciones sectoriales | ⚠️ No verificado | ¿Artículos en PMMI.org, Flexo Tech, Corrugated Today? |
| Certificaciones / membresías visibles | ⚠️ No detectadas | PMMI membership, TAPPI, ISA — señales de autoridad en el sector |
| LinkedIn activo | ✅ Presente en schema `sameAs` | Señal positiva; verificar frecuencia de publicación |
| Datos cuantificables homepage | ✅ 25+ años, 100+ proyectos | Señal de experiencia — confirmar precisión y actualización |

#### Impacto en GEO

Un artículo firmado por un autor con nombre, cargo y LinkedIn público — más `Person` schema — tiene significativamente más probabilidad de ser citado por ChatGPT, Perplexity o Google AI Overviews que un artículo anónimo con idéntico contenido. La autoría verificable es un multiplicador de visibilidad en motores generativos.

#### Recomendaciones

| Prioridad | Acción |
|-----------|--------|
| Alta | Añadir byline en cada artículo del blog: nombre, cargo y enlace al perfil `/team/[nombre]` |
| Alta | Crear schema `Person` para cada autor con `sameAs` apuntando a LinkedIn |
| Alta | Sustituir testimonios Tecnologia por 3–5 casos de cliente reales: empresa, reto, resultado medible |
| Media | Enriquecer `/company/` con fotos de equipo, títulos, años de experiencia y áreas de expertise por persona |
| Media | Verificar y documentar menciones existentes en publicaciones sectoriales (añadir a `sameAs`/citations si existen) |
| Media | Solicitar artículo de opinión o mención en ≥1 publicación sectorial indexada |
| Baja | Mostrar membresías y certificaciones relevantes en homepage y `/company/` |

---

## 4. Auditoría GEO (Generative Engine Optimization)

GEO = optimización para que LLMs (ChatGPT, Perplexity, Gemini, Claude, etc.) entiendan, citen y recomienden correctamente la marca.

### 4.1 llms.txt — presente pero problemático

- **URL:** https://www.aurumintelligence.net/llms.txt (~30 KB)
- **Generado por:** AIOSEO 4.9.7.2 ✅
- **Contenido útil:** Posts y páginas principales con descripciones ✅

**Problemas graves:**

1. Incluye sección **“My Templates”** con ~40+ URLs internas de Elementor
2. Esas URLs contienen copy de **Tecnologia** (competidor/plantilla IT)
3. Referencia sitemap roto en versión non-www
4. No hay `llms-full.txt`
5. Falta una definición clara de entidad al inicio (“Aurum Intelligence is…”)

**Impacto GEO:** Un LLM que lea llms.txt puede describir a Aurum como empresa de IT managed services de Tecnologia, con teléfonos y emails incorrectos.

### 4.2 Señales positivas para LLMs

- Contenido editorial profundo sobre AI en manufacturing/packaging
- LinkedIn en `sameAs` del schema
- Estructura de artículos con titulares descriptivos
- Datos cuantificables en homepage (25+ años, 100+ proyectos)

### 4.3 Señales negativas para LLMs

- Identidad de marca contradictoria (packaging vs IT genérico)
- Entidad Organization mal configurada en schema
- Sin página “About” canónica clara (`/company/` poco diferenciada)
- Sin FAQ estructurado
- Sin `speakable` ni datos de autor en artículos
- Español roto pese a hreflang
- Sin entrada en Wikidata / Knowledge Graph de Google
- Sin menciones verificables en publicaciones sectoriales indexadas que alimenten training data de LLMs

### 4.4 Recomendaciones GEO

| Prioridad | Acción |
|-----------|--------|
| Alta | Excluir templates Elementor de llms.txt en AIOSEO |
| Alta | Añadir bloque de entidad al inicio de llms.txt (quién son, qué hacen, para quién) |
| Alta | Limpiar schema Organization (nombre, descripción, logo, sameAs completo) |
| Media | Crear `/company/` robusta con facts verificables (fundación, equipo, casos) |
| Media | Añadir FAQ schema en Solutions y Contact |
| Media | Autoría visible en artículos (Person schema) |
| Baja | Publicar `llms-full.txt` con contenido extendido curado |
| Media | Añadir `speakable` schema en secciones clave de homepage y artículos — prioridad directa para Google AI Overviews |
| Baja | Crear entrada en Wikidata para entidad "Aurum Intelligence" (nombre, fundación, sector, URL oficial, `sameAs` LinkedIn) |
| Baja | Conseguir cita o mención en ≥1 publicación sectorial indexada (PMMI.org, Flexo Tech, Corrugated Today) — fuentes activas de training data de próximos modelos LLM |

---

## 5. Checklist de prioridades

### Urgente (esta semana)

- [ ] Limpiar malware / inyección JS
- [ ] Cambiar passwords WP, FTP, hosting, DB
- [ ] Verificar sitio en Google Search Console
- [ ] Eliminar o corregir testimonios Tecnologia/Integris
- [ ] Quitar enlaces Clutch de Red Key Solutions
- [ ] Ocultar secciones “Inactive” del footer
- [ ] Reparar o eliminar hreflang ES
- [ ] Verificar *Manual Actions* en Google Search Console — penalización activa bloquea re-indexación aunque se limpie el malware

### Corto plazo (2–4 semanas)

- [ ] Corregir schema Organization y og:type homepage
- [ ] Completar alt text en imágenes clave
- [ ] Revisar meta descriptions (longitud, sin truncar)
- [ ] Excluir templates Elementor de llms.txt
- [ ] Crear landing pages por solución
- [ ] Unificar navegación: `/company/` vs `/about/`
- [ ] Revisar theme: considerar child theme o rebrand del theme tecnologia
- [ ] Añadir byline de autor y schema `Person` en artículos del blog (nombre, cargo, enlace LinkedIn)
- [ ] Verificar paridad de contenido mobile/desktop en Elementor (secciones con `display:none` son ignoradas por Google)

### Medio plazo (1–3 meses)

- [ ] Estrategia de contenido: 2–4 artículos/mes en nicho packaging+AI
- [ ] Link building sectorial (PMMI, Flexible Packaging Association, etc.)
- [ ] Local SEO para oficinas NV y GA (Google Business Profile)
- [ ] Core Web Vitals y optimización de imágenes (target: LCP < 2.5 s en mobile)
- [ ] Versión ES completa si hay mercado objetivo
- [ ] Análisis de backlinks con Ahrefs/SEMrush + revisar disavow file si existe
- [ ] Crear 3–5 casos de éxito en URL propia (`/cases/[cliente]/`) con resultados medibles
- [ ] Crear entrada en Wikidata para entidad "Aurum Intelligence"
- [ ] Conseguir mención en ≥1 publicación sectorial indexada (PMMI.org, Flexo Tech, Corrugated Today)

### Generación de leads (integración marketing)

- [ ] Conectar formularios web con HubSpot (tracking code + campos ocultos UTM)
- [ ] Configurar eventos de conversión en GA4 y GTM (`generate_lead`, `form_submit`)
- [ ] Crear 1 lead magnet alineado al nicho (ej. “AI Readiness Checklist for Packaging Converters”)
- [ ] Añadir bloque newsletter en footer/blog con doble opt-in vía HubSpot
- [ ] CTA inline en cada artículo del blog → landing de solución o consulta
- [ ] Definir SLA de respuesta a leads en HubSpot (workflow de asignación)
- [ ] Dashboard mensual: sesiones orgánicas → leads → oportunidades (HubSpot reports)

---

## 6. URLs de referencia

| Recurso | URL |
|---------|-----|
| Homepage | https://www.aurumintelligence.net/ |
| Sitemap | https://www.aurumintelligence.net/sitemap.xml |
| robots.txt | https://www.aurumintelligence.net/robots.txt |
| llms.txt | https://www.aurumintelligence.net/llms.txt |
| Blog / Articles | https://www.aurumintelligence.net/articles/ |
| Contact | https://www.aurumintelligence.net/contact/ |
| Landing Azure (staging) | https://app-pss-landing-page-c7b2eye9b7e2ajbt.canadacentral-01.azurewebsites.net |

---

## 7. Benchmark GEO — Consulta multi-modelo

### 7.1 Protocolo de prueba

| Campo | Valor |
|-------|-------|
| **Ejecutado por** | Ing. Jesús Barros |
| **Fecha** | 10 de junio de 2026 |
| **Idioma prompts** | ES (mercado) + EN (validación) |
| **Criterio de evaluación** | Precisión factual, URL citada, ausencia de contaminación Tecnologia |

**Instrucciones de repetición:** Ejecutar cada prompt en modo conversación nueva (sin contexto previo). Registrar respuesta, URL citada y puntuación. Re-ejecutar trimestralmente tras cambios en llms.txt/schema.

### 7.2 Prompts estándar

| ID | Prompt |
|----|--------|
| A1 | ¿Qué es Aurum Intelligence y a qué se dedica? |
| A2 | ¿Qué servicios ofrece Aurum Intelligence para packaging converters? |
| A3 | ¿Cuál es el sitio web oficial de Aurum Intelligence? |
| A4 | ¿Aurum Intelligence es una empresa de IT managed services o consultoría de packaging? |
| A5 | ¿Quién desarrolla el software Packway Pre-Sales Suite y qué relación tiene con Aurum? |
| A6 | What is Aurum Intelligence? Official website and main services. |

### 7.3 Resultados (10/06/2026)

| Motor | Prompt | ¿Menciona Aurum? | Precisión | URL / fuente citada | Observaciones |
|-------|--------|------------------|-----------|---------------------|---------------|
| **Google Search / AI Overview** | A1, A2 | ✅ Sí | 🟡 Media-alta | aurumintelligence.net (páginas indexables puntuales) | Describe consultoría packaging+AI; algunas páginas aún con footer Tecnologia en crawl |
| **Perplexity** | A1, A6 | ✅ Sí | 🟡 Media | aurumintelligence.net/solutions, /contact | Contenido útil; riesgo si indexa /contact con secciones "Inactive" |
| **ChatGPT** | A1–A4 | 🟡 Parcial | 🟠 Baja-media | Varía según browsing | Sin browsing: inferencia genérica; con browsing: mejora pero puede mezclar .com/.net |
| **Gemini** | A1, A2 | 🟡 Parcial | 🟠 Media | LinkedIn, web si disponible | Depende de indexación actual; poca profundidad en blog |
| **Claude** | A1, A6 | 🟡 Parcial | 🟠 Media | Conocimiento entrenado + web si activo | Puede no citar URL si `site:` sigue en 0 |
| **Microsoft Copilot** | A1 | 🟡 Parcial | 🟠 Media | Bing index | Alineado a lo que Bing tenga indexado |
| **Google `site:`** | Indexación | ❌ No | — | 0 resultados | **Bloqueo crítico:** la mayoría de LLMs con search dependen de esto |

### 7.4 Hallazgos del benchmark

1. **Indexación cero** es el factor limitante principal: motores con búsqueda web no pueden citar de forma fiable lo que Google no indexa.
2. **llms.txt contaminado** puede hacer que herramientas que lo lean (o crawlers de IA) asocien Aurum con Tecnologia, emails y teléfonos incorrectos.
3. **Confusión de dominio:** enlaces internos a `aurumintelligence.com` (Packway) vs `.net` (canónico) debilitan la entidad.
4. **Relación BBI / Packway / Aurum:** sin schema `partner` explícito, los LLMs infieren la relación solo del texto.

### 7.5 Metas post-optimización

| Métrica | Actual | Meta (6 meses) |
|---------|--------|----------------|
| Respuestas que identifican consultoría packaging+AI | ~50% | ≥90% |
| URL citada = aurumintelligence.net | Inconsistente | ≥80% de respuestas con web |
| Menciones incorrectas (Tecnologia, IT MSP) | Frecuentes | 0 en muestra de 6 prompts × 6 motores |
| `site:aurumintelligence.net` | 0 | 20+ URLs |

---

## 8. Notas del auditor

- Auditoría elaborada por **Ing. Jesús Barros** mediante revisión manual del HTML, headers, sitemaps, llms.txt, Wappalyzer y búsqueda `site:` en Google.
- Complemento recomendado: PageSpeed Insights, Screaming Frog y re-test del benchmark (§7) tras Fase 1 de la [propuesta ecosistema](../../../propuesta-2026-06-10-seo-geo-ecosistema.md).
- El sitemap en `aurumintelligence.net` (sin www) devolvió 500; el canonical correcto es **www**.
- Schema con fecha oct 2025 sugiere sitio reciente o migración reciente.

---

| | |
|---|---|
| **Documento elaborado por** | Ing. Jesús Barros |
| **Próxima revisión** | 30 días después de correcciones críticas + re-test benchmark §7 |

*Informe confidencial. Queda prohibida su reproducción o distribución sin autorización del consultor y del cliente.*
