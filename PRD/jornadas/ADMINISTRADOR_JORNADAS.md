# Jornadas do Administrador

## Base e rastreabilidade

**Persona-fonte:** [ADMINISTRADOR.md](../personas/ADMINISTRADOR.md)

**Acesso:** elevado e concedido conforme permissões administrativas; ações sensíveis permanecem autenticadas, autorizadas, atribuíveis e auditáveis. O acesso direto ao armazenamento de produção é excepcional e controlado, não o fluxo normal de manutenção.

**Objetivo central:** manter a aplicação segura e disponível e assegurar que dados, conteúdo e acessos sejam íntegros, atuais e apresentados ao público correto.

As jornadas não escolhem tecnologia. Dados esportivos podem depender de uma **fonte externa de dados esportivos**; dados comerciais e de redes podem depender de fontes externas conceituais. A origem, o estado e a atualização devem ser identificáveis sempre que disponíveis.

## J01 — Acessar a área administrativa e avaliar a operação

### Persona
Administrador da Plataforma.

### Objetivo
Entrar com segurança, identificar riscos operacionais e priorizar tarefas ou incidentes.

### Relação com a persona
- **Objetivo atendido:** identificar rapidamente falhas, inconsistências e problemas de sincronização.
- **Necessidade atendida:** painel de saúde, estado das integrações, últimas execuções e falhas identificáveis.
- **Dor reduzida:** alertas sem contexto ou ausência de evidência operacional.

### Pré-condições
- O usuário possui conta administrativa ativa e permissão de acesso à área.
- Existem dados operacionais a consultar; a ausência deles deve ser identificada.

### Gatilho
O administrador abre a área administrativa ou recebe indicação de incidente.

### Fluxo principal
1. O administrador informa credenciais e conclui os controles de autenticação exigidos.
2. O sistema valida identidade, estado da conta e permissão administrativa e cria uma sessão autorizada.
3. O dashboard solicita estado da aplicação, alertas, integrações, sincronizações e métricas gerais.
4. O sistema reúne saúde, horário da última execução, erros recentes, áreas afetadas e rotinas operacionais disponíveis.
5. A interface apresenta resumo priorizável e permite abrir o detalhe de alerta, integração ou métrica.
6. O administrador seleciona um item; o sistema verifica novamente a autorização e carrega seu contexto.

### Responsabilidade do Front-end
- Oferecer login administrativo e feedback de autenticação.
- Exibir visão de saúde e diferenciar alertas críticos, avisos e itens informativos segundo severidade definida pelo produto.
- Apresentar últimas execuções, estado, erros e entidades afetadas, quando conhecidos.
- Permitir filtrar por período, integração, categoria e estado, conforme permissões.
- Mostrar carregamento, ausência de eventos, falha de consulta e dados desatualizados.

### Responsabilidade do Back-end
- Autenticar e autorizar o acesso à área administrativa e às funções específicas.
- Recuperar estado e métricas das áreas operacionais, integrações, sincronizações e eventos.
- Agregar alertas sem eliminar ligação aos registros/execuções de origem.
- Registrar eventos relevantes de acesso administrativo.
- Retornar atualização e cobertura de cada indicador.

### Dados envolvidos
- Identidade, conta, permissões, sessão e eventos de autenticação.
- Estado operacional, alertas, integrações, execuções, erros, registros afetados e métricas agregadas.
- Horários, estado de atualização e severidade.

### Regras envolvidas
- Acesso elevado exige autenticação e autorização explícitas.
- Visibilidade de painel ou ação deve respeitar a permissão concedida ao administrador.
- Métrica sem dados não significa operação saudável; indisponibilidade e dado atrasado são estados distintos.

### Validações
- Conta ativa, credenciais válidas, sessão válida e permissão para área/função.
- Datas e filtros válidos para consulta.
- Estado e horário de atualização consistentes com eventos disponíveis.

### Fluxos alternativos
- Administrador sem alertas: exibir Success operacional acompanhado do instante da última atualização.
- Administrador acessa função para a qual não tem permissão: oferecer rota para solicitar acesso, sem revelar informação protegida.
- Métricas parcialmente disponíveis: indicar componentes sem cobertura.

