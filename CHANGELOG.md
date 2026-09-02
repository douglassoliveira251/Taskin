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
