# Jornadas do Torcedor

## Base e rastreabilidade

**Persona-fonte:** [TORCEDOR.md](../personas/TORCEDOR.md)

**Acesso:** usuário público de leitura; pode configurar seus próprios favoritos e preferências. Não pode alterar dados esportivos oficiais, previsões publicadas nem informações administrativas.

**Objetivo central:** acompanhar facilmente o clube, compreender seu desempenho e consultar estatísticas confiáveis de clubes, partidas e jogadores sem reunir informações em vários locais.

As jornadas abaixo traduzem os objetivos, necessidades e dores descritos na persona em interações observáveis e processamento interno. Dados de partidas, campeonatos, clubes, jogadores e estatísticas podem depender de uma **fonte externa de dados esportivos**; a aplicação deve identificar origem e atualização quando disponíveis e não tratar indisponibilidade como valor zero.

## J01 — Primeiro acesso, identificação e personalização

### Persona
Torcedor.

### Objetivo
Conhecer a aplicação e chegar rapidamente às informações do clube que acompanha, com ou sem criação de conta.

### Relação com a persona
- **Objetivo atendido:** escolher um clube favorito e acompanhar sua campanha.
- **Necessidade atendida:** resumo direto e acesso rápido a informações atualizadas.
- **Dor reduzida:** ter de reunir informações em vários serviços e perder preferências entre sessões.

### Pré-condições
- A aplicação está disponível.
- Existe uma lista de clubes que podem ser acompanhados; se ainda não houver dados, a aplicação deve informar isso.
- Criar uma conta é opcional para consultar conteúdo público; autenticação é necessária para persistir preferências associadas ao usuário.

### Gatilho
O torcedor abre a aplicação pela primeira vez ou inicia a configuração de sua experiência.

### Fluxo principal
1. A aplicação apresenta sua finalidade, a opção de entrar/criar conta e uma forma de continuar como visitante.
2. O torcedor escolhe entrar, criar uma conta ou continuar sem autenticação.
3. Se criar uma conta, informa os dados solicitados; se entrar, informa as credenciais de acesso.
4. O sistema valida os dados de identificação e cria ou recupera a sessão e o perfil autorizado.
5. O sistema apresenta a lista de clubes disponíveis para acompanhamento.
6. O torcedor seleciona o clube favorito.
7. A interface confirma a seleção; o sistema registra a preferência no perfil autenticado ou a mantém apenas durante a experiência de visitante.
8. A aplicação carrega e apresenta o dashboard do clube, exibindo a atualização e a disponibilidade dos dados.

### Responsabilidade do Front-end
- Explicar opções de acesso, cadastro e navegação como visitante.
- Solicitar apenas os dados necessários para identificação e permitir correção de campos inválidos.
- Apresentar clubes pesquisáveis e estados sem clubes disponíveis.
- Permitir escolher, alterar e confirmar o clube favorito.
- Apresentar feedback de carregamento, sucesso e falha sem bloquear desnecessariamente a consulta pública.
- Informar quando a preferência do visitante não será preservada após a sessão.

### Responsabilidade do Back-end
- Validar dados de cadastro e autenticação e aplicar as regras vigentes de identificação.
- Criar ou recuperar a sessão e associá-la a um perfil de torcedor, sem atribuir permissões administrativas ou comerciais.
- Retornar somente clubes disponíveis para consulta pública.
- Registrar a preferência para usuários autenticados e retornar a preferência previamente salva quando houver.
- Disponibilizar os dados do clube e metadados de origem, atualização e cobertura.
- Não persistir como preferência permanente a seleção feita por visitante, salvo se houver consentimento e mecanismo definido para isso.

### Dados envolvidos
- Dados de identificação e credenciais; identificador e estado da sessão; perfil e preferências do usuário.
- Identificador, nome e disponibilidade pública do clube selecionado.
- Classificação, campanha, estatísticas resumidas e metadados de atualização do clube.

### Regras envolvidas
- Consulta a informações públicas não exige perfil comercial ou administrativo.
- Preferências vinculadas à conta só podem ser consultadas ou alteradas pelo próprio usuário.
- Não se deve informar existência de dados de clube não publicado ou restrito a usuário sem autorização.
- Falta de dados esportivos deve ser identificada como indisponibilidade ou ausência de cobertura, nunca como zero.

### Validações
- Campos obrigatórios, formato dos dados de cadastro e credenciais.
- Sessão válida para associar preferências à conta.
- Clube selecionado existente e disponível para consulta pública.

### Fluxos alternativos
- O torcedor continua como visitante e escolhe um clube; a aplicação oferece a experiência pública sem prometer persistência entre sessões.
- O torcedor já possui preferência salva; o sistema a recupera e permite confirmá-la ou escolher outro clube.
- A lista contém muitos clubes; o torcedor pesquisa ou filtra antes de selecionar.