### Fluxos de erro
- Autenticação inválida ou conta suspensa: negar acesso e informar a condição sem expor detalhes sensíveis.
- Falha no painel: apresentar erro e permitir acesso a áreas cuja consulta continue disponível.
- Dados operacionais atrasados: marcar o estado como desconhecido/desatualizado, não como saudável.

### Resultado esperado
O administrador entra no escopo autorizado e identifica o que exige ação com contexto e estado confiáveis.

## J02 — Gerenciar usuários, papéis e permissões

### Persona
Administrador autorizado para gestão de acessos.

### Objetivo
Conceder, revisar, alterar, suspender ou remover acesso conforme a responsabilidade de cada usuário.

### Relação com a persona
- **Objetivo atendido:** gerenciar usuários e permissões de acordo com suas responsabilidades.
- **Necessidade atendida:** visualizar usuários, papéis, permissões e estado de acesso.
- **Dor reduzida:** acessos indevidos, permissões amplas demais e dificuldade para revogá-los.

### Pré-condições
- Administrador autenticado com permissão de gestão de acessos.
- Usuário ou novo convite identificável e escopo de acesso definido.

### Gatilho
O administrador abre a gestão de usuários ou precisa alterar um acesso.

### Fluxo principal
1. O administrador pesquisa ou seleciona um usuário ou inicia criação de acesso.
2. A interface apresenta estado atual, papel, permissões, vínculo comercial/administrativo quando aplicável e histórico pertinente.
3. O administrador escolhe criar/ativar, editar, suspender, remover ou revisar acesso e informa o escopo desejado.
4. O sistema valida autoridade do operador, consistência do usuário e limites de privilégio.
5. Antes de mudança de alto impacto, a interface apresenta resumo do estado anterior e novo para confirmação.
6. O sistema grava a alteração e sua trilha de auditoria; atualiza o estado de acesso conforme a ação.
7. A interface informa sucesso e apresenta o novo estado.

### Responsabilidade do Front-end
- Pesquisar, filtrar e visualizar usuários e estados de acesso.
- Apresentar permissões em termos claros, evitando seleção ambígua de privilégios.
- Distinguir papéis de torcedor, investidor/parceiro e administrador e respectivos escopos.
- Mostrar diferenças antes/depois e exigir confirmação proporcional ao impacto.
- Informar sucesso, recusa, falha de validação e impossibilidade de remover a própria trilha de auditoria.

### Responsabilidade do Back-end
- Autenticar operador e autorizar cada operação de acesso.
- Validar papéis, permissões, escopos, estados e restrições de segregação.
- Aplicar alteração sem exceder o nível que o operador pode conceder.
- Revogar ou atualizar o acesso afetado de forma consistente.
- Registrar ator, ação, valores anteriores/novos, data/hora, entidade e resultado.
- Preservar trilha de auditoria contra edição/exclusão pelo mesmo administrador.

### Dados envolvidos
- Usuários, identificadores, papel, permissões, estado, vínculo comercial/administrativo e sessão.
- Alteração solicitada, justificativa quando exigida, confirmação e evento de auditoria.

### Regras envolvidas
- Privilégio mínimo necessário e escopo explícito.
- Parceiros só acessam dados agregados e campanhas autorizadas.
- Torcedores não obtêm permissões de manutenção de dados.
- Nenhuma alteração apaga ou torna não atribuível a trilha de auditoria da própria ação.
- A concessão de permissão não pode ultrapassar a autoridade do administrador executor.

### Validações
- Administrador autorizado para usuário, função e escopo selecionados.
- Identificador de usuário válido e sem duplicidade.
- Permissões compatíveis entre si e com o estado da conta.
- Ações críticas confirmadas e registráveis.

### Fluxos alternativos
- Usuário não encontrado: permitir nova pesquisa ou início de criação, sem alterar dados.
- Permissão já concedida: manter estado atual e evitar duplicação.
- Acesso suspenso reativado: registrar a mudança e comunicar o novo estado ao operador.

### Fluxos de erro
- Ação fora da autoridade do operador: negar e não persistir alteração.
- Conflito de estado por atualização concorrente: recarregar estado atual e solicitar nova confirmação.
- Falha ao registrar auditoria: não confirmar como concluída uma alteração que exija trilha.
- Falha ao atualizar acesso: manter estado anterior e apresentar erro acionável.

