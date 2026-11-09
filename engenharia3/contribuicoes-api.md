# Minhas contribuições no API

**Giovanni Moretto**

Participei de 20 tarefas concluídas. A S3-11 segue em aberto porque depende de outras entregas da equipe.

## Preparação

- **PRE-04 — Fundação de testes:** participei da criação da estrutura inicial de testes.
- **PRE-06 — Dados iniciais:** participei da preparação do seed e da política de dados.

## Sprint 1 — Autenticação e gestão de projetos

- **S1-02 — Autenticação:** implementei login, logout, restauração de sessão, proteção de rotas e retorno seguro ao destino original no frontend.
- **S1-04 — Projetos:** implementei a tela e o formulário de projetos, com estados válido, inválido, carregando, erro e vazio.
- **S1-09 — Arquivamento:** implementei o arquivamento em cascata, a prévia da quantidade de itens afetados e o filtro de arquivados.
- **S1-11 — Critérios:** contribuí com os editores de critérios por nível, a confirmação de remoção e a consulta aos critérios.
- **S1-12 — Cenários:** participei da reordenação de cenários, com persistência da ordem e operação pelo teclado.

## Sprint 2 — Documentos, busca e qualidade

- **S2-01 — Processamento de documentos:** participei do fluxo assíncrono com os estados pendente, processando, processado e falha, incluindo motivo da falha e nova tentativa idempotente.
- **S2-02 — Extração de texto:** contribuí com a extração de PDF, DOCX, MD e TXT e com a divisão e o armazenamento de trechos em fronteiras de parágrafo.
- **S2-03 — Índice:** implementei a publicação de eventos para manter o índice sincronizado, sem duplicatas ou itens arquivados.
- **S2-08 — Interface de busca:** participei da criação da interface que mostra trecho, projeto e fonte, sinaliza a ausência de resultados e permite abrir o conteúdo original.
- **S2-09 — Configuração da IA:** participei da estrutura versionada por modo, com esquemas de saída e regras da PRO4TECH que podem ser atualizadas sem reiniciar a aplicação.
- **S2-10 — Questionador e padronizador:** contribuí com o modo que identifica lacunas e o que padroniza o conteúdo por nível, preservando a edição em caso de indisponibilidade.
- **S2-16 — Histórico:** participei dos registros de versão, da listagem por autor e data e da comparação de campos.
- **S2-19 — Qualidade:** participei da implementação dos endpoints e da configuração das verificações de qualidade da organização.
- **S2-20 — DoR e DoD:** contribuí com a configuração e exibição da Definição de Preparado e da Definição de Pronto.
- **S2-24 — RAG:** participei da recuperação de informações, da montagem do contexto e da geração de respostas estruturadas com as evidências e fontes utilizadas.

## Sprint 3 — Chat e respostas com evidências

- **S3-02 — Respostas sem evidência:** implementei a recusa quando não há evidência, a indicação de respostas parciais e o bloqueio de assuntos fora do acervo, com testes de regressão.
- **S3-03 — Escopo e autorização:** implementei a busca em toda a base ou em um projeto, respeitando as permissões e indicando quando ampliar a busca pode ajudar.
- **S3-04 — Interface de chat:** implementei a exibição do escopo, os estados de envio e erro, as citações e a navegação para as fontes.

## Em aberto

- **S3-11 — Busca por experiência profissional:** a tarefa prevê responder a perguntas como “Quem trabalhou com X?” com profissionais, projetos e evidências, e recusar quando não houver informação suficiente. A conclusão aguarda tarefas de outros integrantes.
