# Instruções para agentes — TCC

Este arquivo vale para qualquer agente de IA (Claude Code ou outro) que edite este repositório. Regras específicas de escrita e estrutura da monografia — leia antes de criar ou editar qualquer `.tex`.

## Sobre o projeto

Monografia de TCC (IFPB Campus Campina Grande, Tecnologia em Telemática). Tema: implementação e validação de uma máquina virtual de lógica Ladder agnóstica de hardware baseada em Model-Based Design. Orientador: Fagner de Araújo Pereira. Escrita em LaTeX com abnTeX2 (classe `book` + `abntex2cite`).

## Estrutura de arquivos

- `main.tex` — arquivo raiz e único ponto de compilação: `\documentclass` + `\input{preambulo}` + corpo do documento (capa, elementos pré-textuais, `\input`/`\include` dos capítulos e apêndices, bibliografia). É o único arquivo com `\begin{document}`/`\end{document}`.
- `preambulo.tex` — pacotes, macros, configuração de listings e do estilo de citação ABNT. **Não alterar sem o usuário pedir explicitamente** — mudanças aqui afetam o documento inteiro e já foram validadas com uma compilação completa.
- `referencias.bib` — banco de referências bibliográficas, estilo `abntex2-alf`.
- `capitulos/NN-nome.tex` — um arquivo por capítulo do corpo principal, numerado (`01-`, `02-`, ...), incluído em `main.tex` via `\input{capitulos/NN-nome}`.
- `apendices/NN-nome.tex` — mesmo padrão, para apêndices, incluído via `\include{apendices/NN-nome}`.
- `figuras/` — imagens, referenciadas sem caminho nem extensão (`\graphicspath{{./figuras/}}` já configurado no preâmbulo).
- Todo arquivo dentro de `capitulos/` e `apendices/` deve começar com `% !TeX root = ../main.tex` (permite compilar a partir de qualquer capítulo aberto no editor).
- Capítulo/apêndice novo: seguir a numeração sequencial e um nome descritivo em kebab-case (ex.: `04-resultados.tex`).

## Regras de escrita (ABNT)

- Português brasileiro; redação impessoal, terceira pessoa ("observa-se", "verifica-se" — nunca "eu observei"/"nós observamos").
- Termos estrangeiros (hardware, firmware, bytecode, sandbox, Ladder etc.) em itálico: `\textit{hardware}`.
- Citações via `\cite{chave}` (estilo alfabético abntex2cite, citações em colchetes). **Nunca inventar chave de referência.** Só citar chaves que já existem em `referencias.bib`; se faltar uma referência necessária, avisar o usuário em vez de criar uma entrada fictícia.
- Rótulos (`\label`) seguem prefixo por tipo, já em uso no projeto: `cap:` (capítulo), `sec:`/`sub:` (seção/subseção), `fig:` (figura), `tab:` (tabela), `ape:` (capítulo de apêndice).
- Manter o padrão de comentários de separação de blocos (`% ---------------------------------------------------------------------------- %`) já usado nos arquivos existentes.

## Compilação

- Sequência: `pdflatex → bibtex → pdflatex → pdflatex`, sempre a partir de `main.tex` (nunca compilar um capítulo isolado).
- No VS Code (LaTeX Workshop), a receita padrão já está em `.vscode/settings.json` (`pdflatex ×2 + bibtex`), roda automaticamente ao salvar.
- Arquivos gerados (`.aux`, `.log`, `.bbl`, `.toc`, `.synctex.gz` etc.) são artefatos de build — não editar nem descrever como conteúdo do trabalho; são limpos automaticamente após cada build.

## Não fazer sem confirmação explícita do usuário

- Alterar `preambulo.tex` (pacotes, margens, fontes, estilo de citação).
- Renomear/mover `main.tex` ou mudar a ordem/numeração dos capítulos já existentes.
- Adicionar ou remover entradas em `referencias.bib`.
- Apagar ou reescrever silenciosamente conteúdo já redigido nos capítulos — proponha a edição em vez de substituir sem avisar.
