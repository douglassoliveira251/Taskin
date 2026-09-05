## [1.8.044] - 2026-09-05 15:39

### Renomeação: Categorias → Espaços

- "Categoria(s)" renomeada para "Espaço(s)" em todas as referências visíveis: aba de Configurações, rótulos de campo, botões, mensagens de confirmação, agrupamento de tarefas, tela de mover item de espaço, etc. As chaves internas (`data-tab="categorias"`, `catById`, `getOrderedCategories` etc.) foram mantidas intactas, mesmo princípio já usado na renomeação para Taskin.

### Added

#### General

- Novo **seletor de espaço** no topo da tela, antes do título: combo com círculo colorido + nome do espaço + seta, abrindo um menu com a lista de espaços (com marca de seleção), opção "Todos os espaços", "+ Novo espaço" (cria e leva direto para Configurações com o campo em foco) e "Gerenciar espaços" (vai para a aba Espaços). Presente nas telas de Tarefas, Notas, Calendário e Visão geral.
- Lista de espaços removida do menu lateral — a seleção agora é feita inteiramente pelo novo seletor no topo, com o mesmo comportamento de antes (sincroniza agrupamento salvo, visão de calendário salva, limpa a busca).

#### Visão geral (Dashboard)

- Tela renomeada de "Dashboard" para "Visão geral" (título e item de menu).
- Redesenho completo com cinco cards de indicadores no topo: **Tarefas** (total, concluídas/pendentes nos últimos 45 dias, barra de progresso), **Notas** (total, novas na semana, gráfico sparkline dos últimos dias), **Eventos hoje** (contagem, próximo evento, atalho para o Calendário), **Tags mais usadas** (total distintas, top 3 em pills, atalho para Configurações → Tags) e **Itens importantes** (tarefas de prioridade alta/crítica + notas fixadas).
- Segunda linha de cards: **Tarefas por prioridade** (gráfico de rosca com total no centro e legenda com contagem/percentual), **Atividades recentes** (feed real das últimas 4 ações — tarefa concluída, nota criada, agenda criada/atualizada — com ícone, espaço de origem, módulo e horário relativo) e **Próximos eventos** (lista compacta com data/hora, título e categoria colorida).
- Terceira seção: **Indicadores gerais** (taxa de conclusão, % em atraso, criadas vs. concluídas em 30 dias, agendas hoje, carga por espaço).
- Quarta linha: **Notas recentes** (lista com ícone, título, pill do espaço e "Editada hoje/ontem/em DD/MM/AAAA") e **Tarefas importantes** (checkbox, título, pill de prioridade, data amigável "Hoje"/"Amanhã"/data completa, bandeira vermelha para prioridade Crítica).
- Visão geral passou a sempre considerar **todos os espaços**, independente do espaço selecionado no seletor do topo — o restante do sistema continua respeitando o filtro normalmente.
- Rastreamento de `updatedAt` adicionado aos eventos do calendário (não existia antes), permitindo diferenciar "agenda criada" de "agenda atualizada" no feed de atividades.

### Changed

#### Visão geral (Dashboard)

- KPIs de conclusão (card "Tarefas" e "Taxa de conclusão") passaram a considerar apenas tarefas concluídas nos **últimos 45 dias**, não o total histórico.
- Gráfico de rosca "Tarefas por status" substituído por "Tarefas por prioridade", reaproveitando os mesmos dados já usados em outro ponto do dashboard.
- Peso da fonte dos números de destaque reduzido (de extra-negrito para um peso mais simples) em todo o dashboard.
- Tamanhos de fonte gerais do dashboard reduzidos (números, títulos de seção, linhas de lista, rótulos).
- Círculo do gráfico de prioridade aumentado (118px → 150px).
- Layout do card "Próximos eventos" simplificado para o formato compacto (data/hora em uma linha, título, categoria colorida à direita).
- Botão do seletor de espaço com visual menos destacado (borda neutra em vez de preenchimento verde) e levemente mais alto.
- Card "Notas recentes" (formato lista) por notas recentes.

### Removed

#### Visão geral (Dashboard)

- Removidos, por redundância com os novos cards de indicadores: banner de "tarefa crítica e vencida", bloco "Vencidas e Hoje / Esta Semana / Próximas agendas", bloco antigo "Tarefas abertas por prioridade / Produtividade", faixa "Últimas Notas" e seção "Outros pontos de atenção".
## [1.7.040] - 2026-09-02 00:05

### Renomeação do sistema