### Fluxos de erro
- Credenciais ou dados de cadastro inválidos: informar o campo ou ação que precisa ser corrigida sem revelar dados sensíveis.
- Falha ao salvar preferência: informar que a consulta pode continuar, mas que a preferência não foi persistida.
- Lista de clubes indisponível: apresentar erro recuperável e opção de tentar novamente.
- Dados esportivos indisponíveis: apresentar o clube e indicar que os dados não puderam ser carregados, se houver dados cadastrais públicos disponíveis.

### Resultado esperado
O torcedor chega ao dashboard do clube escolhido. A preferência é persistida apenas quando autenticado e o estado dos dados apresentados é transparente.

## J02 — Entrar, sair, recuperar acesso e gerenciar preferências

### Persona
Torcedor autenticado.

### Objetivo
Manter acesso seguro à própria conta e controlar clube, jogadores e partidas acompanhados.

### Relação com a persona
- **Objetivo atendido:** acompanhar clube e jogadores favoritos.
- **Necessidade atendida:** voltar facilmente às informações que acompanha.
- **Dores reduzidas:** perda de preferências entre sessões e dificuldade de acesso.

### Pré-condições
- Para gerenciar preferências persistentes, o torcedor possui uma conta.
- Para recuperar acesso, há um identificador de conta previamente cadastrado.

### Gatilho
O torcedor seleciona entrar, sair, recuperar acesso ou gerenciar seus acompanhamentos.

### Fluxo principal
1. O torcedor inicia uma ação de acesso ou abre suas preferências.
2. Para entrar, informa credenciais; para recuperação, informa o identificador solicitado; para preferências, a aplicação verifica a sessão atual.
3. O sistema valida a solicitação, autentica ou inicia o fluxo de recuperação e aplica as permissões do perfil.
4. O sistema recupera preferências associadas à conta.
5. O torcedor adiciona, remove ou troca clube favorito, jogadores favoritos e partidas acompanhadas.
6. A interface mostra o estado atualizado; o sistema persiste as alterações e devolve confirmação.
7. Ao sair, o torcedor solicita logout; o sistema encerra a sessão e a interface remove o estado autenticado.

### Responsabilidade do Front-end
- Oferecer entrada, saída e recuperação de acesso em pontos compreensíveis.
- Mostrar os acompanhamentos atuais e permitir alterar somente preferências próprias.
- Explicar quando uma ação exige autenticação e preservar, quando possível, a intenção do usuário após entrar.
- Solicitar confirmação em ações que removam um acompanhamento, sem tornar a navegação confusa.
- Exibir confirmação de persistência e estado final da sessão.

### Responsabilidade do Back-end
- Validar credenciais, estado da conta e validade da sessão.
- Conduzir recuperação sem revelar se um identificador pertence a uma conta.
- Encerrar a sessão ao receber logout e rejeitar o uso posterior de sessão encerrada.
- Autorizar leitura e alteração somente das preferências do próprio usuário.
- Persistir alterações de clube, jogador e partida acompanhados e retornar o estado resultante.
- Registrar eventos de acesso relevantes segundo as regras de privacidade e segurança.

### Dados envolvidos
- Credenciais, identificador de usuário, estado e validade de sessão.
- Preferências: clube, jogadores e partidas acompanhados.
- Solicitação e estado do processo de recuperação.

### Regras envolvidas
- O torcedor não pode alterar dados esportivos oficiais nem preferências de outra conta.
- A resposta do fluxo de recuperação deve ser neutra quanto à existência da conta.
- Logout encerra a sessão atual, sem excluir conta ou preferências.
- As preferências devem permanecer disponíveis após novo acesso autenticado.

### Validações
- Credenciais e sessão válidas.
- Identificadores de clube, jogador e partida existentes e disponíveis.
- Usuário autenticado como proprietário da preferência que será alterada.

### Fluxos alternativos
- O torcedor escolhe continuar sem conta; a experiência pública permanece disponível, mas a gestão persistente de favoritos requer autenticação.
- Solicitação de recuperação aceita: a interface informa os próximos passos sem confirmar existência de conta.
- Preferência já existe: a interface mantém o estado selecionado sem duplicar acompanhamento.

### Fluxos de erro
- Credenciais inválidas, conta indisponível ou sessão expirada: informar a condição e oferecer nova tentativa ou recuperação.
- Falha ao persistir preferências: manter o estado salvo anterior e sinalizar que a mudança não foi confirmada.
- Tentativa de alterar preferência de outra conta: negar a ação e preservar os dados existentes.
- Falha no logout: informar que o encerramento não foi confirmado e evitar apresentar a sessão como encerrada.

### Resultado esperado
O usuário acessa ou encerra sua própria sessão e mantém controle previsível das preferências que autorizou persistir.

## J03 — Consultar dashboard e situação do clube no campeonato

### Persona
Torcedor.

### Objetivo
Entender rapidamente a posição e a campanha atual do clube.

