# blog — blog.calvet.dev.br

Blog estático em Jekyll com o tema [Hitchens](https://github.com/patdryburgh/hitchens), paleta de cores [Flexoki](https://stephango.com/flexoki) e a fonte CaskaydiaCove Nerd Font.

## Como funciona

```text
.md no repo → git push (main) → GitHub Actions (runner self-hosted no notebook)
            → jekyll build → rsync _site/ → nginx (127.0.0.1:8095) → Cloudflare Tunnel
```

- **Conteúdo:** posts em `_posts/` com nome `YYYY-MM-DD-titulo.md`. Rascunhos em `_drafts/` (não entram no build normal).
- **Servidor:** `compose.yaml` sobe um `nginx:alpine` na porta loopback 8095 servindo `./site/` (gerado pelo build).
- **Deploy:** `.github/workflows/deploy.yml` roda no runner self-hosted do notebook a cada push em `main`.

## Rodar local (preview)

```bash
docker run --rm --user "$(id -u):$(id -g)" -e BUNDLE_PATH=/tmp/bundle \
  -v "$PWD:/site" -w /site -p 4000:4000 \
  ruby:3.3 sh -c "bundle install && bundle exec jekyll serve --host 0.0.0.0"
# http://localhost:4000
```

## Subir o servidor

```bash
docker compose up -d   # serve ./site/ (populado pelo build/deploy)
```

## Rota pública

`blog.calvet.dev.br` → `http://localhost:8095` no Cloudflare Tunnel (painel do túnel `home-server-laptop`).
