# Requisitos Funcionais

## Rastreabilidade e escopo

Este documento deriva exclusivamente das necessidades e jornadas descritas em:

- [Jornadas do Torcedor](../jornadas/TORCEDOR_JORNADAS.md)
- [Jornadas do Administrador](../jornadas/ADMINISTRADOR_JORNADAS.md)
- [Jornadas do Investidor](../jornadas/INVESTIDOR_JORNADAS.md)
- Personas-fonte em [PRD/personas/](../personas/)

Os requisitos descrevem comportamento do produto sem definir linguagem, framework, banco, provedor, arquitetura ou API. **P0** indica comportamento essencial às jornadas centrais; **P1**, aprofundamento operacional/comercial importante; **P2**, capacidade complementar que pode ser escalonada após os fluxos essenciais.

## RF-001 — Identificar usuários e controlar sessão

- **Nome:** Autenticação, sessão e encerramento de acesso.
- **Descrição:** A aplicação deve permitir cadastro/entrada, validar identidade e estado da conta, iniciar sessão autorizada, recuperar acesso sem revelar a existência da conta e encerrar a sessão por logout.
- **Persona relacionada:** Torcedor, Administrador, Investidor/Parceiro.
- **Jornada de origem:** Torcedor J01–J02; Administrador J01; Investidor J01.
- **Prioridade:** P0.
- **Comportamento esperado:** Após autenticação válida, carregar identidade/perfil e escopo correspondente; em logout, invalidar a sessão. Recuperação fornece resposta neutra sobre existência de conta.
- **Entradas:** Dados de identificação, credenciais, solicitação de recuperação e sessão atual.
- **Saídas:** Resultado de autenticação, estado/escopo da sessão e instruções de recuperação.
- **Regras relacionadas:** Papéis e permissões são distintos; consulta pública pode ser anônima; dados comerciais/administrativos exigem autorização.
- **Exceções relevantes:** Credenciais inválidas, conta suspensa, sessão expirada, falha de recuperação e falha ao encerrar sessão.

## RF-002 — Gerenciar preferências do torcedor

- **Nome:** Persistir clube, jogadores e partidas favoritos.
- **Descrição:** A aplicação deve permitir ao torcedor selecionar e alterar seu clube favorito, jogadores favoritos e partidas acompanhadas; preferências persistentes devem pertencer à própria conta.
- **Persona relacionada:** Torcedor.
- **Jornada de origem:** Torcedor J01–J02 e J06.
- **Prioridade:** P1.
- **Comportamento esperado:** Usuário autenticado recupera e altera preferências; visitante pode consultar conteúdo público e recebe indicação de que o estado temporário não é persistente.
- **Entradas:** Usuário autenticado, identificadores de clube/jogador/partida e ação de inclusão/remoção.
- **Saídas:** Preferências atuais e confirmação do estado persistido.
- **Regras relacionadas:** Somente o proprietário da conta altera preferências; entidades devem estar disponíveis publicamente.
- **Exceções relevantes:** Entidade removida/inexistente, preferência duplicada e falha ao salvar.

## RF-003 — Apresentar dashboard do clube

- **Nome:** Resumo de campanha e classificação.
- **Descrição:** A aplicação deve apresentar posição, pontos, jogos, vitórias, empates, derrotas, gols feitos/sofridos, saldo, aproveitamento, situação no campeonato, últimos/próximos jogos e principais jogadores disponíveis.
- **Persona relacionada:** Torcedor.
- **Jornada de origem:** Torcedor J01 e J03.
- **Prioridade:** P0.
- **Comportamento esperado:** Consolidar apenas dados válidos da competição e temporada exibidas e mostrar atualização, disponibilidade e cobertura.
- **Entradas:** Clube, campeonato, temporada e registros de partidas/classificação.
- **Saídas:** Resumo rotulado e navegável para detalhes.
- **Regras relacionadas:** Partidas não finalizadas não contam como resultado final; saldo = gols feitos menos gols sofridos; aproveitamento informa base de cálculo.
- **Exceções relevantes:** Início de campeonato, dados parciais, clubes/campeonato sem publicação e fonte indisponível.

