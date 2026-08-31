# Instruções para agentes — TCC

Este arquivo vale para qualquer agente de IA (Claude Code ou outro) que edite este repositório. Regras específicas de escrita e estrutura da monografia — leia antes de criar ou editar qualquer `.tex`.

## Sobre o projeto

Monografia de TCC (IFPB Campus Campina Grande, Bacharelado em Engenharia de Computação). Tema: implementação e validação de uma máquina virtual de lógica Ladder agnóstica de hardware baseada em Model-Based Design. Orientador: Fagner de Araújo Pereira. Escrita em LaTeX com abnTeX2 (classe `book` + `abntex2cite`).

## Fonte de conformidade ABNT

Antes de decidir qualquer questão de formatação ou estrutura não coberta explicitamente abaixo, consulte primeiro o **[Manual de Elaboração de Trabalhos Acadêmicos do IFPB Campus Campina Grande](https://estudante.ifpb.edu.br/media/cursos/26/documentos/Manual_TCC_14.07.2016.pdf)** — é a referência institucional oficial usada neste projeto (não confundir com manuais de outros campi/instituições, que podem divergir em detalhes). Ele é a fonte de verdade para dúvidas de norma; não presuma uma regra ABNT genérica sem checar se o manual do campus diz algo mais específico.

## Estrutura de arquivos

- `main.tex` — arquivo raiz e único ponto de compilação: `\documentclass` + `\input{preambulo}` + corpo do documento (capa, elementos pré-textuais, `\input`/`\include` dos capítulos e apêndices, bibliografia). É o único arquivo com `\begin{document}`/`\end{document}`.
- `preambulo.tex` — pacotes, macros, configuração de listings, formatação de seções (`titlesec`) e do estilo de citação ABNT. **Não alterar sem o usuário pedir explicitamente** — mudanças aqui afetam o documento inteiro e já foram validadas com uma compilação completa.
- `referencias.bib` — banco de referências bibliográficas, estilo `abntex2-alf`.
- `capitulos/NN-nome.tex` — um arquivo por capítulo do corpo principal, numerado (`01-`, `02-`, ...), incluído em `main.tex` via `\input{capitulos/NN-nome}`.
- `apendices/NN-nome.tex` — mesmo padrão, para apêndices, incluído via `\include{apendices/NN-nome}`.
- `figuras/` — imagens, referenciadas sem caminho nem extensão (`\graphicspath{{./figuras/}}` já configurado no preâmbulo).
- Todo arquivo dentro de `capitulos/` e `apendices/` deve começar com `% !TeX root = ../main.tex` (permite compilar a partir de qualquer capítulo aberto no editor).
- Capítulo/apêndice novo: seguir a numeração sequencial e um nome descritivo em kebab-case (ex.: `04-resultados.tex`).

## Formatação de seções e espaçamento (Quadro 2 do manual IFPB-CG)

Já implementado em `preambulo.tex` via `titlesec` — não redefinir sem necessidade, mas é o padrão a seguir se algo precisar de ajuste:

| Seção | Nível LaTeX | Apresentação |
|---|---|---|
| Primária | `\chapter` | **NEGRITO E MAIÚSCULO** |
| Secundária | `\section` | MAIÚSCULO **sem** negrito |
| Terciária | `\subsection` | Negrito, inicial maiúscula (como digitado) |
| Quaternária | `\subsubsection` | Sem negrito, inicial maiúscula |

**Espaçamento**: o manual do IFPB-CG (seção 2.3.2) é explícito — o espaço entre um título e o texto seguinte, e entre o fim de uma seção e o título da seção seguinte, deve ser **o mesmo espaçamento 1,5 usado no resto do texto** (uma linha em branco), nunca um vão maior. Por isso `\titlespacing*` usa `1\baselineskip` em vez de valores fixos grandes em pontos — não trocar por espaçamentos maiores (ex.: `40pt`, `3em` etc.) sob pena de destoar da norma.

## Paginação e cabeçalhos (seção 2.3.4 do manual IFPB-CG)

- As páginas são contadas a partir da folha de rosto, mas **só ficam graficamente numeradas a partir da primeira página da Introdução** (algarismos arábicos). Nenhum elemento pré-textual (capa, folha de rosto, folha de aprovação, dedicatória, epígrafe, agradecimentos, resumo, abstract, listas, sumário) exibe número de página — nem em romano. Implementado em `main.tex` salvando/redefinindo `\ps@plain` para `\ps@empty` durante o `\frontmatter` e restaurando no `\mainmatter` (junto com `\pagestyle{plain}`).
- **Não usar cabeçalhos correntes** (nome do capítulo/seção repetido no topo da página, número de seção solto tipo "1.3"). O manual só pede o número da página; qualquer cabeçalho decorativo (ex.: o estilo "TAOCP" que existia no template original, via `fancyhdr`) foi removido por gerar números de seção soltos e confusos no topo da folha.
- Ordem dos elementos pré-textuais antes do Sumário (NBR 14724): Agradecimentos, Resumo, Abstract, **Lista de Figuras, Lista de Tabelas, Lista de Abreviaturas** — nessa ordem — e só então o Sumário (`\tableofcontents`), que deve ser o último elemento pré-textual, não o primeiro.

## Estrutura da Introdução e capítulos textuais

- Não fragmentar a Introdução (ou qualquer capítulo) em excesso de subseções numeradas. O roteiro oficial do manual IFPB-CG apresenta contextualização, problema, justificativa e objetivos como **texto corrido dentro de um único bloco**, sem subseção dedicada para cada elemento; um TCC real aprovado no mesmo curso/campus usa só 4 subseções na Introdução.
- **Justificativa não precisa de subseção própria** — não há regra ABNT que a exija separada; pode ficar embutida na seção de contextualização/problema. Só crie uma subseção "Justificativa" separada se o conteúdo for extenso o bastante para justificar a quebra.
- Referência de bom tamanho: Introdução com 3-4 subseções de nível `\section` (ex.: Contextualização e Problema; Objetivos com `\subsection` Geral/Específicos; Justificativa; Estrutura do Documento) — evitar ir além disso sem motivo forte.
- Metodologia resumida (se cabível na Introdução) deve ser breve e pode ser absorvida pela seção de "Estrutura do Documento" em vez de ganhar seção própria — a metodologia detalhada, por etapa, pertence aos capítulos de desenvolvimento.

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

- Alterar `preambulo.tex` (pacotes, margens, fontes, estilo de citação, formatação de seções).
- Renomear/mover `main.tex` ou mudar a ordem/numeração dos capítulos já existentes.
- Adicionar ou remover entradas em `referencias.bib`.
- Apagar ou reescrever silenciosamente conteúdo já redigido nos capítulos — proponha a edição em vez de substituir sem avisar.
- Fundir ou desmembrar subseções de capítulos já escritos sem avisar — mesmo seguindo a diretriz acima de manter poucas subseções.
