---
description: Termina o trabalho do ramo atual — verifica tudo, atualiza o PR e diz se está pronto para publicar
---

Prepara o ramo atual para publicação. Fala em português, de forma breve.

1. `git branch --show-current`. Se for `main`, para: o trabalho tem de estar num ramo.
2. `git fetch origin` e `git rebase origin/main`. Se houver conflitos, para e explica-os.
3. Lê o `AGENTS.md` e repete as verificações do passo 5 do `/nova-seccao`:
   - build sem erros (se `site/` existir);
   - `arquivo/` intacto (`git diff origin/main --stat -- arquivo/` vazio);
   - sem pt-BR, todas as imagens com `alt`, sem dados pessoais nem segredos.
4. Commit do que faltar e `git push` (usa `--force-with-lease` só depois de um rebase).
5. Se não houver PR, cria-o (formato do `/nova-seccao` §6). Se houver, atualiza a descrição.
6. Se houver CI: `gh pr checks --watch`. Lê os erros com `gh run view <id> --log-failed`, corrige e repete até ficar verde.
7. Relatório:
   - link do PR;
   - estado das verificações;
   - TODO ainda por confirmar com a biblioteca;
   - "pronto para merge (= publicar)" ou o que falta.