## RF-004 — Consultar estatísticas e evolução do clube

- **Nome:** Indicadores gerais, mandante, visitante e forma recente.
- **Descrição:** Permitir consultar desempenho geral e segmentado por mando, gols/médias, aproveitamento, sequência, forma recente e evolução no campeonato.
- **Persona relacionada:** Torcedor.
- **Jornada de origem:** Torcedor J04.
- **Prioridade:** P0.
- **Comportamento esperado:** Filtros selecionados ficam explícitos; métricas indicam período, partidas consideradas, denominador, fonte e atualização.
- **Entradas:** Clube, competição, temporada, período, recorte mandante/visitante e partidas válidas.
- **Saídas:** Indicadores e séries de evolução interpretáveis.
- **Regras relacionadas:** Comparações usam critérios equivalentes; ausência não equivale a zero; forma recente indica tamanho da amostra.
- **Exceções relevantes:** Sem partidas, cobertura parcial, amostra insuficiente e falha de consulta.

## RF-005 — Consultar calendário e detalhe das partidas

- **Nome:** Últimos jogos, próximos jogos e estatísticas de partida.
- **Descrição:** Apresentar adversário, placar/estado, rodada, local, data, horário e estádio, além de jogadores e estatísticas disponíveis.
- **Persona relacionada:** Torcedor.
- **Jornada de origem:** Torcedor J03 e J05.
- **Prioridade:** P0.
- **Comportamento esperado:** Separar passado/futuro/estado especial e carregar estatísticas detalhadas sem mascarar atualização pendente.
- **Entradas:** Clube, temporada e identificador de partida.
- **Saídas:** Listagem e detalhe da partida com estado, dados disponíveis e metadados de atualização.
- **Regras relacionadas:** Placar futuro/parcial não pode aparecer como final; partidas adiadas/canceladas devem ter estado identificado.
- **Exceções relevantes:** Horário/estádio pendente, estatísticas ainda não recebidas, partida não pública e fonte indisponível.

## RF-006 — Consultar perfil e desempenho dos jogadores

- **Nome:** Elenco, perfil e estatísticas individuais.
- **Descrição:** Permitir consultar nome/posição e jogos, minutos, gols, assistências, cartões, score, avaliação média, desempenho recente, melhor/pior partida e destaque do clube no campeonato quando calculáveis.
- **Persona relacionada:** Torcedor.
- **Jornada de origem:** Torcedor J06.
- **Prioridade:** P0.
- **Comportamento esperado:** Apresentar período, competição, denominadores, cobertura e explicação dos scores; distinguir zero, ausência e não aplicável.
- **Entradas:** Clube, jogador, competição, temporada, participações e estatísticas.
- **Saídas:** Perfil e métricas individuais contextualizados.
- **Regras relacionadas:** Métricas devem pertencer a contexto compatível; melhor/pior partida e destaque do clube exigem critério identificado e amostra suficientes.
- **Exceções relevantes:** Jogador sem partidas, estatísticas parciais, vínculo histórico, perfil não encontrado.

## RF-007 — Comparar clubes

- **Nome:** Comparação esportiva de clubes.
- **Descrição:** Permitir comparação de posição, pontos, vitórias, derrotas, gols, saldo, aproveitamento, últimos cinco jogos, forma, jogadores e confrontos recentes.
- **Persona relacionada:** Torcedor.
- **Jornada de origem:** Torcedor J07.
- **Prioridade:** P1.
- **Comportamento esperado:** Apresentar clubes lado a lado e sinalizar diferenças de período, cobertura, denominador e contexto dos confrontos diretos.
- **Entradas:** Dois clubes distintos, competição, temporada/período e indicadores.
- **Saídas:** Indicadores comparativos, cobertura e contexto.
- **Regras relacionadas:** Usar unidades, definição e período equivalentes; não calcular diferenças sem base válida.
- **Exceções relevantes:** Dados parciais, sem confrontos recentes, filtros incompatíveis ou falha parcial.

## RF-008 — Apresentar previsões como estimativas

