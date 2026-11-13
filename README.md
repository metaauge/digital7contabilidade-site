# Digital 7 — Contabilidade & Coworking Virtual

**Site no ar:** https://digital7contabilidade.com.br
(`www.digital7contabilidade.com.br` redireciona 308 para o domínio principal)

Landing page institucional da **Digital 7**, com a identidade visual da marca
(logotipo como favicon) e três chamadas por segmento de atendimento.

**Domínio/DNS:** registrado e gerenciado na Hostinger (`apollo/athena.dns-parking.com`).
Registros apontando para a Vercel:

```
A      @     216.198.79.1
A      @     64.29.17.1
CNAME  www   beb7edd9b4baec28.vercel-dns-017.com
```

**Hospedagem:** Vercel (projeto `digital7contabilidade-site`), deploy automático a cada
`git push` na `main`. Espelho em GitHub Pages: https://metaauge.github.io/digital7contabilidade-site/

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

## Rotas

| Rota | Conteúdo |
|---|---|
| `/` | Landing principal da Digital 7 (logo + 3 botões) |
| `/medicos` | LP de Médicos, servida via `rewrites` do projeto Vercel `digital7-medicos` |

Como funciona a integração (`vercel.json`):

- `/medicos` → proxy para `https://digital7-medicos.vercel.app/` (URL do domínio é preservada)
- `/medicos/*` → proxy para o mesmo projeto (assets da LP em caminho relativo)
- `/assets/*` → proxy para o mesmo projeto (a LP referencia `/assets/images/...` dentro do CSS);
  arquivos locais do site têm prioridade (ex.: `/assets/favicon-*.png`)
- `/medicos/` → redirect 308 para `/medicos`

> Para publicar mudanças na LP de Médicos, basta fazer deploy no projeto `digital7-medicos`
> — este site continua apontando para o domínio de produção dele.

## Próximos passos

Os três botões usam âncoras provisórias (`#mercado-digital`, `#medicos`, `#dentistas`).
Quando as páginas/landing de cada segmento estiverem prontas, basta trocar o `href`
de cada `.btn` no `index.html` (por exemplo `href="mercado-digital.html"`).