# Worldaily — Memória & Contexto do Projeto

> **Idioma de comunicação:** Converse com o usuário em **Português**. A interface do aplicativo suporta **English (`en`)** e **Português (`pt`)** (opção de espanhol foi removida a pedido do usuário).

## 1. Visão Geral
- **Nome:** Worldaily (`Projects & Daily`)
- **Arquivo principal:** `Planner.html` (aplicação web single-file HTML/CSS/JS com Tailwind CSS via CDN, Chart.js, FontAwesome 6 e fontes *Plus Jakarta Sans* & *Inter*).
- **Origem:** Iniciado dentro do projeto `Dolcezzza/Features/Tools/Planner.html` e movido para este workspace dedicado (`Worldaily/`) para evoluir de forma independente.

## 2. Arquitetura & Funcionalidades Atuais (`Planner.html`)
- **Persistência Local (`localStorage`):**
  - `worldaily_workspace_store_v1`: armazena `activeProjectId`, `members` compartilhados e lista `projects` (cada projeto tem `id`, `planTitle`, `category` (`Project` | `Personal`), `description`, `icon`, `buckets`, `labelsCatalog`, `tasks`).
  - `worldaily_theme`: tema `light` ou `dark`.
  - `worldaily_lang`: idioma `en` ou `pt`.
  - Suporta também sincronização opcional com GitHub (`planner_github_config` / `planner_data.json`).
- **Workspaces Padrão:**
  - `Cake Portfolio Development` (`Project`)
  - `Personal & Daily Routine` (`Personal`)
- **Views Implementadas:**
  1. **Projects & Daily Hub (`#view-projects`):** Tela inicial para escolher, filtrar (*All Workspaces*, *Projects*, *Personal & Daily*), criar, editar ou excluir projetos/planos pessoais (`#projectModal`).
  2. **Executive List (`#view-grid`):** Planilha desktop editável inline (`contenteditable` com quebra de linha para *Task*, seletores customizados com seta espaçada para *Assigned to*, *Stage (Bucket)*, *Status*, *Priority*, datas e *Labels*) + visualização em cards no mobile com alternância para tabela.
  3. **Kanban Board (`#view-board`):** Colunas totalmente personalizáveis — criar novas etapas (`addKanbanStage`), renomear inline (`renameKanbanStage`), trocar cor (`cycleKanbanStageColor`), reordenar via setas ou drag-and-drop (`reorderKanbanStage` / `moveKanbanStage`) e excluir etapas (`deleteKanbanStage`, movendo tarefas para a primeira coluna restante).
  4. **Schedule (`#view-calendar`):** Calendário mensal com drag-and-drop de tarefas sem data.
  5. **Insights & Metrics (`#view-charts`):** 4 gráficos Chart.js (*Status Breakdown*, *Volume by Priority*, *Tasks by Stage*, *Workload by Member*).
- **Task Inspector Modal (`#taskModal`):**
  - Seletores segmentados para *Execution Status* e *Priority Level*, *Stage*, *Assigned To*, *Goal*, datas (*Start*, *Finish*, *Due*), *Subtasks Checklist* com barra de progresso, *Notes & Context* e **Tag Studio** inline (`#tagManagerPanel`) para criar tags com cores prontas/customizadas, renomear, mudar cor e apagar qualquer tag diretamente pelo `×` na pill ou no painel.
- **Equipe (`#membersModal`):** Adicionar, alternar perfil ativo e remover membros (`removeMember`).

## 3. Decisões de Design & Restrições do Usuário (Não Regredir)
1. **Identidade Visual:** Paleta Sky-Blue (`#0284C7` / `#0EA5E9`), Light & Dark Mode, **uma única logo Worldaily fixa no `<header>`** e favicon SVG idêntico.
2. **Cabeçalho Limpo:** Sem tags/contadores de resumo (`Total / In progress / Completed`) e sem filtro `All statuses` no topo. Barra de busca agrupada à direita junto do seletor de idioma (`EN / PT`), botão de tema e `+ New Task`.
3. **Painel Lateral (`#appSidebar`):** Sem duplicar a logo; card de projeto ativo sem barra de progresso e com título completo sem corte (`break-words`) + acordeão animado (`wd-accordion-wrapper`) para trocar de projeto. No mobile, abre abaixo do `<header>`.
4. **Sem Fotos / Avatares Circulares:** Não usar fotos de usuário nem círculos com iniciais (`AR`, `DK`); usar sempre ícones `fa-user` e nomes em texto.
5. **Executive List:** Não incluir a coluna `Goal` na tabela principal (foi removida para dar espaço às colunas *Task*, *Assigned to* e *Stage*).
6. **Idiomas:** Apenas **English (`en`)** e **Português (`pt`)** (não adicionar espanhol).
7. **Mobile / APK:** Não gerar `.apk` nem configurar PWA a menos que o usuário peça explicitamente.