### Resultado esperado
O acesso do usuário reflete o escopo aprovado, e toda mudança importante pode ser explicada e atribuída.

## J03 — Administrar clubes, jogadores, partidas e estatísticas

### Persona
Administrador responsável por dados esportivos.

### Objetivo
Manter cadastros e informações esportivas consistentes e corretamente disponibilizados.

### Relação com a persona
- **Objetivo atendido:** manter clubes, jogadores, partidas, campeonatos, rodadas e estatísticas consistentes.
- **Necessidade atendida:** pesquisa, filtros, origem, histórico e fluxos seguros de criação/edição/publicação.
- **Dor reduzida:** dados incorretos/duplicados e correções dispersas ou sem fonte evidente.

### Pré-condições
- Administrador com permissão de gestão da entidade.
- Entidade existente ou informação documentada a incluir/corrigir.

### Gatilho
O administrador recebe uma tarefa de manutenção, detecta inconsistência ou revisa dados recebidos.

### Fluxo principal
1. O administrador escolhe tipo de entidade (clube, jogador, campeonato, rodada, partida ou estatística) e pesquisa registros.
2. O sistema apresenta registros relacionados, estado de publicação, origem, atualização e histórico de alteração.
3. O administrador seleciona criar, editar, corrigir, arquivar ou publicar e fornece valores e justificativa quando requerida.
4. O sistema valida formato, relações, estado esportivo e possíveis duplicidades/inconsistências.
5. Para alteração importante, a interface apresenta valores anteriores e novos; o administrador confirma.
6. O sistema grava a alteração, registra auditoria, atualiza estado de publicação e propaga a informação às consultas dependentes.
7. A interface confirma resultado e apresenta estado de sincronização/publicação.
8. O administrador verifica o registro ou os dados derivados para confirmar a correção.

### Responsabilidade do Front-end
- Oferecer busca e filtros por identificador, clube, competição, rodada, jogador, estado, fonte e período.
- Apresentar relações entre entidades e estado público/restrito/interno.
- Exibir origem, última atualização e alterações anteriores.
- Diferenciar rascunho, validado, publicado, arquivado e estado de sincronização.
- Apresentar validações antes de gravar e confirmar alterações de alto impacto.
- Permitir verificar o resultado e localizar os consumidores/visões afetados, quando conhecido.

### Responsabilidade do Back-end
- Consultar e alterar registros apenas no escopo autorizado.
- Validar campos, duplicidades, vínculos e coerência entre clube, jogador, campeonato, rodada, partida e estatística.
- Identificar conflito entre valor informado e fonte esportiva externa sem substituir silenciosamente uma correção administrativa.
- Armazenar origem, data/hora e usuário responsável conforme aplicável.
- Registrar estado anterior/novo e resultado na auditoria.
- Atualizar consultas derivadas e propagar correções, expondo o estado e falhas da propagação.

### Dados envolvidos
- Clubes, jogadores, campeonatos, temporadas, rodadas, partidas, placares e estatísticas.
- Relações e estado de publicação; fonte, horário de atualização, autor, justificativa e histórico.

### Regras envolvidas
- Valores devem respeitar relações esportivas e estado oficial da entidade.
- Publicação só ocorre após validações aplicáveis e autorização.
- Dado não confirmado não deve ser apresentado como oficial.
- A correção deve preservar a versão anterior na trilha de auditoria.
- Arquivar/remover logicamente não deve quebrar referências históricas válidas.

### Validações
- Campos obrigatórios, tipos e faixas válidas segundo regras de negócio a definir.
- Identificadores e relações existentes e compatíveis.
- Duplicidade de entidade ou evento.
- Estado da partida compatível com placar, escalação e estatísticas informadas.
- Permissão e confirmação para publicação ou ação irreversível.

### Fluxos alternativos
- Registro novo não possui fonte externa: permitir inclusão manual apenas se autorizada e identificada como tal.
- Fonte externa envia valor divergente: apresentar conflito para revisão, sem sobregravar silenciosamente.
- Registro arquivado é necessário a uma relação histórica: preservar consulta histórica conforme política de produto.