### Relação com a persona
- **Objetivo atendido:** acompanhar posição, pontuação, resultados e situação no campeonato.
- **Necessidade atendida:** resumo em linguagem direta, atualizado e contextualizado.
- **Dor reduzida:** informação espalhada ou sem indicação de atualização.

### Pré-condições
- O clube está selecionado ou a aplicação consegue oferecer uma seleção.
- Há campeonato e dados públicos associados, ou a aplicação consegue identificar ausência de dados.

### Gatilho
O torcedor abre o dashboard, retorna à aplicação ou troca de clube.

### Fluxo principal
1. O torcedor abre o dashboard do clube.
2. A interface solicita o resumo atual e exibe carregamento.
3. O sistema consulta campanha, classificação, partidas e estatísticas disponíveis para o campeonato e clube selecionados.
4. O sistema consolida jogos, vitórias, empates, derrotas, gols feitos e sofridos, saldo e aproveitamento com base em partidas válidas.
5. O sistema identifica últimos e próximos jogos, destaques de jogadores disponíveis, posição e situação no campeonato.
6. A interface apresenta indicadores rotulados, contexto do campeonato e horário/estado de atualização.
7. O torcedor abre um indicador ou link para consultar o detalhe correspondente.

### Responsabilidade do Front-end
- Hierarquizar posição, pontos, jogos, vitórias, empates, derrotas, gols feitos/sofridos, saldo e aproveitamento.
- Mostrar situação atual no campeonato, últimos jogos, próximos jogos e principais jogadores quando houver dados.
- Explicar rótulos e indicadores sem exigir conhecimento estatístico avançado.
- Oferecer navegação para estatísticas, partidas e jogadores.
- Sinalizar carregamento, atualização, dados desatualizados, cobertura parcial e ausência de dados.

### Responsabilidade do Back-end
- Consultar registros públicos do clube e do campeonato.
- Aplicar consistência temporal: incluir apenas partidas válidas segundo o estado oficial de cada partida e a rodada/campanha considerada.
- Calcular ou consolidar saldo, aproveitamento e totais da campanha com denominadores explícitos.
- Ordenar classificação segundo as regras do campeonato vigente, sem inferir regras não definidas.
- Selecionar os últimos e próximos jogos e os destaques apenas quando houver dados suficientes.
- Informar data/hora de atualização, origem conceitual, estado de sincronização e campos sem cobertura.

### Dados envolvidos
- Campeonato, temporada, rodada, tabela e critérios de classificação.
- Clube, partidas, placares, estado das partidas e estatísticas agregadas.
- Identificadores de jogadores e métricas de destaque.
- Fonte e data/hora de atualização, cobertura e estado de sincronização.

### Regras envolvidas
- Partidas não finalizadas não podem ser contabilizadas como resultado final.
- Empates, jogos adiados, anulados ou sem placar válido devem respeitar o estado oficial registrado.
- Saldo é gols feitos menos gols sofridos; aproveitamento deve informar o critério/denominador utilizado.
- Indicadores sem base de cálculo suficiente são apresentados como indisponíveis, não como zero.
- Previsões, se exibidas, devem ser claramente separadas de resultados observados.

### Validações
- Clube e campeonato selecionados são válidos e públicos.
- Os registros usados pertencem à mesma temporada e ao contexto apresentado.
- Somatórios e denominadores são compatíveis com o número e estado das partidas consideradas.

### Fluxos alternativos
- Ainda não há partidas na temporada: exibir a situação de início de campeonato e não calcular métricas sem base.
- O clube não tem preferência salva: solicitar seleção ou apresentar a lista pública de clubes.
- Apenas alguns indicadores estão disponíveis: apresentar os existentes e identificar cobertura parcial.

### Fluxos de erro
- Serviço de dados indisponível: preservar a navegação e informar indisponibilidade; dados em cache, se apresentados, devem ser marcados como desatualizados.
- Dados inconsistentes (por exemplo, total de partidas incompatível com partidas listadas): evitar publicar cálculo enganoso e sinalizar atualização/inconsistência.
- Clube/campeonato não encontrado ou não público: apresentar estado Not Found sem expor conteúdo restrito.

### Resultado esperado
O torcedor compreende a posição e a campanha do clube e sabe se os números são atuais, parciais ou indisponíveis.

## J04 — Explorar estatísticas, forma e evolução do clube

### Persona
Torcedor.

### Objetivo
Entender tendências e comparar o desempenho geral, como mandante, como visitante e ao longo do campeonato.

### Relação com a persona
- **Objetivo atendido:** compreender médias, desempenho em casa/fora e sequência de resultados.
- **Necessidade atendida:** estatísticas explicadas, gráficos legíveis e comparação consistente.
- **Dor reduzida:** dificuldade para interpretar métricas e comparar períodos incompatíveis.

### Pré-condições
- O clube e o campeonato estão selecionados.
- Há partidas válidas suficientes para uma ou mais métricas.

### Gatilho
O torcedor seleciona estatísticas, forma recente ou evolução no dashboard do clube.

