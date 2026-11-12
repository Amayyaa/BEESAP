---
description: Cria (ou refaz) uma secção do site da BEESAP — conteúdo, página e PR
argument-hint: <id> "<objetivo>"
---

Cria uma secção do site da BEESAP de ponta a ponta e abre um PR.

Argumentos: $ARGUMENTS. A primeira palavra é o id da secção (ex.: `noticias`, `projetos`, `horario`). O resto, entre aspas, é o objetivo: o que a secção mostra e para quem. Se o objetivo faltar ou for vago demais, faz uma pergunta curta e continua.

Segue os passos por ordem e não saltes verificações. Fala com o utilizador em português. Escreve o texto do site em pt-PT e o código e os commits em inglês.

## 1. Partir do zero
- `git status --porcelain` tem de estar vazio. Se não estiver, para e pergunta o que fazer. Nunca descartes alterações.
- `git switch main && git pull --ff-only`.
- Id em kebab-case, minúsculas, sem acentos (`Bancos de imagens` → `bancos-de-imagens`).
- Confirma que não existe o ramo remoto: `git ls-remote --heads origin feat/<id>`.
- `git switch -c feat/<id>`.
- Se houver uma issue correspondente (`gh issue list --search "<id>"`), anota o número para `Closes #N`.

## 2. Ler
- Lê todo o `AGENTS.md`. Se este ficheiro discordar dele, segue o `AGENTS.md`.
- Lê `conteudo/mapa-do-site.md` para ver onde a secção encaixa.
- Encontra o conteúdo de origem em `arquivo/` (`grep -rli "<palavra>" arquivo/google-sites arquivo/webnode`).
- Se já existir: `design/` (o desenho) e uma secção de referência em `site/`, para copiares o padrão.

## 3. Planear (curto)
Escreve 4 a 8 linhas para o utilizador:
- de onde vem o conteúdo (que ficheiros do arquivo);
- que ficheiros vais criar em `conteudo/` (e em `site/`, se o site já existir);
- como a responsável vai atualizar esta secção no futuro (tem de ser simples);
- o que falta confirmar com a biblioteca.

Prefere a versão mais pequena que cumpre o objetivo. Só paras para perguntar se a decisão muda o que o público vê.

## 4. Construir
- **Conteúdo:** cria ou atualiza os `.md` em `conteudo/` no formato do `AGENTS.md` §5. Revê o texto vindo do arquivo:
  - corrige gralhas e linguagem pt-BR;
  - mantém o sentido;
  - marca o que for duvidoso com `<!-- TODO: confirmar com a biblioteca -->`.
- **Imagens:** copia do `arquivo/imagens/` para junto do conteúdo, converte para WebP (≤ 1600 px, ~300 KB) e escreve sempre um `alt` descritivo. Nunca alteres o `arquivo/`.
- **Página:** só se o site já existir (fase 4 do `AGENTS.md` §0). Segue o design de `design/` e a secção de referência. Não acrescentes bibliotecas novas.
- Se a secção for nova, acrescenta-a ao `conteudo/mapa-do-site.md`.

## 5. Verificar
- Se o site existir: `npm run build` em `site/` sem erros nem avisos. Abre localmente e vê-o com 390 px e em computador.
- Revê o teu diff (`git diff main --stat` e depois completo):
  - nada dentro de `arquivo/` foi alterado;
  - não há pt-BR (tabela de vocabulário);
  - todas as imagens têm `alt`;
  - não há nomes de alunos com fotos sem confirmação, emails pessoais nem segredos;
  - não há texto inventado.

## 6. Commit, push e PR
- Commit curto em inglês: `feat(<id>): …` ou `content(<id>): …`.
- `git push -u origin feat/<id>`.
- `gh pr create --base main --title "<Secção>: <resumo>"`. O corpo é em pt-PT e curto:
  - **O que muda** (2 a 4 pontos)
  - **De onde veio o conteúdo**
  - **Por confirmar com a biblioteca** (os TODO)
  - **Como verificar**
  - `Closes #N`, se aplicável
- Se houver CI: `gh pr checks --watch`, corrige até ficar verde.

## 7. Relatório
Diz brevemente ao utilizador:
- o que foi feito;
- o link do PR;
- o que deve perguntar à senhora da biblioteca;
- que o merge publica o site.