### Fluxos de erro
- Dados inválidos/inconsistentes: destacar campos/relações, não persistir parcialmente.
- Duplicidade provável: interromper ou exigir decisão explícita sem apagar registros.
- Falha na gravação: conservar estado anterior e informar a ação não concluída.
- Gravação concluída, mas propagação falha: distinguir sucesso de gravação de falha de atualização das visões dependentes.

### Resultado esperado
Dados esportivos são mantidos com contexto, validação, confirmação, rastreabilidade e confirmação de propagação.

## J04 — Investigar inconsistências e reconciliar dados

### Persona
Administrador responsável por qualidade de dados.

### Objetivo
Encontrar, avaliar e resolver duplicidades, divergências e dados incompletos sem ocultar sua origem.

### Relação com a persona
- **Objetivo atendido:** identificar duplicidades, inconsistências e problemas de sincronização.
- **Necessidade atendida:** localizar registros afetados, comparar histórico e confirmar propagação.
- **Dor reduzida:** erros sem contexto, correções manuais dispersas e sobrescritas sem auditoria.

### Pré-condições
- Existem alertas, relatórios de consistência ou suspeita de divergência.
- Administrador pode consultar as entidades envolvidas.

### Gatilho
Um alerta é recebido, uma verificação encontra inconsistência ou o administrador inicia análise.

### Fluxo principal
1. O administrador abre a inconsistência e consulta entidade, campos, origem, horário e impacto conhecido.
2. O sistema recupera registros relacionados, histórico, sincronizações e possíveis duplicados.
3. O administrador compara os valores e determina a ação permitida: corrigir, associar, descartar registro inválido ou encaminhar para revisão.
4. O sistema valida a decisão e apresenta impacto e valores anteriores/novos.
5. O administrador confirma a resolução.
6. O sistema registra a decisão e sua justificativa, atualiza a entidade e solicita/acompanha propagação.
7. O administrador verifica a resolução e fecha ou mantém o incidente pendente conforme resultado.

### Responsabilidade do Front-end
- Apresentar alerta, causa conhecida, entidade afetada, possíveis registros correspondentes e ações disponíveis.
- Comparar valores/origens lado a lado e exibir datas e histórico.
- Diferenciar suspeita automática de conclusão confirmada pelo administrador.
- Solicitar confirmação e justificativa quando requerido.
- Mostrar estado aberto, em análise, resolvido ou falha na propagação.

### Responsabilidade do Back-end
- Detectar/registrar sinais de inconsistência e relacioná-los aos registros de origem.
- Recuperar histórico e metadados sem descartar divergências.
- Validar a decisão e aplicar alteração de maneira atômica quando necessário.
- Auditar ator, ação, valores anterior/novo, entidade, instante e resultado.
- Reprocessar ou propagar dados dependentes e devolver seu estado.

### Dados envolvidos
- Alertas, entidades, valores conflitantes, duplicidades, origem, histórico e sincronizações.
- Decisão, justificativa, alterações e resultados de propagação.

### Regras envolvidas
- Não consolidar ou descartar duplicatas sem decisão autorizada e rastreável.
- Divergência entre origem externa e correção manual deve permanecer explicável.
- Resolução só é concluída quando a ação primária e o estado final estiverem claros.

### Validações
- Registros afetados pertencem ao escopo autorizado.
- Decisão não rompe relações ou histórico válido.
- Conflitos e valores finais estão identificados antes de confirmar.

### Fluxos alternativos
- A causa não é conclusiva: manter como investigação aberta e encaminhar, sem aplicar correção especulativa.
- O dado é correto, mas a fonte está atrasada: registrar a decisão e acompanhar a fonte/sincronização.
- Propagação pendente: manter situação resolvida parcialmente, não marcar todas as superfícies atualizadas.

### Fluxos de erro
- Evidência/histórico indisponível: não permitir resolução definitiva sem indicar a limitação.
- Erro ao corrigir: reter o estado anterior e manter o incidente aberto.
- Falha de propagação: emitir estado/alerta acionável, sem apresentar dados dependentes como atualizados.

### Resultado esperado
Inconsistências são resolvidas ou encaminhadas com evidência e trilha de decisão; impactos residuais ficam visíveis.