- **Nome:** Previsões de partida e campeonato.
- **Descrição:** Disponibilizar probabilidades de vitória/empate/derrota, chances de título/vagas continentais/rebaixamento e projeções de posição/pontuação final conforme dados e cenários disponíveis.
- **Persona relacionada:** Torcedor.
- **Jornada de origem:** Torcedor J08.
- **Prioridade:** P1.
- **Comportamento esperado:** Exibir rótulo “Estimativa baseada em dados”, escopo, instante do cálculo, dados/cobertura usados e aviso de que não há garantia de resultado.
- **Entradas:** Classificação atual, desempenho recente, partidas realizadas/restantes, adversários e histórico/estatísticas disponíveis.
- **Saídas:** Estimativas de partida e campeonato, estado de disponibilidade e data de cálculo.
- **Regras relacionadas:** Previsão não altera resultado observado; não publicar projeção conclusiva com entradas insuficientes; identificar dado desatualizado.
- **Exceções relevantes:** Dados insuficientes, cálculo indisponível, entrada alterada sem recálculo, partida/campeonato não encontrado.

## RF-009 — Exibir estados dos dados esportivos

- **Nome:** Atualização, origem e cobertura de informações esportivas.
- **Descrição:** A aplicação deve indicar estado de atualização e disponibilidade para dados esportivos, incluindo origem e horário quando disponíveis.
- **Persona relacionada:** Torcedor.
- **Jornada de origem:** Torcedor J01, J03–J09.
- **Prioridade:** P0.
- **Comportamento esperado:** Distinguir sucesso atual, atraso, cobertura parcial, ausência de dados e falha da fonte.
- **Entradas:** Metadados de atualização, origem, cobertura e estado de sincronização.
- **Saídas:** Estado visível e contextualizado por conjunto de dados.
- **Regras relacionadas:** Indisponível/desatualizado não equivale a zero ou a resultado atual.
- **Exceções relevantes:** Metadados de origem desconhecidos; exibir indisponibilidade sem inventar origem.

## RF-010 — Administrar contas, papéis e permissões

- **Nome:** Gestão de usuários e escopos de acesso.
- **Descrição:** Administrador autorizado deve poder criar, consultar, alterar, suspender/remover usuários e conceder/revisar permissões compatíveis com papéis e vínculos.
- **Persona relacionada:** Administrador.
- **Jornada de origem:** Administrador J02.
- **Prioridade:** P0.
- **Comportamento esperado:** Aplicar privilégio mínimo e refletir revogação/alteração de acesso, com confirmação de ações críticas.
- **Entradas:** Usuário, papel, permissões, vínculo, estado, operador e confirmação.
- **Saídas:** Estado de conta/permissões e confirmação ou erro.
- **Regras relacionadas:** Operador não concede privilégio acima de sua autoridade; parceiro tem escopo limitado; torcedor não gerencia dados oficiais.
- **Exceções relevantes:** Usuário duplicado, permissão conflitante, operador sem autoridade e conflito concorrente.

## RF-011 — Auditar operações administrativas importantes

- **Nome:** Trilha de auditoria atribuível.
- **Descrição:** Registrar para alteração administrativa importante o usuário responsável, ação, informação anterior e nova, data/hora, entidade afetada e resultado.
- **Persona relacionada:** Administrador.
- **Jornada de origem:** Administrador J02–J07.
- **Prioridade:** P0.
- **Comportamento esperado:** Disponibilizar histórico autorizado e impedir que o operador apague a trilha da própria ação.
- **Entradas:** Ator autenticado, ação, entidade, valores antes/depois, instante e resultado.
- **Saídas:** Evento de auditoria pesquisável e associado à entidade.
- **Regras relacionadas:** Ação sensível só é concluída como sucesso se o registro de auditoria exigido também for concluído.
- **Exceções relevantes:** Falha ao registrar evento, acesso não autorizado ao histórico e informação que precise ser ocultada por privacidade.

## RF-012 — Pesquisar e manter dados esportivos

