# AGENTS.md — contexto para agentes de IA

## O que é este projeto

Blog pessoal estático de Leonardo Calvet, publicado em `https://blog.calvet.dev.br`.

- **Gerador:** Jekyll · **Tema:** Beautiful Jekyll (MIT — manter o `LICENSE`) · **Cores:** paleta [Flexoki](https://stephango.com/flexoki), variante light (aplicada no `_config.yml` + `assets/css/flexoki.css`; dark mode é TODO)
- **Repo:** `github.com/LeoCalvet/blog` (público) · **Língua do conteúdo:** pt-BR
- **Sem banco, sem segredos, sem `.env`** — 100% do site vive neste repo. O checkout deste repo É a pasta da aplicação no notebook (`~/Projetos/home_server_apps/blog`).

## Como funciona o deploy — LEIA ANTES DE PUSH

`git push` em `main` **publica de verdade no site**:

```text
push em main → GitHub Actions (runner self-hosted no notebook pop-os-laptop)
  → jekyll build em container ruby:3.3
  → rsync _site/ → ./site/ (servido pelo nginx, 127.0.0.1:8095)
  → Cloudflare Tunnel → https://blog.calvet.dev.br
```

- **Commitar não publica; push em `main` sim.** Só faça push quando a publicação for desejada.
- Não existe staging. Preview local é o "staging" (comando abaixo). Valide o build antes de push que mexa em tema/config.
- Não rode deploy manual (rsync/docker build direto na pasta `site/`) — o pipeline é o único caminho de publicação.

## O que o agente PODE fazer

- Escrever/editar posts em `_posts/` e rascunhos em `_drafts/`
- Editar `sobre.md`, `index.html`, `404.html`, `tags.html`
- Ajustar `_config.yml` (título, navbar, cores, plugins)
- Ajustar `assets/` (CSS Flexoki, imagens, JS)
- Rodar preview/build local para validar

## O que o agente NÃO deve fazer

- NÃO editar `site/` nem `_site/` — artefatos de build; `site/` é sobrescrito pelo pipeline a cada deploy
- NÃO mudar `compose.yaml` ou `nginx/` sem dizer que mudou: exige `docker compose up -d` no notebook pra valer
- NÃO introduzir segredos, tokens ou chaves no repo
- NÃO criar post com data no futuro — Jekyll não publica post datado à frente do relógio
- NÃO substituir arquivos do tema (`_layouts/`, `_includes/`) sem necessidade — o padrão é sobrescrever por cima (cópia do arquivo + ajuste), mantendo fácil o diff com o upstream

## Convenções

- Post: `_posts/YYYY-MM-DD-slug.md`, front matter mínimo:

  ```yaml
  ---
  title: "Título"
  date: 2026-08-30 18:00:00 -0300
  categories: [categoria]
  tags: [tag1, tag2]
  ---
  ```

- Permalink: `/:year/:month/:day/:slug/` · Timezone: `America/Sao_Paulo` · `lang: pt-BR`
- Data de exibição: `date_format: "%d/%m/%Y"`
- Commits com prefixo: `post:` (conteúdo), `fix:` (correção), `config:` (tema/infra)
- `AGENTS.md`, `README.md`, `compose.yaml`, `nginx/`, `LICENSE` estão no `exclude` do Jekyll — não vão pro site publicado

## Preview e build local

```bash
# preview (rebuild automático) — http://localhost:4000
docker run --rm --user "$(id -u):$(id -g)" -e BUNDLE_PATH=/tmp/bundle \
  -v "$PWD:/site" -w /site -p 4000:4000 \
  ruby:3.3 sh -c "bundle install && bundle exec jekyll serve --host 0.0.0.0"

# validar build (mesmo comando do pipeline)
docker run --rm --user "$(id -u):$(id -g)" -e BUNDLE_PATH=/tmp/bundle \
  -v "$PWD:/site" -w /site \
  ruby:3.3 sh -c "bundle install --quiet && bundle exec jekyll build"
```

## Fora do repo (infra do notebook — não editar via git)

- **Runner do Actions:** `~/actions-runner`, serviço de usuário `github-runner-blog.service` (`systemctl --user status github-runner-blog`)
- **nginx/containers:** `docker compose` nesta pasta (container `home-server-blog-web`, porta loopback 8095)
- **Rota pública:** `blog.calvet.dev.br` → `HTTP localhost:8095` no túnel `home-server-laptop` (Cloudflare Zero Trust — só o Leonardo tem acesso ao painel)
