# Plantium — Landing Page

Sito statico 1-pagina per Plantium (Manutenzione + Produzione).

Stack: HTML + CSS puro. Nessun build step, nessun framework.

## Struttura

```
plantium-landing/
├── index.html             ← landing principale
├── style.css              ← stile minimale
├── robots.txt             ← SEO
├── sitemap.xml            ← SEO
├── manuali/
│   ├── Manuale_Manutenzione.pdf
│   └── Manuale_Produzione.pdf
└── README.md
```

## Test in locale

Apri `index.html` nel browser, oppure server statico:

```bash
# Python
python -m http.server 8080

# Node
npx serve .
```

## Deploy su GitHub Pages

1. Crea repo `plantium-landing` su GitHub e pusha questi file
2. Vai su **Settings → Pages**
3. **Source**: `Deploy from a branch`
4. **Branch**: `main`, folder `/ (root)`
5. Salva → URL temporaneo: `https://<username>.github.io/plantium-landing/`

### Custom domain (es. plantium.it)

1. Registra `plantium.it` (Aruba / Cloudflare / Namecheap, ~15€/anno)
2. Su GitHub Pages settings: aggiungi `plantium.it` come custom domain
3. Sul DNS del registrar:
   - Record A → `185.199.108.153`
   - Record A → `185.199.109.153`
   - Record A → `185.199.110.153`
   - Record A → `185.199.111.153`
   - Record CNAME `www` → `<username>.github.io`
4. Attendi propagazione DNS (10 min - 24h)
5. GitHub Pages settings: spunta `Enforce HTTPS`

## Deploy alternative

- **Cloudflare Pages**: connetti repo → build command vuoto → publish dir `/`
- **Netlify**: drag&drop della cartella o connetti repo
- **Aruba/SiteGround**: upload via FTP nella public_html

## Branding

Colori dei due moduli (usati anche nei bottoni e nelle card):

- **Manutenzione**: viola → `linear-gradient(135deg, #8b5cf6, #4f46e5)`
- **Produzione**: arancione fuoco → `linear-gradient(135deg, #fb923c, #ea580c)`
- Brand mark Plantium: `linear-gradient(135deg, #1e293b, #334155)`
- Accent gradient hero: viola + arancione fuoco

## SEO incluso

- `<title>` + `<meta description>` + `<meta keywords>` IT
- Open Graph (Facebook, WhatsApp link preview)
- Twitter Card
- Schema.org JSON-LD `SoftwareApplication`
- `<link rel="canonical">`
- `robots.txt` + `sitemap.xml`
- `theme-color` per browser mobile
- `preconnect` agli hostname app per caricamento più veloce dei link

## TODO post-deploy

- [ ] Sostituire `info@plantium.it` con email reale nel footer e nel link contatti
- [ ] Sostituire i placeholder `https://plantium.it` in `sitemap.xml`, `robots.txt`, `<link rel="canonical">`, og:url, og:image col dominio scelto
- [ ] Generare immagine `assets/og-image.png` 1200×630 px per anteprime social (placeholder ora)
- [ ] Endpoint pubblico `/api/public/stats` su una delle due app per riempire i contatori reali
- [ ] Sostituire il `<script>` JS finale in `index.html` con la chiamata a quell'endpoint
- [ ] Aggiungere Google Search Console + Cloudflare Analytics (o Plausible)
- [ ] Aggiungere pagina `/installa-app` (PWA add-to-home iOS/Android) quando pronto
- [ ] Verificare il sito su PageSpeed Insights e correggere eventuali warning Core Web Vitals

## Aggiornamento dei manuali

I PDF in `manuali/` sono copie di quelli generati nei progetti app. Per
rigenerarli ed aggiornare:

```bash
cd ../plant-manutenzione\ v3 && node scripts/genera-manuale.mjs
cp docs/Manuale_Utente.pdf ../plantium-landing/manuali/Manuale_Manutenzione.pdf

cd ../plant-produzione\ v3 && node scripts/genera-manuale.mjs
cp docs/Manuale_Utente.pdf ../plantium-landing/manuali/Manuale_Produzione.pdf
```

Poi commit + push.