- Sistema renomeado de "TYVRA Tasks" para **Taskin** em todas as referências visíveis: título da página, marca na sidebar (logo antigo substituído por marca em texto), nome de arquivo padrão sugerido (`taskin.json`), textos de diálogo e metadados de exportação `.ics`.
- As chaves internas de armazenamento (`localStorage`, `IndexedDB`) foram mantidas intactas de propósito, para não causar perda aparente dos dados já salvos pelos usuários.

### Added

#### General

- Perfil do usuário movido do topo da sidebar para um **avatar circular no canto superior direito**, com avatar genérico (ícone) quando não há foto cadastrada.
- Menu dropdown no avatar com as opções **Perfil**, **Configurações** e **Sair** (aciona a desconexão do arquivo).
- Botão de **notificações** (sino) no topo, ainda sem função — placeholder para funcionalidade futura.

#### Sidebar

- Sidebar agora é **expansível/minimizável**, com botão dedicado em formato de círculo flutuante na borda direita, posicionado logo abaixo do nome do sistema.
- No modo minimizado, a sidebar fica só com ícones; a lista de categorias vira um botão único que abre um popover para seleção.
- Alternador de modo escuro/claro sempre fixado no rodapé da sidebar (`margin-top:auto`), na mesma posição em ambos os modos (expandido e minimizado).
- Cor da sidebar fixada permanentemente no esquema escuro, independente do tema geral do sistema — trocar entre modo claro/escuro agora afeta só o restante da tela.
- Largura útil das telas de Notas aumenta automaticamente quando a sidebar está minimizada, aproveitando o espaço liberado.

#### Notes

- Associação de notas com tarefas, no mesmo padrão já usado no calendário: botão "Vincular tarefa" no composer da nota, e seção "Notas" no painel de edição da tarefa listando as vinculadas.
- Ícone do menu "Notas" substituído por um de documento com linhas de texto (mais parecido com anotações).

#### Calendar

- Colunas de data da visão mensal e semanal destacam sábado e domingo com cor diferenciada.
- Eventos com título longo agora quebram linha em vez de estourar a largura da célula (visão mensal).

### Changed

#### Tasks

- Campos "Prazo e hora" e "Recorrência" ficam na mesma linha, lado a lado, com larguras recalculadas para não sobrepor nem cortar texto.
- Coluna de data/hora dimensionada ao próprio conteúdo; Recorrência cresce para ocupar o espaço restante.
- Altura dos campos de data/hora/recorrência padronizada em 34px, alinhados horizontalmente.
- Campos "Status" e "Prioridade" na mesma linha, com distribuição de largura ajustada para dar mais espaço aos botões de prioridade.
- Removidos os textos "Nenhuma agenda/nota vinculada a esta tarefa" — os campos ficam apenas em branco quando vazios.
- Largura do painel de edição fixada em 500px.

#### Calendar

- Campos de data/hora de Início e Fim do composer de evento recalculados para o contexto mais estreito do modal, corrigindo sobreposição.

#### General

- Botão "Desconectar" removido da barra superior — acessível apenas via "Sair" no menu do avatar.
- Nome do arquivo removido da exibição no topo (status do arquivo continua acessível em Configurações → Arquivo).

### Fixed

#### Notes

- Corrigido bug crítico de **duplicação de notas**: o mecanismo de salvamento de segurança (acionado ao trocar de aba/minimizar/fechar) criava uma nova entrada a cada acionamento para notas ainda não salvas, em vez de atualizar a mesma nota. Corrigido tornando a criação idempotente.
- Corrigido o botão de limpar formatação, que ao processar uma seleção dentro de um único parágrafo reconstruía o bloco inteiro, podendo alterar conteúdo fora da seleção e perder quebras de linha. Corrigido usando o `removeFormat` nativo do navegador para esse caso, preservando o restante do conteúdo intacto.

#### Tasks

- Corrigido bug de CSS em que a coluna de Prioridade parou de esticar até a borda direita do painel por reutilizar, por engano, a mesma classe de outra coluna (Prazo e hora); agora usa uma classe própria.

#### Calendar

- Corrigido o cálculo de largura das colunas da visão mensal (bug de `min-width` do CSS Grid) que fazia colunas ficarem com tamanhos desiguais quando havia conteúdo mais longo.

#### Sidebar

- Corrigido o efeito hover do botão de minimizar/expandir, que clareava em vez de escurecer devido a um efeito colateral da cor fixa escura da sidebar; trocado para `filter: brightness()`, que sempre escurece corretamente.
