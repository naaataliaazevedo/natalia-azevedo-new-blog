# natazevedo.com.br — blog

Site do blog em Astro, com estética "terminal" (dark mode + monospace).

## Rodando localmente

```bash
npm install
npm run dev
```

Abra http://localhost:4321

## Adicionando um post novo

Crie um arquivo em `src/content/posts/meu-post.md`:

```md
---
title: "Título do post"
description: "Resumo de 1-2 linhas pro SEO e pra listagem."
date: 2026-09-13
tags: ["frontend", "n8n"]
draft: false
---

Conteúdo do post em Markdown normal.
```

Enquanto `draft: true`, o post não aparece no site — útil pra escrever
com calma antes de publicar.

Tem um post de exemplo em `src/content/posts/migrando-legado-para-microfrontends.md`
(está com `draft: true`) — edite-o ou apague-o pra começar do zero.

## Estrutura

- `src/layouts/BaseLayout.astro` — layout base (header, footer)
- `src/components/PostRow.astro` — linha de post nas listagens
- `src/pages/index.astro` — home
- `src/pages/blog/` — listagem e página de post
- `src/pages/sobre/` — sobre
- `src/pages/servicos/` — serviços da software house
- `src/styles/global.css` — tokens de cor/tipografia, tudo centralizado aqui

## Build e deploy

```bash
npm run build
```

Gera a pasta `dist/` — pode subir direto pra Netlify, Vercel ou
GitHub Pages (é tudo estático). Se for reaproveitar o domínio
natazevedo.com.br que já existe no Netlify, é só apontar o novo
build command (`npm run build`) e publish dir (`dist`).