### Fluxo principal
1. O torcedor escolhe uma visão (geral, mandante, visitante ou evolução) e, se disponível, período/recorte.
2. A interface solicita os dados e mostra carregamento.
3. O sistema recupera partidas e estatísticas válidas para o mesmo campeonato, temporada e recorte.
4. O sistema consolida gols, médias, aproveitamento, sequência e forma recente; define os jogos incluídos e o denominador.
5. O sistema prepara pontos da evolução por rodada/tempo e metadados de cobertura.
6. A interface apresenta os resultados com unidades, legenda, período, base de comparação e explicação dos indicadores.
7. O torcedor altera recorte ou abre uma partida para contextualizar um ponto da série.

### Responsabilidade do Front-end
- Permitir alternar entre desempenho geral, mandante e visitante.
- Permitir escolher os recortes de período disponíveis e indicar qual está ativo.
- Apresentar gols, médias, aproveitamento, sequência, forma recente e evolução em visualização responsiva.
- Mostrar o conjunto de partidas e o denominador que sustentam cada métrica, com explicação concisa.
- Distinguir dado observado de previsão e dado ausente de valor igual a zero.

### Responsabilidade do Back-end
- Filtrar as partidas pelo clube, competição, temporada, período, mando e estado oficial.
- Consolidar médias, aproveitamento, resultados sequenciais e pontos de evolução de forma reproduzível.
- Retornar denominadores, partidas consideradas, intervalo, origem e atualização.
- Detectar séries incompletas, amostras insuficientes e lacunas de cobertura.

### Dados envolvidos
- Partidas, datas, rodadas, mandante/visitante, placares e estatísticas de jogo.
- Período selecionado, sequência de resultados, gols, denominadores e agregados.
- Metadados de origem, atualização e completude.

### Regras envolvidas
- Recortes comparados usam a mesma competição e temporada salvo indicação explícita em contrário.
- Médias e percentuais sempre apresentam período e base de cálculo.
- Forma recente deve indicar quantas partidas compõem a amostra.
- Não se calcula tendência ou aproveitamento como se dados ausentes fossem partidas sem desempenho.

### Validações
- Período e filtros pertencem às opções suportadas.
- Mandante/visitante é definido pela relação da partida com o clube consultado.
- Quantidade de partidas e métricas calculadas são coerentes com os registros disponíveis.

### Fluxos alternativos
- O torcedor consulta apenas o desempenho geral, sem alterar filtros.
- A série histórica não cobre todas as rodadas: a interface identifica o intervalo coberto.
- A amostra é pequena: a aplicação apresenta os números disponíveis com aviso de amostra limitada.

### Fluxos de erro
- Filtros sem partidas: mostrar Empty State e permitir remover ou ampliar filtros.
- Falha de processamento/consulta: mostrar Error recuperável e preservar seleção de filtros.
- Fonte atrasada: sinalizar dados desatualizados e exibir a última atualização conhecida quando houver.

### Resultado esperado
O torcedor vê estatísticas interpretáveis e consegue entender período, cobertura e base dos cálculos.

## J05 — Consultar últimos jogos, próximos jogos e detalhes de uma partida

### Persona
Torcedor.

### Objetivo
Revisar resultados e calendário e aprofundar a análise de uma partida.

### Relação com a persona
- **Objetivo atendido:** consultar adversário, placar, rodada, local, data, horário, estádio, jogadores e estatísticas.
- **Necessidade atendida:** acesso rápido ao calendário e ao contexto do jogo.
- **Dor reduzida:** calendário ou estatísticas incompletas e desatualizadas.

### Pré-condições
- Um clube está selecionado.
- A partida, caso exista, tem estado e visibilidade compatíveis com consulta pública.

### Gatilho
O torcedor abre últimos jogos/próximos jogos ou seleciona uma partida.

### Fluxo principal
1. A interface solicita jogos recentes e futuros do clube.
2. O sistema recupera partidas por clube e temporada, separando partidas passadas, futuras e estados especiais.
3. A interface apresenta adversário, rodada, data, horário, local/estádio e placar quando aplicável.
4. O torcedor seleciona uma partida.
5. O sistema consulta o detalhe e consolida desempenho da partida, jogadores e estatísticas disponíveis.
6. A interface apresenta o detalhe, o estado da partida e o horário de atualização.

### Responsabilidade do Front-end
- Separar jogos anteriores, próximos e partidas com estado especial.
- Apresentar adversário, placar, rodada, data, horário, local e estádio quando disponíveis.
- Identificar fuso horário ou contexto temporal adotado para a exibição.
- Apresentar desempenho, escalações/jogadores e estatísticas somente quando disponíveis.
- Permitir navegar de uma partida a um perfil de jogador ou ao histórico do clube.