- **Nome:** Gestão de clubes, jogadores, campeonatos, rodadas, partidas e estatísticas.
- **Descrição:** Permitir administradores autorizados criar, consultar, corrigir, editar, arquivar e publicar dados esportivos com busca, relações e estados claros.
- **Persona relacionada:** Administrador.
- **Jornada de origem:** Administrador J03.
- **Prioridade:** P0.
- **Comportamento esperado:** Validar campos, relações, duplicidade e estado antes de persistir; apresentar histórico e estado de publicação.
- **Entradas:** Entidade, campos, relações, origem, ação e justificativa quando requerida.
- **Saídas:** Registro atualizado, validações, estado de publicação e propagação.
- **Regras relacionadas:** Informação não confirmada não é oficial; histórico anterior deve ser preservado; registros históricos relacionados não são removidos de forma inconsistente.
- **Exceções relevantes:** Duplicidade, fonte divergente, relação inválida, falta de permissão e falha de propagação.

## RF-013 — Detectar e resolver inconsistências

- **Nome:** Investigação e reconciliação de dados.
- **Descrição:** Permitir localizar inconsistências/duplicidades, comparar origem e histórico, registrar decisão e acompanhar correção e propagação.
- **Persona relacionada:** Administrador.
- **Jornada de origem:** Administrador J03–J04.
- **Prioridade:** P1.
- **Comportamento esperado:** Não consolidar ou descartar dados sem decisão autorizada e rastreável; manter incidentes inconclusivos abertos.
- **Entradas:** Alerta, registros conflitantes, evidências, decisão e justificativa.
- **Saídas:** Estado resolvido/pendente, alteração auditada e status de propagação.
- **Regras relacionadas:** Conflitos de fonte externa não são sobrescritos silenciosamente; dado parcialmente propagado não é marcado como totalmente atualizado.
- **Exceções relevantes:** Evidência indisponível, resolução parcial, falha ao gravar ou propagar.

## RF-014 — Monitorar fontes externas e sincronizações

- **Nome:** Acompanhar estado e execução de integrações conceituais.
- **Descrição:** Exibir estado, última execução, erros, tentativas, registros afetados e permitir repetição/reprocessamento controlado a operadores autorizados.
- **Persona relacionada:** Administrador.
- **Jornada de origem:** Administrador J01 e J05.
- **Prioridade:** P1.
- **Comportamento esperado:** Distinguir execução bem-sucedida sem dados novos, atraso, falha e processamento parcial; evitar efeitos duplicados.
- **Entradas:** Fonte/integração, período, execução, entidade e solicitação de reprocessamento.
- **Saídas:** Histórico, estado, erro/contexto e resultado de nova tentativa.
- **Regras relacionadas:** Reprocessar não duplica registros; estado de execução não implica atualização de todas as entidades.
- **Exceções relevantes:** Estado indisponível, execução em progresso, falha parcial e operador não autorizado.

## RF-015 — Controlar conteúdo e visibilidade

- **Nome:** Gerenciar conteúdo público, restrito e interno.
- **Descrição:** Permitir a administradores autorizados revisar e alterar conteúdo/estado de publicação, com escopo, histórico e confirmação quando a visibilidade aumentar.
- **Persona relacionada:** Administrador.
- **Jornada de origem:** Administrador J06.
- **Prioridade:** P1.
- **Comportamento esperado:** Impedir acesso público a conteúdo restrito e diferenciar rascunho, agendado, publicado e encerrado.
- **Entradas:** Conteúdo, entidade associada, escopo, período, estado e autorização.
- **Saídas:** Conteúdo e visibilidade efetivos, auditoria e estado de propagação.
- **Regras relacionadas:** Conteúdo esportivo não validado não é oficial; alterações importantes são auditáveis.
- **Exceções relevantes:** Conflito de período, falta de permissão, dependência pendente e falha de propagação.

## RF-016 — Administrar publicidade e campanhas

- **Nome:** Configurar estado e escopo de campanhas.
- **Descrição:** Permitir gestão autorizada de conteúdo publicitário/campanhas, período, clube, áreas de exibição e visibilidade.
- **Persona relacionada:** Administrador.
- **Jornada de origem:** Administrador J06; Investidor J04.
- **Prioridade:** P1.
- **Comportamento esperado:** Registrar alterações e permitir que parceiros vejam somente campanhas autorizadas; publicidade não deve obstruir tarefas centrais do torcedor.
- **Entradas:** Campanha, clube, espaço/área, público, período e estado.
- **Saídas:** Estado efetivo, escopo autorizado e confirmação/auditoria.
- **Regras relacionadas:** Acesso do parceiro limitado ao vínculo; campanha deve ser identificável e respeitar escopo.
- **Exceções relevantes:** Campanha em conflito, período inválido, propagação não confirmada e usuário sem permissão.