## J05 — Monitorar integrações e sincronizações

### Persona
Administrador responsável por operação de dados.

### Objetivo
Identificar falhas de recebimento/processamento externo e garantir que os registros afetados sejam tratados.

### Relação com a persona
- **Objetivo atendido:** administrar integrações e acompanhar disponibilidade e qualidade.
- **Necessidade atendida:** estado, horário, erros, tentativas e dados afetados.
- **Dor reduzida:** erros difíceis de diagnosticar e sintomas sem entidade ou período.

### Pré-condições
- Integração ou sincronização conceitual configurada e visível ao administrador.
- Permissão de monitoramento ou operação correspondente.

### Gatilho
O administrador abre o painel de integrações, recebe alerta ou investiga dados desatualizados.

### Fluxo principal
1. O administrador seleciona integração, intervalo ou execução.
2. O sistema recupera estado, última execução, duração/resultado disponível, erros, tentativas e entidades afetadas.
3. A interface apresenta histórico pesquisável e separa falha, execução em andamento, atraso e sucesso.
4. O administrador abre um evento e avalia a causa e o escopo do impacto.
5. Se autorizado, solicita repetição ou reprocessamento controlado, ou encaminha a ocorrência.
6. O sistema valida a ação, registra operador e solicitação e informa resultado.
7. O administrador acompanha a nova execução e verifica atualização dos dados afetados.

### Responsabilidade do Front-end
- Listar integrações conceituais e estado/última atualização.
- Pesquisar execuções por período, estado e entidade afetada.
- Exibir erros em linguagem acionável e contexto suficiente para investigação.
- Restringir controles de repetição/reprocessamento às permissões específicas e solicitar confirmação.
- Distinguir sucesso de execução de atualização confirmada das entidades.

### Responsabilidade do Back-end
- Manter estado e histórico de execução, falhas, tentativas e abrangência de registros.
- Detectar atraso ou falha segundo regras operacionais definidas.
- Validar e executar nova tentativa/reprocessamento somente quando autorizado e seguro.
- Evitar duplicação de dados ou efeitos repetidos em operações repetidas.
- Registrar solicitação e resultado operacional e expor atualização final dos registros afetados.

### Dados envolvidos
- Identificação da integração, execuções, horários, estados, tentativas, erros e entidades afetadas.
- Solicitações de repetição, operador e resultados.

### Regras envolvidas
- Ausência de atualização é distinta de uma execução bem-sucedida sem novos dados.
- Reprocessamento não deve duplicar partidas, jogadores ou estatísticas.
- Mensagens de erro podem ocultar detalhes sensíveis, mantendo informação segura para investigação autorizada.

### Validações
- Integração/execução existe e pertence ao escopo de consulta.
- Operador tem permissão para solicitar reprocessamento.
- A execução não está em estado incompatível com nova solicitação.

### Fluxos alternativos
- Execução concluiu sem registros novos: apresentar Success e quantidade/escopo processado, quando disponíveis.
- Execução está em andamento: apresentar estado e permitir acompanhar, sem iniciar operação duplicada.
- Integração sem dados históricos: mostrar Empty State e data inicial de cobertura, se conhecida.

### Fluxos de erro
- Erro na consulta de estado: declarar que o estado não pôde ser confirmado.
- Reprocessamento falha: preservar erro, identificar execução e manter dados marcados conforme atualização real.
- Dados parcialmente atualizados: informar entidades concluídas e pendentes sem declarar sucesso global.

### Resultado esperado
O administrador entende saúde, cobertura e impacto das integrações e consegue acompanhar uma ação operacional até sua confirmação.

## J06 — Gerenciar conteúdo, visibilidade e publicidade

### Persona
Administrador responsável por conteúdo e publicação.

### Objetivo
Controlar o que é público, restrito ou interno e administrar conteúdo e publicidade sem publicação acidental.

### Relação com a persona
- **Objetivo atendido:** controlar a visibilidade de informação e conteúdo.
- **Necessidade atendida:** estado de publicação claro e controle de publicidade/conteúdo.
- **Dor reduzida:** publicar conteúdo restrito ou dado não validado por engano.

### Pré-condições
- Administrador tem permissão para conteúdo, publicidade e escopo selecionados.
- Conteúdo ou campanha existe ou está sendo criado.