### Responsabilidade do Back-end
- Consultar calendário e resultados da temporada para o clube.
- Distinguir partida agendada, em andamento, finalizada, adiada, cancelada ou com estado equivalente registrado.
- Retornar placar somente conforme estado confirmado; evitar expor placar futuro ou parcial como definitivo.
- Consultar estatísticas e participantes associados à partida.
- Retornar origem, atualização e disponibilidade por conjunto de dados.

### Dados envolvidos
- Partida, rodada, temporada, data/hora, estádio/local, mandante, visitante, placar e estado.
- Jogadores participantes, desempenho e estatísticas da partida.
- Fonte e atualização.

### Regras envolvidas
- Data e horário não confirmados devem ser identificados como pendentes.
- Partida adiada ou cancelada não deve aparecer como jogo futuro confirmado nem como resultado concluído.
- Estatística individual só é apresentada quando associada à partida e à fonte correspondente.
- Métricas indisponíveis não equivalem a zero.

### Validações
- Partida pertence ao clube/temporada selecionados e está disponível para o público.
- Estado, placar e horário são coerentes com o registro atual.
- Não há duplicação de jogos na lista por fontes ou atualizações repetidas.

### Fluxos alternativos
- Não existem próximos jogos publicados: informar que o calendário ainda não está disponível.
- Partida futura ainda não tem estádio ou horário: apresentar os campos como não definidos.
- Estatísticas pós-jogo ainda não foram recebidas: mostrar resultado e indicar processamento/atualização pendente.

### Fluxos de erro
- Partida não encontrada ou sem visibilidade pública: Not Found.
- Falha ao carregar estatísticas: preservar dados básicos da partida e sinalizar que o detalhe estatístico não está disponível.
- Fonte externa indisponível ou atraso: identificar a última atualização conhecida e evitar apresentar o dado como atual.

### Resultado esperado
O torcedor encontra calendário e resultados com estado claro e consegue consultar o contexto disponível de uma partida.

## J06 — Consultar elenco, perfil e favoritos de jogadores

### Persona
Torcedor.

### Objetivo
Avaliar o desempenho e acompanhar jogadores do elenco.

### Relação com a persona
- **Objetivo atendido:** consultar jogos, minutos, gols, assistências, cartões, score, avaliação e forma.
- **Necessidade atendida:** perfil claro, destaques e opção de favoritar jogadores.
- **Dor reduzida:** pouca informação sobre contribuição individual e falta de comparabilidade.

### Pré-condições
- Um clube está selecionado e possui elenco público cadastrado.
- Estatísticas podem não estar disponíveis para todo jogador ou competição.

### Gatilho
O torcedor abre o elenco ou seleciona um jogador em uma partida, comparação ou dashboard.

### Fluxo principal
1. A aplicação apresenta o elenco público do clube com filtros disponíveis, como posição.
2. O torcedor seleciona um jogador.
3. O sistema recupera perfil, vínculo esportivo público e estatísticas da competição/temporada.
4. O sistema consolida jogos disputados, minutos, gols, assistências, cartões, score, avaliação média e desempenho recente.
5. Quando há base suficiente, o sistema identifica melhor e pior partida do jogador e o destaque do clube no campeonato segundo o indicador disponível.
6. A interface apresenta o perfil, período, definições dos indicadores e data de atualização.
7. O torcedor favorita ou remove dos favoritos; autenticado, o sistema persiste a preferência.

### Responsabilidade do Front-end
- Apresentar o elenco e permitir encontrar jogador por nome ou filtro disponível.
- Exibir posição e indicadores solicitados com período e unidade.
- Explicar score e avaliação sem apresentá-los como medida oficial quando não forem.
- Apresentar desempenho recente, melhor/pior partida e melhor jogador do clube no campeonato somente com amostra suficiente e critério identificado.
- Permitir favoritar e retirar favorito, apresentando claramente se a ação foi persistida.

### Responsabilidade do Back-end
- Retornar jogadores ativos/publicáveis do clube e dados de perfil autorizados.
- Consultar estatísticas por jogador, clube, competição, temporada e partida.
- Consolidar jogos, minutos, gols, assistências, cartões, score e avaliação média, retornando período e denominadores.
- Definir melhor/pior partida apenas dentro do critério de score/avaliação disponível e expor o contexto utilizado.
- Persistir favoritos do próprio usuário autenticado; para visitante, manter somente estado temporário.
- Preservar distinção entre dado ausente, não aplicável e zero registrado.

### Dados envolvidos
- Jogador, clube, posição, período, competição e temporada.
- Participações, minutos, gols, assistências, cartões, score, avaliações e partidas relacionadas.
- Preferência de favorito e metadados de fonte/atualização.

### Regras envolvidas
- Métricas de jogador devem pertencer ao mesmo período e contexto ou declarar explicitamente diferenças.
- Melhor/pior partida exige métrica e amostra válidas; empate de métrica deve ser tratado de forma consistente.
- O torcedor não pode modificar dados do perfil esportivo.
- Favoritos autenticados pertencem à conta que os criou.