## RF-017 — Consultar logs, métricas operacionais e auditoria

- **Nome:** Busca operacional com controle de escopo.
- **Descrição:** Permitir consulta de logs, acessos autorizados, eventos administrativos e métricas gerais com filtros e permissões.
- **Persona relacionada:** Administrador.
- **Jornada de origem:** Administrador J01 e J07.
- **Prioridade:** P1.
- **Comportamento esperado:** Mostrar ator, ação, entidade, resultado e contexto permitido; minimizar dados pessoais.
- **Entradas:** Intervalo, entidade, ator, categoria, resultado e identidade/permissão do administrador.
- **Saídas:** Eventos/métricas agregados e metadados de cobertura/atualização.
- **Regras relacionadas:** Logs individuais são restritos por finalidade; auditoria não pode ser apagada pelo autor.
- **Exceções relevantes:** Nenhum evento, consulta falha, campos ocultados por privacidade e intervalo não autorizado.

## RF-018 — Acompanhar backup e recuperação

- **Nome:** Consultar e operar procedimentos de recuperação autorizados.
- **Descrição:** Apresentar estado, verificação e resultado das rotinas de backup/recuperação; permitir ação de recuperação apenas a operadores autorizados, com escopo e confirmação.
- **Persona relacionada:** Administrador.
- **Jornada de origem:** Administrador J07.
- **Prioridade:** P1.
- **Comportamento esperado:** Distinguir cópia existente de recuperação verificada e informar execução parcial/falha.
- **Entradas:** Rotina, escopo, operador e confirmação.
- **Saídas:** Estado, cobertura, resultado e evento auditável.
- **Regras relacionadas:** Ação de alto impacto exige autorização e trilha de auditoria.
- **Exceções relevantes:** Estado não confirmado, verificação indisponível, recuperação parcial ou falha.

## RF-019 — Consultar dashboard comercial agregado

- **Nome:** Indicadores gerais de audiência.
- **Descrição:** Disponibilizar acessos, usuários únicos/recorrentes, crescimento, tempo médio, páginas acessadas, páginas por usuário, clubes mais acessados e clubes com maior crescimento dentro do escopo do parceiro.
- **Persona relacionada:** Investidor/Parceiro Comercial.
- **Jornada de origem:** Investidor J01.
- **Prioridade:** P0.
- **Comportamento esperado:** Aplicar filtros, definições, denominadores e cobertura; retornar somente dados agregados.
- **Entradas:** Período, clube/campanha autorizados e métricas de audiência.
- **Saídas:** Indicadores, variações, ordenações comparáveis de clubes e metadados de período/fonte/atualização.
- **Regras relacionadas:** Sem PII; crescimento requer base válida; ausência de dados não equivale a zero.
- **Exceções relevantes:** Conta sem escopo, período vazio, métrica sem denominador e falha parcial.

## RF-020 — Analisar audiência por clube, conteúdo e jogador

- **Nome:** Segmentação comercial por clube.
- **Descrição:** Permitir análise agregada de audiência, engajamento, crescimento, conteúdos e jogadores mais visualizados por clube autorizado.
- **Persona relacionada:** Investidor/Parceiro Comercial.
- **Jornada de origem:** Investidor J02.
- **Prioridade:** P1.
- **Comportamento esperado:** Expor período, fonte e cobertura e impedir inferência de identidade individual.
- **Entradas:** Clube, período e dimensão (conteúdo, página, jogador).
- **Saídas:** Indicadores agregados e tendências.
- **Regras relacionadas:** Escopo por clube aplicado no servidor; tendência não implica causalidade.
- **Exceções relevantes:** Cobertura parcial, clube não autorizado, ausência de integração social e resultado vazio.

## RF-021 — Comparar métricas comerciais

