# BEESAP — regras para cada sessão de trabalho

Novo site da **Biblioteca Escolar da Escola Secundária Adolfo Portela (BEESAP)**, em Águeda. Substitui dois sites antigos:

- Google Site `sites.google.com/view/beesap`, com recursos e informações. A conta Google ficou sem espaço e o acesso perdeu-se.
- Webnode `ler-o-mundo-na-beesap.webnode.pt`, com notícias e projetos.

**Para quem é:** alunos do 3.º ciclo e do secundário, professores e famílias. Quem vai **manter** o site é a professora bibliotecária, que não tem experiência em informática. Tudo o que fizermos tem de lhe ser fácil de usar. Este é o critério mais importante de todas as decisões.

Lê este ficheiro com atenção antes de mudar seja o que for.

## 0. Estado do projeto

| Fase | Estado |
|---|---|
| 1. Arquivo dos sites antigos (`arquivo/`) | feito (2026-11-12) |
| 2. Conteúdo organizado para o novo site (`conteudo/`) | em curso |
| 3. Design: desenho à mão da responsável (`design/`) | **à espera do desenho** |
| 4. Construção do site (`site/`) | não começou: não escrever código de site antes do design |
| 5. Editor simples para a responsável + publicação | não começou |

Atualiza esta tabela sempre que uma fase muda.

## 1. Regras de ouro

1. **Texto do site em português europeu (pt-PT).** Fala com os alunos por "tu", como nos sites antigos ("Inscreve-te", "Procura o livro"). Nunca uses português do Brasil (ver vocabulário abaixo). Código, nomes de ficheiros técnicos, comentários e mensagens de commit são em inglês. Conversa com o utilizador em português.
2. **Simplicidade acima de tudo.** O menu tem no máximo 6 entradas. Os botões são grandes e as frases curtas. Nada de menus escondidos dentro de menus. Se uma funcionalidade obrigar a responsável a aprender algo técnico, procura outra solução.
3. **Não inventar conteúdo.** Os textos, nomes, datas e horários vêm de `arquivo/` ou da responsável. Se faltar alguma coisa, deixa `<!-- TODO: confirmar com a biblioteca -->` e pergunta. Nunca preenchas com texto inventado.
4. **O design é da responsável.** Enquanto `design/` não tiver o desenho dela, não escolhas cores, tipos de letra nem layout final. Quando o desenho chegar, segue-o fielmente. Só o adaptas para telemóvel e para acessibilidade, e explicas cada adaptação.
5. **Proteção de dados (RGPD).** Os alunos são menores. Não publiques nomes completos de alunos juntamente com fotografias sem confirmação da responsável. Não publiques emails pessoais nem números de telefone pessoais. O contacto público é `beesap@esap.edu.pt` e o telefone da escola é 234 623 808.
6. **Sem segredos no repositório.** Nada de palavras-passe, tokens ou ficheiros `.env`.
7. **Uma mudança = um ramo = um PR para `main`.** `main` é o que está publicado. Nunca faças push direto para `main` depois de o site estar no ar.
8. **Nunca apagar o arquivo.** `arquivo/` é só para leitura. Serve de referência histórica e nunca é editado. Corrige o conteúdo em `conteudo/`.

### Vocabulário pt-PT

| ✅ usar | ❌ evitar |
|---|---|
| ecrã | tela |
| telemóvel | celular |
| utilizador | usuário |
| guardar | salvar |
| apagar | deletar |
| partilhar | compartilhar |
| ficheiro | arquivo (no sentido de *file*) |
| transferir | baixar |
| equipa | time |
| inscreve-te / consulta | inscreva-se / consulte (no tom "tu") |
| "A carregar…" | "Carregando…" |

Datas escritas assim: "15 de janeiro de 2025", com meses e dias da semana em minúscula. Horas assim: 08h30–17h00.

## 2. Mapa do repositório

```
AGENTS.md                ← estas regras (a fonte de verdade)
CLAUDE.md                ← aponta para AGENTS.md
README.md                ← o que é o projeto, para humanos
.claude/commands/        ← /start, /nova-seccao, /publicar
arquivo/                 ← cópia fiel dos sites antigos (NÃO editar)
  LEIA-ME.md             ← índice e avisos (links no OneDrive que podem desaparecer)
  google-sites/*.md      ← texto completo de cada página
  webnode/*.md           ← idem, incluindo artigos (artigo-*.md)
  imagens/<site>/<pagina>/  ← todas as imagens descarregadas
  html-original/         ← HTML bruto, por segurança
conteudo/                ← conteúdo revisto e organizado para o novo site
  informacoes.md         ← contactos, horário, equipa, missão
  mapa-do-site.md        ← menu do novo site e origem de cada secção
  noticias/ projetos/ recursos/
design/                  ← desenho(s) da responsável e decisões de design
site/                    ← código do site (vazio até haver design)
```