### Validações
- Jogador existe, é público e pertence ou esteve vinculado ao clube no período exibido.
- Competição, temporada e partidas são compatíveis.
- Totais e médias têm denominadores disponíveis e coerentes.

### Fluxos alternativos
- Jogador ainda não disputou partidas: mostrar perfil e Empty State para indicadores de desempenho.
- O torcedor consulta perfil sem estar autenticado: permitir leitura pública, mas explicar que favorito persistente requer conta.
- Só há métricas parciais: apresentar as disponíveis e a cobertura faltante.

### Fluxos de erro
- Jogador removido, oculto ou inexistente: Not Found, sem expor dados restritos.
- Falha de estatísticas: preservar identificação pública do jogador e informar quais dados não foram carregados.
- Falha ao salvar favorito: reverter o estado visual ou indicar claramente que a operação não foi confirmada.

### Resultado esperado
O torcedor entende o desempenho disponível do jogador e pode voltar a ele por meio de um favorito persistente quando autenticado.

## J07 — Comparar jogadores

### Persona
Torcedor.

### Objetivo
Comparar jogadores usando indicadores e períodos equivalentes para compreender suas contribuições.

### Relação com a persona
- **Objetivo atendido:** comparar jogadores com critérios consistentes.
- **Necessidade atendida:** consultar estatísticas e avaliações de jogadores com contexto.
- **Dor reduzida:** dificuldade para comparar desempenho individual com métricas ou períodos incompatíveis.

### Pré-condições
- Há pelo menos dois jogadores públicos selecionáveis.
- Existem indicadores individuais para um mesmo período/contexto ou diferenças de cobertura podem ser explicadas.

### Gatilho
O torcedor seleciona a opção de comparação a partir do elenco ou de um perfil de jogador.

### Fluxo principal
1. O torcedor seleciona dois ou mais jogadores e a competição, temporada/período e indicadores disponíveis.
2. A interface mostra a seleção e solicita comparação.
3. O sistema valida jogadores, contexto, dados disponíveis e comparabilidade.
4. O sistema recupera jogos, minutos, gols, assistências, cartões, score, avaliação média e forma recente para cada jogador.
5. O sistema calcula ou consolida indicadores usando bases equivalentes e retorna amostras, denominadores, fontes e cobertura.
6. A interface apresenta os indicadores lado a lado e explica diferenças de clube, posição ou minutos quando relevantes.
7. O torcedor ajusta seleção/filtros ou abre o perfil de um jogador.

### Responsabilidade do Front-end
- Permitir selecionar jogadores e período/competição.
- Apresentar os mesmos indicadores, unidades e recortes para cada jogador.
- Explicar score/avaliação e informar quantidade de jogos/minutos considerados.
- Diferenciar falta de dados de zero e destacar cobertura desigual.
- Permitir navegar aos perfis e retornar à comparação.

### Responsabilidade do Back-end
- Validar jogadores públicos e recuperar métricas do período selecionado.
- Harmonizar filtros e definições sem misturar temporadas/contextos silenciosamente.
- Retornar denominadores, amostra, cobertura, origem e atualização por jogador.
- Impedir comparação conclusiva quando as bases forem incompatíveis.

### Dados envolvidos
- Jogadores, clubes, posições, competição, temporada, período, partidas e participações.
- Minutos, gols, assistências, cartões, score, avaliações e forma recente.
- Denominadores, origem, cobertura e atualização.

### Regras envolvidas
- Indicadores devem usar período e critério equivalentes; diferenças de clube/posição devem ser identificadas.
- Médias e scores informam amostra/base e não são apresentados como medida oficial sem esse contexto.
- Dados sem cobertura não equivalem a zero.

### Validações
- Jogadores distintos, públicos e com dados compatíveis.
- Período, competição e indicadores selecionados válidos.
- Denominadores presentes para qualquer taxa ou média comparada.

### Fluxos alternativos
- Um jogador tem dados parciais: exibir métricas comuns e marcar cobertura diferente.
- Jogadores atuaram por clubes distintos no período: explicitar vínculo e contexto de cada participação.
- Apenas estatísticas básicas estão disponíveis: comparar somente os indicadores comuns.

### Fluxos de erro
- Jogador não encontrado/não público: informar sem expor dado restrito.
- Nenhum indicador comparável: oferecer alteração de filtros sem calcular diferenças enganosas.
- Falha parcial: preservar indicadores válidos e identificar os blocos não carregados.

### Resultado esperado
O torcedor compara contribuições individuais de forma contextualizada e entende quando as bases não são equivalentes.

## J08 — Comparar clubes

### Persona
Torcedor.

### Objetivo
Comparar dois clubes em bases equivalentes e compreender diferenças de campanha e desempenho recente.

### Relação com a persona
- **Objetivo atendido:** comparar posição, pontos, resultados, gols, forma, jogadores e confrontos recentes.
- **Necessidade atendida:** comparação legível com mesmos períodos e indicadores.
- **Dor reduzida:** números incompatíveis ou espalhados em diferentes locais.