- **Nome:** Comparação de clubes e períodos.
- **Descrição:** Permitir comparar clubes e períodos com variação absoluta/percentual e contexto de definições, duração, denominadores e cobertura.
- **Persona relacionada:** Investidor/Parceiro Comercial.
- **Jornada de origem:** Investidor J03.
- **Prioridade:** P1.
- **Comportamento esperado:** Comparar somente dimensões compatíveis ou explicar diferenças e impedir percentual sem base válida.
- **Entradas:** Clubes, períodos e indicadores autorizados.
- **Saídas:** Valores comparativos, variações e limitações.
- **Regras relacionadas:** Definição e base de comparação devem ser explícitas; autorização aplicada a todos os lados.
- **Exceções relevantes:** Períodos incompatíveis, cobertura desigual, lado indisponível e denominador inválido.

## RF-022 — Consultar métricas de campanhas

- **Nome:** Desempenho de publicidade autorizada.
- **Descrição:** Exibir campanhas, período, clube, espaço de exibição, impressões, alcance, cliques, CTR, engajamento e desempenho disponíveis.
- **Persona relacionada:** Investidor/Parceiro Comercial.
- **Jornada de origem:** Investidor J04.
- **Prioridade:** P1.
- **Comportamento esperado:** Filtrar campanhas autorizadas e identificar definição/denominador de CTR, fonte, cobertura e atualização.
- **Entradas:** Campanha, período, clube e espaço de exibição dentro do escopo.
- **Saídas:** Indicadores e tendências de campanha.
- **Regras relacionadas:** Métricas ausentes não são zero; parceiro não acessa campanhas de terceiros.
- **Exceções relevantes:** Sem impressões, fonte indisponível, campanha inexistente/não autorizada e período parcialmente coberto.

## RF-023 — Consultar métricas sociais externas

- **Nome:** Indicadores agregados de redes sociais.
- **Descrição:** Quando dados estiverem disponíveis, apresentar seguidores, crescimento, publicações, curtidas, comentários, compartilhamentos, visualizações e taxa de engajamento.
- **Persona relacionada:** Investidor/Parceiro Comercial.
- **Jornada de origem:** Investidor J05.
- **Prioridade:** P2.
- **Comportamento esperado:** Identificar origem externa, cobertura e atualização e separar da audiência interna.
- **Entradas:** Clube, período e métricas fornecidas por fonte externa conceitual.
- **Saídas:** Indicadores sociais ou estado explícito de indisponibilidade.
- **Regras relacionadas:** Integração ausente não se representa como zero; taxas declaram denominador.
- **Exceções relevantes:** Fonte atrasada, cobertura parcial, clube não coberto e métricas inconsistentes.

## RF-024 — Consultar ranking de engajamento

- **Nome:** Ranking comparável de clubes.
- **Descrição:** Recuperar indicadores agregados, calcular score segundo regra de negócio aprovada posteriormente e ordenar clubes com critérios e cobertura visíveis.
- **Persona relacionada:** Investidor/Parceiro Comercial.
- **Jornada de origem:** Investidor J06.
- **Prioridade:** P2.
- **Comportamento esperado:** Apresentar período, fontes, dimensões, score e cobertura; não tratar fórmula ainda não aprovada como definitiva.
- **Entradas:** Período, clubes e acessos/interações/visualizações/crescimento/métricas sociais disponíveis.
- **Saídas:** Ranking, score, critério aplicado e limitações.
- **Regras relacionadas:** Fórmula do score ainda não definida; cobertura desigual deve ser explícita; empates precisam de regra aprovada.
- **Exceções relevantes:** Dados insuficientes, fontes indisponíveis, escopo parcial e critério não aprovado.

## RF-025 — Gerar relatórios comerciais autorizados

- **Nome:** Relatórios e exportação de métricas agregadas.
- **Descrição:** Permitir montar prévia e exportar indicadores com filtros, período, definições, fontes, atualização e limitações visíveis.
- **Persona relacionada:** Investidor/Parceiro Comercial.
- **Jornada de origem:** Investidor J03–J07.
- **Prioridade:** P1.
- **Comportamento esperado:** Revalidar escopo na geração, respeitar filtros e impedir exportação de dados pessoais, logs ou campanhas não autorizadas.
- **Entradas:** Período, clubes/campanhas, métricas e parâmetros autorizados.
- **Saídas:** Prévia e saída agregada autorizada.
- **Regras relacionadas:** Exportação não amplia permissão; relatórios devem ser interpretáveis e reproduzíveis.
- **Exceções relevantes:** Permissão revogada, cobertura insuficiente, falha de geração e dados alterados após prévia.