## 3. Tecnologia (proposta: confirmar quando chegar o design)

- **Site estático** (HTML/CSS, gerado a partir de Markdown), alojado gratuitamente no **GitHub Pages**. Não tem servidor nem base de dados, e não depende de contas pessoais. É exatamente o problema que se quer evitar desta vez.
- **Gerador proposto:** Astro, porque o conteúdo vem de ficheiros `.md` em `conteudo/`.
- **Edição pela responsável:** um editor visual que grava no GitHub, como o Pages CMS ou o Decap CMS. Com ele, a responsável escreve uma notícia num formulário, anexa fotos e carrega em "Publicar", sem ver código.
- **Conta:** o repositório e o alojamento devem ficar numa conta **da escola** ou com pelo menos duas pessoas com acesso, para nunca mais se perder o site por causa de uma conta.
- Nada de bibliotecas pesadas, nem de serviços pagos ou que exijam conta pessoal da responsável.

Quando a tecnologia for decidida, atualiza esta secção e acrescenta os comandos (`npm run dev`, `npm run build`, …).

## 4. Requisitos do site

- **Telemóvel primeiro.** Desenha primeiro para 390 px de largura e depois para computador. Alvos de toque com pelo menos 44 px. Texto do corpo com pelo menos 16 px.
- **Acessibilidade (WCAG AA):** contraste suficiente, `alt` descritivo em todas as imagens, títulos em ordem (h1 → h2 → h3), o site tem de funcionar só com teclado e as ligações têm de dizer para onde vão (nunca "clica aqui").
- **Rápido:** as imagens são comprimidas (WebP, no máximo ~300 KB, largura máxima de 1600 px). Os vídeos ficam no YouTube e não no repositório.
- **Links externos** abrem no mesmo separador, exceto documentos (PDF) e o catálogo.
- **Informação essencial sempre visível no rodapé:** morada, telefone, email, horário e um link para o site da escola (esap.edu.pt).
- **Sem cookies nem rastreadores.** Se for preciso medir visitas, usa uma solução sem cookies e pergunta antes.

## 5. Conteúdo

**Dados confirmados (dos sites antigos):**

- Morada: Rua Joaquim Valente Almeida, 242, 3750-154 Águeda
- Coordenadas: 40.583714, -8.447813
- Telefone: 234 623 808. Email: beesap@esap.edu.pt
- Horário: segunda, terça e quinta 08h30–17h00; quarta 08h30–16h00; sexta 08h30–13h00
- Instagram @na_beesap. Facebook: perfil BEESAP. Catálogo: rede de bibliotecas de Águeda (bibliopolis)

**A confirmar com a responsável** (marcar com TODO até haver resposta):

- Equipa atual: os dois sites antigos não coincidem.
- Horário deste ano letivo.
- Que notícias e projetos antigos ficam no novo site.
- Os ficheiros que hoje estão no OneDrive pessoal de Regina Gaspar (ver `arquivo/LEIA-ME.md`).

**Formato de uma notícia** (`conteudo/noticias/AAAA-MM-DD-titulo-curto.md`):

```markdown
---
titulo: Workshop de Literacia da Informação
data: 2024-06-07
resumo: Os alunos do 12.º ano aprenderam a citar e referenciar com a norma APA.
imagem: ./imagens/2024-06-07-workshop.webp
imagem_alt: Alunos sentados na biblioteca a ouvir a apresentação
---

Texto da notícia…
```

Os projetos (`conteudo/projetos/<id>.md`) e os recursos (`conteudo/recursos/<id>.md`) seguem o mesmo esquema: cabeçalho com `titulo` e `resumo`, seguido do texto.

**Ids:** em português, minúsculas, sem acentos e com hífens (`newton-gostava-de-ler`, `bancos-de-imagens`). O id dá o nome ao ficheiro, ao URL e à pasta das imagens.

## 6. Fluxo de trabalho (Git)

1. No início de cada sessão: `/start`.
2. Ramo por mudança: `feat/<id>` para coisas novas, `content/<id>` para conteúdo, `fix/<o-que>` para correções.
3. Antes de abrir o PR: o site compila sem erros (quando existir), não há texto em pt-BR, todas as imagens têm `alt` e não há dados pessoais nem segredos.
4. PR para `main` com uma descrição curta em pt-PT: o que muda, porquê e como verificar.
5. Merge = publicação. Revê sempre o site publicado no telemóvel.
6. Commits curtos em inglês, por exemplo `content(noticias): add 2024 reading contest`.
7. Não reformates ficheiros em que não mexeste. Um PR trata de um só assunto.

Sessões em paralelo no mesmo PC precisam de pastas diferentes: `git worktree add ../beesap-<id> -b feat/<id> origin/main`.
