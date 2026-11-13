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
| `/medicos` | LP de Médicos — projeto Vercel `digital7-medicos` |
| `/mercado-digital` | LP de Mercado Digital — projeto Vercel `digital7-mercado-digital` |
| `/dentistas` | LP de Dentistas — projeto Vercel `digital7-dentistas` (zona com prefixo `/dentistas/`) |

Como funciona a integração (`vercel.json` — proxy por `rewrites`, a URL do domínio é preservada):

| Rota no domínio | Encaminha para | Por quê |
|---|---|---|
| `/medicos` | `digital7-medicos.vercel.app/` | página da LP |
| `/medicos/*` | `digital7-medicos.vercel.app/*` | assets relativos da LP |
| `/dentistas/` | `digital7-dentistas.vercel.app/` | página da LP (zona isolada por prefixo) |
| `/dentistas/*` | `digital7-dentistas.vercel.app/*` | assets relativos da LP |
| `/mercado-digital` | `digital7-mercado-digital.vercel.app/` | página da LP |
| `/mercado-digital/*` | `digital7-mercado-digital.vercel.app/*` | assets relativos da LP |
| `/assets/*` | `digital7-medicos.vercel.app/assets/*` | assets relativos de Médicos |
| `/assets/images/*` | `digital7-mercado-digital.vercel.app/assets/images/*` | imagens de Mercado Digital (regra mais específica, avaliada antes) |
| `/css/*`, `/js/*` | `digital7-mercado-digital.vercel.app/...` | CSS/JS de Mercado Digital |

- Arquivos locais do site **têm prioridade** sobre os rewrites (ex.: `/assets/favicon-*.png`, `/assets/logotipo-digital-7.png`, `/favicon.ico`)
- `/medicos/` e `/mercado-digital/` (com barra) → **308** para a versão sem barra, garantindo URL única
- Para publicar mudanças em qualquer LP, basta fazer deploy no projeto Vercel correspondente

## Próximos passos

Os botões **Mercado Digital** (`/mercado-digital`) e **Médicos** (`/medicos`) já apontam para as LPs.
Falta o botão **Dentistas**, que continua como âncora provisória (`#dentistas`) até a LP ser publicada
em um projeto Vercel — aí é só adicionar as regras no `vercel.json` no mesmo padrão.