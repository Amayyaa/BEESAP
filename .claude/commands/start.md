---
description: Começa uma sessão no site da BEESAP — atualiza o repositório, lê as regras e mostra o estado do projeto
argument-hint: [o que queres fazer hoje, opcional]
---

Começa esta sessão a conhecer bem o projeto e depois ajuda o utilizador a escolher o próximo passo. Nota opcional do utilizador: $ARGUMENTS

Fala com o utilizador em português, de forma breve e simpática. Corre os comandos só de leitura sem perguntar.

## 1. Ferramentas
- `gh auth status` tem de funcionar. Se falhar, pede ao utilizador `! gh auth login` e para.
- Se já existir `site/package.json`: `node --version` (≥ 22).

## 2. Atualizar o código
- `git status --porcelain` e `git branch --show-current`.
- Em `main`, sem alterações: `git pull --ff-only`.
- Noutro ramo: é trabalho em curso. Faz `git fetch origin` e diz quantos commits está atrás (`git rev-list --count HEAD..origin/main`). Não faças merge sem perguntar.
- Se houver alterações por guardar, lista-as e não lhes toques.
- Se existir `site/package.json` e `site/node_modules` faltar ou o lockfile tiver mudado: `npm install` em `site/`.

## 3. Ler as regras
- Lê **todo** o `AGENTS.md`, que é a fonte de verdade. Repara na tabela "Estado do projeto" (§0).
- Vê rapidamente `conteudo/mapa-do-site.md` e o que existe em `conteudo/` e em `design/`.
- Verifica se `design/` já tem o desenho da responsável (imagens ou PDF). Se sim e se o site ainda não foi começado, esse é o próximo grande passo.

## 4. Estado no GitHub (resume, não mostres a saída em bruto)
- `gh pr list --state open --json number,title,author,headRefName,statusCheckRollup,url`
- `gh issue list --state open --json number,title,assignees,url --limit 50`
- `git log origin/main --oneline -10`
- `gh run list --branch main -L 3`: confirma se a última publicação correu bem.

## 5. Relatório e sugestão
Resumo curto:
- **Fase atual** (da tabela §0) e o que falta para a próxima.
- **Publicação:** OK ou não.
- **PRs e issues abertos**, uma linha cada.
- **Este computador:** ramo atual e alterações pendentes.
- **Pendentes com a biblioteca:** os TODO em `conteudo/` (`grep -rn "TODO" conteudo/`).

Depois sugere um passo:
- Para criar ou rever uma secção do site: `/nova-seccao <id> "<objetivo>"`.
- Para terminar e publicar o trabalho atual: `/publicar`.
- Se o utilizador deu uma nota, usa-a para escolher a sugestão.
