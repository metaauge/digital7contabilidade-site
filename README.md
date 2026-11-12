# Digital 7 — Contabilidade & Coworking Virtual

**Sites publicados:**
- Vercel (principal): https://digital7contabilidade-site.vercel.app
- GitHub Pages (espelho): https://metaauge.github.io/digital7contabilidade-site/

Landing page institucional da **Digital 7**, com a identidade visual da marca
(logotipo como favicon) e três chamadas por segmento de atendimento.

## Estrutura

```
index.html                  página única (HTML + CSS + JS inline)
favicon.ico                 favicon 16px + 32px (raiz do site)
assets/
  logotipo-digital-7.png    logotipo (fundo transparente, recortado)
  favicon-512x512.png       favicon (símbolo D7) 512px
  favicon-192x192.png       favicon 192px
  favicon-32x32.png         favicon 32px
  favicon-16x16.png         favicon 16px
  apple-touch-icon.png      ícone iOS 180px
```

## Como visualizar localmente

Basta abrir o `index.html` no navegador, ou servir a pasta:

```powershell
python -m http.server 8000
# http://localhost:8000
```

## Como publicar

O site é 100% estático e está publicado em dois lugares:

- **Vercel** (`digital7contabilidade-site` → alias `https://digital7contabilidade-site.vercel.app`),
  com deploy automático a cada `git push` na branch `main`.
- **GitHub Pages** (branch `main`, pasta raiz `/`).

## Próximos passos

Os três botões usam âncoras provisórias (`#mercado-digital`, `#medicos`, `#dentistas`).
Quando as páginas/landing de cada segmento estiverem prontas, basta trocar o `href`
de cada `.btn` no `index.html` (por exemplo `href="mercado-digital.html"`).