### Gatilho
O administrador cria, edita, revisa, agenda, publica, restringe ou encerra conteúdo/campanha.

### Fluxo principal
1. O administrador seleciona conteúdo ou campanha e consulta estado, escopo, período e histórico.
2. A interface apresenta campos e visibilidade atual.
3. O administrador altera conteúdo, público autorizado, clube/área associada e período, quando aplicável.
4. O sistema valida completude, coerência de período, autorização e possíveis conflitos de visibilidade.
5. O sistema apresenta resumo da alteração e impacto esperado; o administrador confirma.
6. O sistema atualiza o estado e registra autoria, valores anteriores/novos, data/hora e entidade.
7. A interface confirma publicação/restrição e apresenta estado efetivo.

### Responsabilidade do Front-end
- Pesquisar conteúdo/campanhas e exibir estados rascunho, agendado, publicado, restrito e encerrado.
- Apresentar escopo de audiência, clube, período e áreas de exibição com clareza.
- Alertar quando a ação amplia visibilidade e solicitar confirmação.
- Diferenciar conteúdo esportivo validado de rascunho ou dado pendente.
- Mostrar confirmação e trilha/histórico acessível.

### Responsabilidade do Back-end
- Autorizar mudanças de conteúdo e publicidade pelo escopo do administrador.
- Validar período, dependências, visibilidade e estado de publicação.
- Aplicar estado efetivo e impedir acesso de perfis fora do escopo.
- Registrar auditoria com ator, ação, valores anterior/novo, instante e entidade.
- Retornar conflitos e estado de propagação da alteração.

### Dados envolvidos
- Conteúdo, publicidade/campanhas, clubes, segmentos autorizados, período, estado de publicação e áreas de exibição.
- Autor, estado anterior/novo, auditoria e métricas disponíveis associadas.

### Regras envolvidas
- Conteúdo restrito/interno não pode ser exposto por uma rota pública.
- Publicidade deve ser identificável e não pode impedir tarefas esportivas centrais.
- Dados esportivos não validados não devem ser promovidos a informação oficial.
- Mudança importante de visibilidade é auditável e confirmada.

### Validações
- Permissão para conteúdo/campanha e escopo selecionado.
- Data inicial/final e transições de estado coerentes.
- Conteúdo e entidade relacionados existem e estão aptos à publicação.

### Fluxos alternativos
- Alteração fica em rascunho para revisão: confirmar salvamento sem indicar publicação.
- Campanha termina: apresentar encerramento e manter histórico de consulta autorizado.
- Conteúdo depende de validação esportiva: manter não público e indicar pendência.

### Fluxos de erro
- Falta de permissão: negar mudança e manter estado.
- Conflito de datas/escopo: destacar campos e impedir publicação.
- Falha ao propagar estado: diferenciar alteração registrada de visibilidade ainda não confirmada.

### Resultado esperado
Conteúdo e publicidade são publicados no escopo correto, com estado compreensível e histórico atribuível.

## J07 — Consultar logs, auditoria, métricas e recuperação operacional

### Persona
Administrador autorizado.

### Objetivo
Investigar eventos, comprovar mudanças e acompanhar métricas, backups e capacidade de recuperação.

### Relação com a persona
- **Objetivo atendido:** acompanhar acessos, métricas, logs e backups e conseguir explicar/reverter mudanças quando possível.
- **Necessidade atendida:** eventos pesquisáveis, auditoria e rotinas verificáveis de recuperação.
- **Dor reduzida:** alterações sem autor/histórico e falta de confiança em backups.

### Pré-condições
- Administrador autenticado com permissão para o tipo de log, auditoria, métrica ou rotina consultada.
- Período/entidade de interesse identificado ou consulta geral necessária.

### Gatilho
O administrador investiga incidente, verifica auditoria, métricas gerais ou estado de backup/recuperação.