### Pré-condições
- Dois clubes públicos selecionáveis.
- Há competição, temporada e período comuns ou uma forma explícita de explicar diferenças de cobertura.

### Gatilho
O torcedor seleciona comparar clubes ou inicia a comparação a partir do dashboard.

### Fluxo principal
1. O torcedor seleciona clube A e clube B.
2. Escolhe período/competição disponíveis e indicadores de interesse.
3. A interface envia uma solicitação de comparação.
4. O sistema valida clubes e escopo, recupera os dados dos dois clubes e normaliza período, unidade e critérios.
5. O sistema consolida posição, pontos, vitórias, derrotas, gols, saldo, aproveitamento, últimos cinco jogos, forma recente e médias de jogadores.
6. O sistema recupera confrontos diretos recentes quando houver registros compatíveis.
7. A interface apresenta os dados lado a lado, cobertura, atualização e explicações.
8. O torcedor altera clube, período ou indicadores ou abre um detalhe.

### Responsabilidade do Front-end
- Permitir selecionar dois clubes distintos e filtros de período/competição.
- Apresentar os indicadores em paralelo com unidades, intervalos e denominadores.
- Diferenciar ausência de cobertura de valor zero e evidenciar diferenças de amostra.
- Mostrar últimos cinco jogos, forma recente, jogadores e confrontos diretos disponíveis.
- Permitir retornar aos detalhes de clube, jogo ou jogador.

### Responsabilidade do Back-end
- Validar que clubes e filtros são públicos e comparáveis.
- Recuperar dados para intervalos e competições coerentes.
- Calcular métricas usando critérios consistentes e retornar denominadores e cobertura de cada clube.
- Selecionar últimos cinco jogos de cada clube segundo ordenação temporal explícita.
- Recuperar confrontos diretos dentro do período e competição definidos ou identificar o contexto histórico utilizado.
- Não gerar comparação enganosa quando as bases não são equivalentes.

### Dados envolvidos
- Clubes, competição, temporadas, período, partidas, classificação e estatísticas.
- Jogadores e agregados correspondentes.
- Confrontos diretos e metadados de origem, atualização e cobertura.

### Regras envolvidas
- Indicadores equivalentes devem usar o mesmo período, competição, unidade e definição.
- Se cobertura ou quantidade de partidas diferir, a diferença deve ser declarada.
- Confrontos diretos devem identificar o intervalo/contexto utilizado.
- O usuário público só consulta dados esportivos publicáveis.

### Validações
- Seleção contém exatamente dois clubes válidos e distintos.
- Os filtros são permitidos e os períodos comparados são interpretáveis.
- Percentuais, médias e rankings possuem denominador/base expostos.

### Fluxos alternativos
- Um clube tem dados parciais: apresentar a comparação possível com alerta de cobertura.
- Não existem confrontos diretos recentes: apresentar Empty State específico sem interferir nos demais indicadores.
- O torcedor compara apenas os indicadores selecionados, mantendo período e base compartilhados.

### Fluxos de erro
- Clube/filtro inválido: destacar seleção que precisa ser corrigida.
- Falha parcial: manter os dados válidos identificados e informar quais blocos falharam.
- Nenhum dado comparável: não calcular diferença e oferecer alteração de filtros.

### Resultado esperado
O torcedor interpreta diferenças entre clubes sem confundir bases, períodos ou ausências de dados.

## J09 — Consultar previsões da partida e do campeonato

### Persona
Torcedor.

### Objetivo
Explorar cenários prováveis sem confundi-los com resultados oficiais ou garantidos.

### Relação com a persona
- **Objetivo atendido:** compreender chances de vitória/empate/derrota, título, vagas continentais, rebaixamento, posição e pontuação final.
- **Necessidade atendida:** estimativas contextualizadas, explicadas e atualizadas.
- **Dor reduzida:** previsões apresentadas como certezas ou sem contexto de incerteza.

### Pré-condições
- O campeonato ou partida está identificado.
- Há dados de entrada suficientes; as previsões são um recurso informativo, não uma promessa de resultado.

### Gatilho
O torcedor abre a área de previsões de uma partida ou campeonato.

### Fluxo principal
1. O torcedor escolhe uma partida ou cenário de campeonato.
2. A interface informa o escopo e solicita previsões disponíveis.
3. O sistema verifica disponibilidade e atualidade de classificação, resultados recentes, partidas realizadas/restantes, adversários e histórico/estatísticas disponíveis.
4. O sistema gera ou recupera estimativas para vitória/empate/derrota, chance de título, classificação para Libertadores/Sul-Americana, rebaixamento, posição e pontuação final, conforme aplicável.
5. O sistema associa às estimativas a data de cálculo, período, cobertura e dados utilizados.
6. A interface apresenta probabilidades/projeções com rótulo destacado **“Estimativa baseada em dados”**, contexto e aviso de incerteza.
7. Quando os dados mudam ou uma previsão está vencida, o sistema recalcula; a interface mostra atualização e eventual diferença em relação à previsão anterior, quando disponível.