## RF-026 — Tratar estados de carregamento, ausência e falha

- **Nome:** Estados e feedback das jornadas.
- **Descrição:** Toda consulta ou ação deve distinguir Loading, Empty State, Success, Error, Unauthorized, Not Found e dados desatualizados quando aplicável.
- **Persona relacionada:** Torcedor, Administrador, Investidor/Parceiro.
- **Jornada de origem:** Todas as jornadas; detalhado nas seções de estados dos três documentos.
- **Prioridade:** P0.
- **Comportamento esperado:** Mensagem coerente com resultado real; preservar filtros/seleções e não converter erro/ausência em sucesso ou zero.
- **Entradas:** Estado da solicitação, autorização, existência, cobertura e atualização.
- **Saídas:** Feedback e ação de recuperação adequada.
- **Regras relacionadas:** Nenhuma falha deve ser silenciosa nem produzir apresentação enganosa.
- **Exceções relevantes:** Falha parcial, resultado desconhecido após operação e metadados de atualização indisponíveis.

## RF-027 — Comparar jogadores

- **Nome:** Comparação de desempenho individual.
- **Descrição:** Permitir comparar jogadores por jogos, minutos, gols, assistências, cartões, score, avaliação média e forma recente em período/competição comparáveis.
- **Persona relacionada:** Torcedor.
- **Jornada de origem:** Torcedor J07.
- **Prioridade:** P1.
- **Comportamento esperado:** Exibir métricas equivalentes lado a lado, com amostra, denominadores, cobertura e diferenças de clube/posição quando relevantes.
- **Entradas:** Dois ou mais jogadores, competição, temporada/período e indicadores.
- **Saídas:** Comparação contextualizada ou indicação de métricas sem base comparável.
- **Regras relacionadas:** Médias/scores identificam critério e base; dados ausentes não equivalem a zero.
- **Exceções relevantes:** Jogador não público, atuação em contextos distintos, cobertura parcial e falha de consulta.

## Revisão cruzada e rastreabilidade

- Torcedor: comparar jogadores: Torcedor J07; RF-027.
- Torcedor: comparar clubes e períodos esportivos: Torcedor J08; RF-007.
- Torcedor: consultar previsão contextualizada e identificada como estimativa: Torcedor J09; RF-008.
- Os objetivos, necessidades e dores centrais de cada persona estão associados a pelo menos uma jornada e a requisitos de origem.
- O dashboard do clube e os dashboards comerciais funcionam como resumos e pontos de entrada; calendário, perfil, campanha e relatórios mantêm detalhes em jornadas próprias, evitando fluxos duplicados.
- Ações que alteram preferências, dados, permissões, conteúdo, campanhas ou exportações têm resultado explícito, e os fluxos comuns cobrem falha, ausência, acesso negado, não encontrado e dados desatualizados.
- As origens conceituais estão identificadas: fonte externa de dados esportivos, dados agregados internos de audiência/campanhas, registros administrativos e fonte externa de métricas sociais.
- Consultas, filtros, agregações/cálculos, persistência, autorização, auditoria e propagação de correções estão tratados como responsabilidades internas do sistema quando aplicáveis.
- Dados externos são tratados como fontes conceituais; fornecedores e APIs não foram escolhidos.
- Não há permissão para torcedor alterar dados esportivos, nem para investidor administrar operação ou consultar informação individual.
- Requisitos comerciais usam métricas agregadas e preservam escopo de campanhas e clubes.
- Regras de cálculo que ainda dependem de decisão de negócio (por exemplo, fórmula do score de engajamento) são explicitamente pendentes e não foram presumidas.
- Definições quantitativas de atualização, retenção, limiares de privacidade e condições para ranking devem ser acordadas antes de transformar os requisitos em critérios mensuráveis.