### Fluxo principal
1. O administrador escolhe logs, auditoria, métricas ou rotinas de backup/recuperação e define filtros.
2. O sistema verifica permissão e recupera somente o escopo autorizado.
3. A interface apresenta eventos por data/hora, operador, ação, entidade, resultado e contexto permitido.
4. O administrador abre evento ou rotina para examinar valores anteriores/novos, estado, cobertura e resultado.
5. Quando houver operação de recuperação autorizada, o administrador revisa impacto e confirma o procedimento.
6. O sistema executa ou acompanha o procedimento, registra solicitante, escopo, resultado e falhas.
7. A interface apresenta conclusão, pendências e próximo passo operacional.

### Responsabilidade do Front-end
- Permitir filtros por data, entidade, ator, categoria e resultado quando autorizados.
- Exibir trilha de alterações legível e preservar distinção entre evento e interpretação.
- Mostrar métricas gerais com período, definição e atualização.
- Apresentar estado de cópia de segurança/verificação/recuperação e resultados disponíveis.
- Exigir revisão e confirmação para recuperação ou ação de impacto amplo.

### Responsabilidade do Back-end
- Recuperar e proteger registros de log/auditoria contra alteração por operador sem autoridade.
- Aplicar filtros e permissões antes de retornar eventos ou métricas.
- Manter sequência e atribuição de eventos administrativos relevantes.
- Disponibilizar evidências de execução, verificação e cobertura das rotinas de backup/recuperação.
- Registrar solicitação e resultado de ações de recuperação e comunicar falhas explicitamente.

### Dados envolvidos
- Logs, acessos autorizados, auditoria, atores, ações, valores anterior/novo, entidades e resultados.
- Métricas agregadas, intervalo, definições, rotinas de backup, verificação e recuperação.

### Regras envolvidas
- Administrador não pode apagar ou alterar a trilha de suas próprias ações.
- Acesso a eventos individuais deve respeitar finalidade e permissão; dados pessoais devem ser minimizados.
- Backup existente não equivale a recuperação verificada.
- Recuperação deve ter escopo, impacto e resultado rastreáveis.

### Validações
- Acesso permitido ao tipo de evento e intervalo.
- Filtros válidos e compatíveis com limites de consulta.
- Ação de recuperação exige permissão específica e confirmação.

### Fluxos alternativos
- Nenhum evento no intervalo: informar ausência de registros e manter os filtros visíveis.
- Rotina de recuperação apenas em simulação/verificação: identificar claramente que dados não foram restaurados.
- Evento parcialmente detalhado por privacidade: indicar campos ocultados e motivo permitido.

### Fluxos de erro
- Falha ao carregar logs/auditoria: não sugerir ausência de eventos.
- Backup/verificação indisponível: indicar que a condição não pôde ser confirmada.
- Recuperação falha ou parcial: identificar escopo concluído e pendente e manter alerta operacional.

### Resultado esperado
O administrador tem evidência confiável para explicar mudanças e avaliar prontidão operacional, sem confundir cópia com recuperação comprovada.

## Estados transversais da aplicação

| Estado | Comportamento esperado para o administrador |
|---|---|
| Loading | Indicar consulta/ação em andamento e impedir repetição acidental de operação crítica. |
| Empty State | Distinguir lista sem registros de consulta falha e manter filtros/contexto visíveis. |
| Success | Confirmar escopo, entidade, estado final e eventuais pendências de propagação. |
| Error | Informar causa e próximo passo seguro; não mascarar resultado parcial como sucesso. |
| Unauthorized | Negar consulta/ação e identificar necessidade de permissão sem expor dados protegidos. |
| Not Found | Informar entidade/evento não encontrado ou não disponível no escopo do administrador. |
| Dados desatualizados | Mostrar instante conhecido e marcar estado operacional como não confirmado quando a atualização falhar. |

## Revisão de cobertura da persona

- Painel administrativo, autenticação e métricas gerais: J01 e J07.
- Usuários, papéis e permissões: J02.
- Clubes, jogadores, partidas, estatísticas, campeonatos e rodadas: J03.
- Correção, duplicidade e inconsistência: J03 e J04.
- Integrações, sincronizações, falhas e propagação: J04 e J05.
- Conteúdo, publicidade e estados público/restrito/interno: J06.
- Logs, auditoria, acessos, backup e recuperação: J02, J03, J04, J05, J06 e J07.

Não foi identificada jornada sem necessidade da persona. Privilégio administrativo não remove limites de permissão por função nem salvaguardas para auditoria e operações de alto impacto.
