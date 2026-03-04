# SolarWatson — Embed instructies

## Stap 1: Deploy index.html

Upload `index.html` naar een van deze opties:

### Optie A: Vercel (gratis, aanbevolen)
1. Maak een account op vercel.com
2. Maak een nieuwe map met alleen `index.html`
3. Sleep de map naar het Vercel dashboard
4. Kies een custom domain: `check.zonhub.com`
   - Voeg in je DNS een CNAME toe: `check` → `cname.vercel-dns.com`

### Optie B: Netlify (gratis)
1. Ga naar netlify.com → "Deploy manually"
2. Sleep de map met `index.html` naar het drop-zone
3. Stel custom domain in: `check.zonhub.com`

### Optie C: Eigen server
Upload `index.html` naar `/var/www/check/index.html` en configureer nginx/Apache.

---

## Stap 2: Embed via iframe in je CMS

Plak dit in het **Raw HTML** blok in je CMS:

```html
<iframe
  src="https://check.zonhub.com"
  width="100%"
  height="800"
  frameborder="0"
  scrolling="no"
  style="border:none; width:100%; min-height:800px;"
  title="SolarWatson — Prestatie Check">
</iframe>

<script>
  // Auto-resize iframe aan content hoogte
  window.addEventListener('message', function(e) {
    if (e.data && e.data.type === 'resize') {
      var iframe = document.querySelector('iframe[title="SolarWatson — Prestatie Check"]');
      if (iframe) iframe.style.height = e.data.height + 'px';
    }
  });
</script>
```

### Vaste hoogte (eenvoudiger, zonder auto-resize):
```html
<iframe
  src="https://check.zonhub.com"
  width="100%"
  height="900"
  frameborder="0"
  style="border:none; width:100%;"
  title="SolarWatson — Prestatie Check">
</iframe>
```

---

## Stap 3: DNS instelling (voor check.zonhub.com)

Bij je DNS-provider (bijv. Cloudflare, TransIP, Antagonist):

| Type  | Naam  | Waarde                  |
|-------|-------|-------------------------|
| CNAME | check | cname.vercel-dns.com    |

(Waarde verschilt per hostingprovider — zie hun documentatie)

---

## Notities

- De tool werkt volledig client-side: geen server, geen database nodig
- KNMI-data is ingebakken (t/m maart 2026) — update het JSX-bestand voor nieuwe periodes
- De tool werkt op mobiel en desktop