### Responsabilidade do Front-end
- Separar visualmente estimativas de resultados registrados e dados oficiais.
- Exibir probabilidades de partida e cenários de campeonato aplicáveis, com contexto e data/hora do cálculo.
- Explicar quais categorias de dados foram consideradas e sinalizar cobertura insuficiente.
- Mostrar aviso de que estimativas não garantem resultados nem substituem informação oficial.
- Indicar se a estimativa está atualizada, pendente de recálculo, desatualizada ou indisponível.

### Responsabilidade do Back-end
- Reunir classificação atual, desempenho recente, partidas realizadas/restantes, adversários, histórico e estatísticas disponíveis.
- Verificar qualidade, período, cobertura e consistência dos dados de entrada.
- Produzir ou recuperar as probabilidades e projeções solicitadas sem expor mecanismo técnico como decisão de produto nesta etapa.
- Recalcular quando houver mudança relevante nos dados de entrada, atualização do estado de partidas/classificação ou política de atualização aplicável.
- Registrar contexto e instante de cálculo e retornar indisponibilidade quando entradas forem insuficientes.

### Dados envolvidos
- Campeonato, temporada, clubes, partida e resultado observado.
- Classificação e pontos atuais, resultados recentes, partidas realizadas/restantes, adversários e histórico disponível.
- Estimativas, data do cálculo, cobertura e estado de atualização.

### Regras envolvidas
- Toda previsão é identificada explicitamente como estimativa baseada em dados.
- A soma/representação das probabilidades de partida deve ser coerente com as categorias apresentadas.
- Não gerar projeção conclusiva quando a cobertura ou qualidade de dados for insuficiente.
- Estimativas não alteram classificação, resultado oficial ou estatística observada.
- A aplicação deve indicar os dados considerados e o momento do último cálculo.

### Validações
- Escopo da previsão corresponde à partida, campeonato e temporada selecionados.
- Dados de entrada pertencem ao período relevante e têm estado confiável.
- Estimativas não são exibidas como atuais se a entrada mudou e o recálculo falhou ou ainda não ocorreu.

### Fluxos alternativos
- Há estimativa de partida, mas não projeção de campeonato: apresentar somente a disponível e identificar as demais como indisponíveis.
- A previsão existente continua válida segundo o estado dos dados: apresentar a data do cálculo e sua base.
- O sistema identificou dados insuficientes: explicar quais grupos de dados estão ausentes sem inventar valores.

### Fluxos de erro
- Erro ao calcular/recuperar: informar que a estimativa está indisponível e manter separados os dados observados.
- Dados desatualizados: marcar explicitamente a projeção e não sugerir que representa o estado atual.
- Partida/campeonato inexistente ou não público: Not Found.

### Resultado esperado
O torcedor recebe estimativas contextualizadas e reconhece claramente sua incerteza, origem temporal e diferença em relação a fatos observados.

## Estados transversais da aplicação

| Estado | Comportamento esperado para o torcedor |
|---|---|
| Loading | Indicar carregamento da área solicitada sem sugerir que os dados já estão atualizados. |
| Empty State | Explicar qual conjunto não possui dados (por exemplo, sem partidas ou sem estatísticas do jogador) e oferecer ação útil quando possível. |
| Success | Confirmar a operação ou apresentar os dados, filtros, período e atualização aplicáveis. |
| Error | Informar falha específica em linguagem compreensível, preservar seleções e oferecer nova tentativa quando segura. |
| Unauthorized | Explicar que a ação exige autenticação ou não pertence às permissões do torcedor; permitir retornar à área pública. |
| Not Found | Informar que clube, jogador, partida ou conteúdo não foi encontrado ou não está disponível publicamente, sem revelar conteúdo restrito. |
| Dados desatualizados | Exibir quando os dados foram atualizados pela última vez, quais blocos estão atrasados e evitar apresentar projeção como atual. |

## Revisão de cobertura da persona

- Acompanhamento de clube, classificação, campanha, mandante/visitante, forma e evolução: J01, J03 e J04.
- Login, cadastro, logout, recuperação, clube favorito e preferências: J01 e J02.
- Partidas passadas/futuras, local, estádio e estatísticas: J03 e J05.
- Elenco, métricas de jogador, destaques e favoritos: J06.
- Comparação de jogadores com métricas equivalentes: J07.
- Comparação de clubes, forma, últimos cinco jogos e confrontos recentes: J08.
- Previsões informativas e seus avisos: J09.
- Navegação pública, privacidade, publicidade não intrusiva, atualização e ausência de dados: regras e estados transversais.

Não foi identificada jornada sem necessidade da persona. A consulta a perfil é pública; apenas a persistência de preferências requer autenticação, evitando conflito entre acesso público e gestão de conta.
