# Jornadas do Investidor e Parceiro Comercial

## Base e rastreabilidade

**Persona-fonte:** [INVESTIDOR.md](../personas/INVESTIDOR.md)

**Acesso:** analítico/comercial, de leitura e limitado ao vínculo, às métricas agregadas e às campanhas autorizadas. Não acessa dados pessoais identificáveis, logs operacionais ou campanhas de terceiros fora do escopo.

**Objetivo central:** avaliar audiência, comportamento agregado, engajamento e desempenho comercial com métricas comparáveis, explicáveis e exportáveis.

Métricas da aplicação e métricas oriundas de fontes externas devem permanecer distinguíveis. Métricas sociais podem depender de uma **fonte externa de métricas de redes sociais**; indisponibilidade, falta de integração e ausência de cobertura não devem ser representadas como valor zero.

## J01 — Entrar e consultar o dashboard comercial

### Persona
Investidor e Parceiro Comercial.

### Objetivo
Entender tamanho, recorrência e crescimento da audiência dentro do escopo autorizado.

### Relação com a persona
- **Objetivo atendido:** entender tamanho, composição temporal e crescimento da audiência.
- **Necessidade atendida:** dashboard com filtros, definições estáveis, dados agregados e destaque de clubes mais acessados/com maior crescimento.
- **Dor reduzida:** métricas espalhadas, inconsistentes ou sem contexto de origem.

### Pré-condições
- O usuário possui conta comercial ativa e escopo autorizado.
- Há dados internos de audiência disponíveis para o período ou a ausência está identificada.

### Gatilho
O investidor/parceiro entra na aplicação ou abre o dashboard comercial.

### Fluxo principal
1. O usuário informa credenciais.
2. O sistema valida identidade, estado da conta, perfil comercial, vínculo e escopo autorizado.
3. O sistema carrega o dashboard inicial para um período padrão definido pelo produto.
4. O usuário seleciona período, clube ou campanha disponível.
5. O sistema valida filtros, aplica escopo de acesso e consulta acessos, usuários únicos, recorrência, crescimento, tempo médio, páginas e demais métricas cobertas.
6. O sistema calcula agregados e variações em base comparável, identificando denominadores, cobertura e atualização.
7. A interface apresenta indicadores, clubes mais acessados e clubes com maior crescimento no período, e permite aprofundar por clube, conteúdo, campanha ou comparação.

### Responsabilidade do Front-end
- Oferecer acesso comercial e explicar o escopo ativo.
- Apresentar filtros de período, clube e campanha autorizada, com filtros aplicados visíveis.
- Mostrar acessos, usuários únicos, recorrência, crescimento, tempo médio, páginas acessadas e páginas por usuário.
- Destacar clubes mais acessados e clubes com maior crescimento, sempre com período, base e cobertura explícitos.
- Definir métricas junto aos valores ou em explicação acessível.
- Indicar período, fonte, atualização, cobertura, denominadores e comparação utilizada.
- Permitir remover filtros e recuperar visão geral.

### Responsabilidade do Back-end
- Autenticar o usuário e resolver vínculo, permissões e escopo comercial.
- Aplicar a autorização a cada consulta, não apenas à interface.
- Consultar/agregar dados de audiência sem retornar informações pessoais identificáveis.
- Calcular métricas e variações segundo definições estáveis e retornar denominadores, cobertura e fonte.
- Consolidar ordenações de clubes por acessos e crescimento apenas quando a cobertura e o período forem comparáveis.
- Não substituir ausência de dados por zero nem misturar métrica externa com interna sem identificação.

### Dados envolvidos
- Identidade, papel, vínculo e escopo do parceiro.
- Eventos agregáveis de audiência, acessos, usuários únicos/recorrentes, páginas e tempo.
- Agregados de audiência e crescimento por clube.
- Período, filtros, métricas, denominadores, fonte e atualização.

### Regras envolvidas
- Métricas são agregadas; não há acesso a dados pessoais identificáveis.
- Resultados obedecem ao vínculo e às autorizações vigentes.
- Comparação de períodos usa definições e intervalos explícitos.
- Crescimento percentual requer base de comparação disponível e não enganosa.

### Validações
- Conta ativa, perfil comercial e autorização para escopo/período consultado.
- Período válido e filtros pertencentes ao escopo.
- Denominador e cobertura suficientes para cada métrica.

### Fluxos alternativos
- Sem filtros, apresenta visão geral autorizada.
- Sem dados em um período, apresenta Empty State identificado e permite alterar período.
- O parceiro não possui campanhas vinculadas: apresenta campanhas como indisponíveis, não vazias por falha.

### Fluxos de erro
- Login negado: informar falha de acesso sem revelar detalhes da conta.
- Escopo não autorizado: negar dado e manter os demais indicadores permitidos.
- Consulta falha: preservar filtros e indicar se a falha afeta total ou parcialmente o painel.
- Dados atrasados: apresentar data conhecida e rotular indicadores como desatualizados.

### Resultado esperado
O usuário visualiza indicadores comerciais agregados e comparáveis dentro de seu escopo, com definições e limitações claras.

## J02 — Analisar audiência, conteúdos e jogadores por clube

### Persona
Investidor e Parceiro Comercial.

### Objetivo
Identificar interesse e oportunidades comerciais associados a um clube.

### Relação com a persona
- **Objetivo atendido:** avaliar diferenças de acesso, encontrar conteúdos e jogadores de maior interesse.
- **Necessidade atendida:** segmentação por clube, páginas, conteúdo e tendências.
- **Dor reduzida:** incerteza sobre audiência e esforço manual para combinar relatórios.

### Pré-condições
- O clube e o período estão no escopo de acesso do parceiro.
- Existem dados internos de audiência relacionados a clubes/conteúdos; cobertura pode variar.

### Gatilho
O parceiro seleciona um clube no dashboard ou inicia uma análise por clube.

### Fluxo principal
1. O parceiro escolhe clube e período.
2. O sistema valida escopo e consulta acessos, recorrência, páginas/conteúdos mais acessados, jogadores mais visualizados e tendências disponíveis.
3. O sistema agrega indicadores por clube e período e prepara comparação com período equivalente, se solicitada.
4. A interface apresenta audiência, engajamento, crescimento e itens de maior interesse com definição, cobertura e atualização.
5. O parceiro seleciona um conteúdo, jogador ou tendência para detalhar dados agregados.
6. O sistema confirma escopo e retorna apenas métricas permitidas.

### Responsabilidade do Front-end
- Permitir escolher clube, período e dimensão de interesse.
- Exibir acessos, recorrência, crescimento, páginas/conteúdos populares e jogadores mais visualizados quando cobertos.
- Apresentar tendências e comparação temporal sem sugerir causalidade não comprovada.
- Identificar a origem interna ou externa e a disponibilidade de cada indicador.
- Distinguir contagem sem cobertura, valor zero observado e indicador não aplicável.

### Responsabilidade do Back-end
- Aplicar escopo do parceiro ao clube, período e dimensão.
- Agregar eventos por clube/conteúdo/jogador com proteção contra exposição individual.
- Calcular tendências e variações com base comparável e denominadores claros.
- Retornar apenas dados de popularidade agregados e disponíveis.
- Associar origem, período, atualização e cobertura.

### Dados envolvidos
- Clube, período, páginas/conteúdo, jogadores visualizados, acessos, usuários únicos/recorrentes e interações agregadas.
- Comparação temporal, cobertura, fonte e atualização.

### Regras envolvidas
- O parceiro não identifica torcedores nem consulta logs individuais.
- Dados de clube não autorizado não podem ser recuperados por filtro, detalhe ou exportação.
- Tendência não significa causalidade.
- Métrica sem cobertura não pode ser exibida como zero.

### Validações
- Clube, dimensão e período pertencem ao escopo permitido.
- Volume agregado atende aos critérios de privacidade que serão definidos.
- Período e base de comparação são equivalentes ou a diferença é explicitada.

### Fluxos alternativos
- Clube tem dados parciais: apresentar métricas disponíveis e identificar blocos sem cobertura.
- Conteúdo/jogador não possui visualizações no recorte: mostrar Empty State específico.
- Dados externos não estão integrados: explicar indisponibilidade sem criar valor zero.

### Fluxos de erro
- Clube fora do escopo: negar a consulta sem revelar métricas ou campanhas.
- Falha parcial de agregação: apresentar blocos carregados e identificar os que falharam.
- Filtros sem resultados: explicar recorte e permitir ajuste.

### Resultado esperado
O parceiro entende a audiência agregada e os conteúdos/jogadores de interesse do clube autorizado, com limitações explícitas.

## J03 — Comparar clubes e períodos

### Persona
Investidor e Parceiro Comercial.

### Objetivo
Comparar audiência e engajamento entre clubes ou intervalos com denominadores consistentes.

### Relação com a persona
- **Objetivo atendido:** comparar clubes e períodos e explicar resultados.
- **Necessidade atendida:** variação absoluta/percentual, período equivalente e filtros reproduzíveis.
- **Dor reduzida:** comparações com definições, períodos ou denominadores diferentes.

### Pré-condições
- Os clubes e períodos estão dentro da autorização do usuário.
- As definições das métricas selecionadas estão disponíveis.

### Gatilho
O parceiro seleciona comparar clubes, períodos ou ambas as dimensões.

### Fluxo principal
1. O parceiro seleciona clubes, períodos e métricas.
2. A interface confirma os filtros e informa o escopo.
3. O sistema valida autorização e compatibilidade temporal/metodológica.
4. O sistema recupera os agregados comparáveis e calcula diferenças absolutas e percentuais quando a base permite.
5. A interface mostra os resultados lado a lado, o período de cada base, denominadores, cobertura e variação.
6. O parceiro altera filtros ou abre análise de clube/conteúdo para explicar a diferença observada.

### Responsabilidade do Front-end
- Oferecer comparações clube x clube e período x período.
- Exibir filtros, métricas, intervalos e denominadores para cada lado.
- Distinguir variação absoluta e percentual e explicar a base.
- Alertar quando períodos não têm duração ou cobertura equivalentes.
- Evitar escalas/gráficos que ocultem diferença de cobertura ou induzam causalidade.

### Responsabilidade do Back-end
- Autorizar todos os lados da comparação.
- Consultar métricas com definições equivalentes e normalizar apenas segundo regras explícitas.
- Calcular diferença absoluta/percentual quando o denominador for válido.
- Retornar cobertura, origem, atualização e motivo quando não houver comparação válida.
- Manter filtros utilizados reproduzíveis para visualização/relatório.

### Dados envolvidos
- Clubes, intervalos, indicadores agregados, definições, denominadores e resultados comparativos.
- Fonte, cobertura, atualização e parâmetros do relatório.

### Regras envolvidas
- Não comparar percentuais sem base de referência válida.
- Mudança de definição exige identificação no período afetado.
- Períodos não equivalentes devem ser claramente marcados e não rotulados como equivalentes.

### Validações
- Autorização para todos os clubes, períodos e métricas.
- Intervalos válidos, sem sobreposição ambígua quando a comparação exige períodos separados.
- Denominadores e cobertura suficientes para diferenças calculadas.

### Fluxos alternativos
- Somente métricas comuns possuem dados: comparar as métricas comuns e listar indisponíveis.
- Cobertura diferente: permitir comparação com aviso e dados de cobertura visíveis.
- Variação percentual não calculável: apresentar diferença absoluta quando válida e explicar percentual indisponível.

### Fluxos de erro
- Um dos lados não autorizado: negar o resultado comparativo completo ou remover o item apenas se isso não revelar informação protegida.
- Consulta de um período falha: preservar outro resultado como parcial e identificar lado indisponível.
- Nenhuma métrica comparável: solicitar ajuste de filtros sem produzir um ranking enganoso.

### Resultado esperado
O parceiro pode explicar diferenças entre clubes e períodos sem ocultar base, cobertura ou limites metodológicos.

## J04 — Acompanhar campanhas publicitárias autorizadas

### Persona
Investidor, anunciante ou parceiro autorizado à campanha.

### Objetivo
Medir alcance e desempenho das campanhas às quais possui acesso.

### Relação com a persona
- **Objetivo atendido:** acompanhar impressões, cliques, CTR, alcance e engajamento.
- **Necessidade atendida:** campanha, clube, período e espaço de exibição identificáveis.
- **Dor reduzida:** dificuldade para medir retorno e explicar desempenho de campanhas.

### Pré-condições
- Existe campanha disponível e o usuário está autorizado a consultá-la.
- As métricas relevantes foram fornecidas e têm estado de atualização conhecido.

### Gatilho
O parceiro abre campanhas ou seleciona uma campanha no dashboard.

### Fluxo principal
1. O parceiro seleciona campanha, período, clube e/ou espaço de exibição entre as opções autorizadas.
2. O sistema valida o escopo e recupera estado, intervalo, impressões, alcance, cliques e engajamento disponíveis.
3. O sistema calcula CTR conforme definição comercial aplicável e retorna denominador e cobertura.
4. A interface apresenta indicadores, tendência e desempenho no período com rótulos e definições.
5. O parceiro compara períodos ou campanhas autorizadas.
6. O sistema mantém os filtros e aplica as mesmas regras de comparação; a interface atualiza resultados e confirma escopo.

### Responsabilidade do Front-end
- Listar somente campanhas autorizadas e indicar estado/período.
- Permitir filtrar por clube, período e espaço de exibição autorizado.
- Exibir impressões, alcance, cliques, CTR, engajamento e desempenho quando disponíveis.
- Informar fórmula/denominador de CTR e definições de métricas.
- Mostrar fonte, atualização, cobertura e comparações aplicadas.

### Responsabilidade do Back-end
- Autorizar campanha, clube, período e espaço de exibição em cada consulta.
- Recuperar métricas por campanha e período, mantendo origem identificada.
- Calcular CTR segundo regra definida e retornar numerador/denominador.
- Diferenciar zero observado, dado ausente e indisponibilidade da fonte.
- Agregar resultados e proteger dados pessoais.

### Dados envolvidos
- Campanha, estado, período, clube, espaço de exibição.
- Impressões, alcance, cliques, engajamento, CTR, denominadores, origem e atualização.

### Regras envolvidas
- O parceiro só consulta campanhas autorizadas.
- CTR e outras taxas sempre têm definição, período e denominador.
- Métrica ausente por integração não significa campanha sem desempenho.
- Dados agregados não devem permitir identificar indivíduos.

### Validações
- Usuário está vinculado e autorizado à campanha e ao período.
- Campanha, clube e espaço de exibição são compatíveis.
- Denominador não nulo e base válida antes de calcular CTR.

### Fluxos alternativos
- Campanha sem impressões/cliques ainda: apresentar valores observados e taxas não calculáveis quando apropriado.
- Métricas disponíveis apenas para parte do período: identificar o intervalo coberto.
- Campanha encerrada: manter consulta histórica segundo autorização.

### Fluxos de erro
- Campanha não autorizada ou inexistente: negar sem expor detalhes.
- Falha de fonte: marcar métricas afetadas como indisponíveis.
- Filtro incompatível: informar qual campo precisa ser ajustado e não retornar mistura de campanhas.

### Resultado esperado
O parceiro avalia desempenho de campanhas com escopo autorizado, métricas definidas e rastreabilidade até período e espaço de exibição.

## J05 — Consultar métricas de redes sociais

### Persona
Investidor e Parceiro Comercial.

### Objetivo
Usar indicadores sociais disponíveis como contexto complementar de audiência e engajamento.

### Relação com a persona
- **Objetivo atendido:** consultar indicadores sociais consolidados quando integrações existirem.
- **Necessidade atendida:** separar dados da aplicação e dados externos e indicar origem/cobertura.
- **Dor reduzida:** dados externos ausentes, incompletos ou irregulares tratados sem contexto.

### Pré-condições
- Uma fonte externa de métricas de redes sociais fornece dados para o clube/período.
- O parceiro tem autorização de leitura agregada.

### Gatilho
O parceiro abre métricas sociais no detalhe do clube ou dashboard.

### Fluxo principal
1. O parceiro seleciona clube e período.
2. O sistema verifica fonte, permissão, cobertura e atualização.
3. O sistema recupera seguidores, crescimento, publicações, curtidas, comentários, compartilhamentos, visualizações e taxa de engajamento disponíveis.
4. O sistema consolida os resultados sem misturá-los com métricas internas da aplicação.
5. A interface identifica claramente origem externa, período coberto, data de atualização e campos indisponíveis.
6. O parceiro compara período ou clube se ambos tiverem métricas compatíveis.

### Responsabilidade do Front-end
- Distinguir visualmente indicadores de redes sociais dos indicadores internos.
- Apresentar métricas e definições, período, fonte, atualização e cobertura.
- Mostrar integração ausente ou dados incompletos sem preencher com zero.
- Permitir comparações apenas quando compatíveis e expor diferenças de cobertura.

### Responsabilidade do Back-end
- Consultar métricas disponibilizadas por fonte externa conceitual.
- Validar escopo de clube e período e preservar metadados de origem.
- Consolidar métricas sem atribuir valores inexistentes.
- Indicar falha, atraso, ausência de integração e cobertura parcial como estados distintos.
- Proteger dados restritos de contas ou parceiros.

### Dados envolvidos
- Clube, período, seguidores, variação, publicações, curtidas, comentários, compartilhamentos, visualizações e taxa de engajamento.
- Fonte externa, atualização, cobertura e estado de disponibilidade.

### Regras envolvidas
- Ausência de integração não é zero.
- Métrica social permanece identificada como externa.
- Comparações exigem definições, períodos e cobertura explícitos.

### Validações
- Clube, período e fonte disponíveis e autorizados.
- Taxa de engajamento tem definição e denominador conhecidos.
- Dados recebidos pertencem ao período informado.

### Fluxos alternativos
- Integração existe mas ainda não há dados no período: Empty State com período e cobertura conhecidos.
- Alguns indicadores estão ausentes: exibir somente os disponíveis e explicar a limitação.
- Fonte não cobre todos os clubes: impedir interpretação de ranking completo sem aviso.

### Fluxos de erro
- Fonte externa indisponível: mostrar Error/atraso com última atualização.
- Métricas inconsistentes: não calcular taxa comparativa sem base confiável.
- Clube fora do escopo: negar consulta.

### Resultado esperado
O parceiro interpreta métricas sociais como dados externos, com cobertura e atualização transparentes, ou entende por que não estão disponíveis.

## J06 — Consultar ranking de engajamento

### Persona
Investidor e Parceiro Comercial.

### Objetivo
Identificar clubes com maior engajamento no período sem ocultar critérios e cobertura.

### Relação com a persona
- **Objetivo atendido:** comparar engajamento e identificar tendências de clubes.
- **Necessidade atendida:** ranking com período, critérios transparentes e fontes disponíveis.
- **Dor reduzida:** rankings opacos e comparações com cobertura desigual.

### Pré-condições
- Há indicadores agregados de um ou mais clubes no período.
- O usuário tem acesso ao escopo de clubes considerado.

### Gatilho
O parceiro abre ranking e seleciona período e critérios disponíveis.

### Fluxo principal
1. O parceiro seleciona período e, quando disponível, conjunto de indicadores/fontes.
2. O sistema valida autorização, cobertura e compatibilidade entre clubes.
3. O sistema recupera acessos, interações, visualizações, crescimento e métricas sociais disponíveis.
4. O sistema calcula um score segundo regra de negócio a definir posteriormente, sem apresentar fórmula não aprovada como definitiva.
5. O sistema ordena clubes e retorna critérios, cobertura, dados excluídos e data de atualização.
6. A interface apresenta ranking, filtros e explicação do score e permite abrir análise de clube.

### Responsabilidade do Front-end
- Permitir selecionar período e dimensões disponíveis.
- Apresentar posição, score, indicadores considerados e fontes/cobertura.
- Explicar que a fórmula final do score depende de regra de negócio aprovada.
- Destacar clubes com cobertura parcial e não sugerir comparação completa quando não for válida.
- Permitir navegar ao detalhe do clube e rever filtros.

### Responsabilidade do Back-end
- Reunir somente indicadores agregados e autorizados.
- Avaliar cobertura comparável e retornar quais dimensões entram ou não.
- Calcular score conforme regra aprovada futura e versionar/identificar critério e período.
- Ordenar resultados de forma consistente e tratar empates conforme regra de negócio definida.
- Não transformar dado externo ausente em score zero sem regra explícita.

### Dados envolvidos
- Clubes, período, acessos, interações, visualizações, crescimento e dados sociais disponíveis.
- Score, posição, critérios, fontes, cobertura, versão/regra e atualização.

### Regras envolvidas
- Não fixar a fórmula do score nesta fase.
- Critérios e fontes considerados devem ser explicáveis.
- Cobertura desigual deve ser exposta e pode limitar comparabilidade.
- Acesso restrito a um clube não autoriza inferir ou retornar seus dados pelo ranking.

### Validações
- Período válido e métricas/clubes autorizados.
- Cobertura mínima conforme regra futura explicitada.
- Score e ordem calculados a partir da mesma versão de critério.

### Fluxos alternativos
- Cobertura parcial: apresentar ranking parcial ou limitar clubes, conforme política futura explícita e comunicada.
- Empate: aplicar regra de desempate aprovada ou exibir posições empatadas.
- Fonte social ausente: calcular somente com indicadores permitidos e declarar exclusão.

### Fluxos de erro
- Nenhum clube possui cobertura suficiente: informar que não há ranking comparável no período.
- Falha em uma fonte: indicar indicadores afetados e não afirmar ranking completo.
- Regra de score não definida/indisponível: não publicar posição como oficial; apresentar estado não disponível.

### Resultado esperado
O parceiro entende ordem, período, score e limitações do ranking; nenhum método ainda não aprovado é apresentado como definitivo.

## J07 — Gerar e exportar relatórios

### Persona
Investidor e Parceiro Comercial.

### Objetivo
Compartilhar evidências comerciais com filtros reproduzíveis e dentro do escopo autorizado.

### Relação com a persona
- **Objetivo atendido:** exportar relatórios para decisão e prestação de contas.
- **Necessidade atendida:** filtros persistentes e exportação controlada.
- **Dor reduzida:** trabalho manual e risco de expor dados além da autorização.

### Pré-condições
- O parceiro está autenticado.
- Há indicadores e filtros válidos no escopo autorizado.

### Gatilho
O parceiro solicita criar, visualizar ou exportar um relatório.

### Fluxo principal
1. O parceiro seleciona período, clube(s), campanha(s) autorizada(s) e métricas.
2. A interface apresenta um resumo dos filtros e dados que farão parte do relatório.
3. O sistema valida autorização, filtros, cobertura e política de exportação.
4. O sistema monta o relatório usando as mesmas definições e agregações do dashboard.
5. A interface apresenta prévia com fonte, período, filtros, atualização e limitações.
6. O parceiro confirma exportação.
7. O sistema aplica minimização de dados, gera o arquivo/saída autorizada e registra evento de exportação conforme política.
8. A interface confirma resultado e disponibiliza saída apenas ao usuário autorizado.

### Responsabilidade do Front-end
- Permitir configurar filtros e métricas do relatório.
- Mostrar prévia, escopo, definições, fontes e cobertura antes de exportar.
- Exibir formato de saída disponível sem decisão tecnológica.
- Confirmar sucesso ou erro e manter filtros usados para reexecução.

### Responsabilidade do Back-end
- Revalidar permissões de cada dado ao gerar a saída.
- Utilizar agregados e definições coerentes com o dashboard.
- Remover informações pessoais identificáveis e dados fora do escopo.
- Incluir período, filtros, definições, fontes e atualização no relatório.
- Registrar solicitação/resultado quando requerido pela governança.

### Dados envolvidos
- Filtros, métricas agregadas, definições, fontes, atualização, cobertura e dados do relatório.
- Identidade autorizada, escopo, solicitação e resultado da exportação.

### Regras envolvidas
- Exportação respeita o mesmo escopo de leitura do dashboard.
- Não exportar dados pessoais identificáveis, logs operacionais ou campanhas não autorizadas.
- Relatório deve informar filtros, período, denominadores, fontes e limitações.
- A saída não pode ampliar acesso por ser exportada.

### Validações
- Sessão ativa e escopo válido no momento da exportação.
- Período, filtros e dimensões autorizados.
- Nenhum campo restrito ou identificador pessoal na saída.

### Fluxos alternativos
- Prévia mostra cobertura parcial: permitir exportação apenas com aviso explícito.
- O usuário salva/consulta relatório sem exportá-lo: preservar parâmetros permitidos.
- Os dados mudam entre prévia e confirmação: recalcular ou informar diferença antes de gerar.

### Fluxos de erro
- Autorização expirada/revogação: cancelar geração e não disponibilizar saída.
- Falha de geração: preservar filtros e informar que nenhum relatório foi disponibilizado.
- Falha de fonte: incluir limitação somente se o relatório continuar interpretável; caso contrário, impedir exportação e explicar.

### Resultado esperado
O parceiro obtém relatório agregado, reproduzível e compatível com seu escopo, com contexto suficiente para interpretar os números.

## Estados transversais da aplicação

| Estado | Comportamento esperado para o investidor/parceiro |
|---|---|
| Loading | Indicar filtros e visões em processamento; não exibir resultados antigos como atuais sem marcação. |
| Empty State | Diferenciar período sem eventos, campanha inexistente e falta de integração/cobertura. |
| Success | Confirmar filtros, escopo, período, fonte, atualização e resultado da operação. |
| Error | Identificar bloco/fonte afetada, preservar filtros e oferecer nova tentativa quando segura. |
| Unauthorized | Negar dado/ação fora do vínculo e não revelar a existência ou os valores de informação restrita. |
| Not Found | Informar campanha/clube não encontrado ou indisponível no escopo, sem expor informação de terceiros. |
| Dados desatualizados | Exibir última atualização e cobertura; evitar tratar valor antigo como atual. |

## Revisão de cobertura da persona

- Dashboard, acessos, usuários únicos, recorrência, tempo, páginas, clubes mais acessados e clubes com maior crescimento: J01.
- Análise por clube, conteúdo, jogadores e tendências: J02.
- Comparações entre clubes/períodos: J03.
- Campanhas, impressões, alcance, cliques, CTR e engajamento: J04.
- Seguidores, crescimento e interações sociais: J05.
- Ranking de engajamento: J06.
- Relatórios e exportação controlada: J07.
- Escopo comercial, agregação, privacidade, origem e atualização: regras transversais em todas as jornadas.

Não foi identificada jornada sem necessidade da persona. A experiência mantém isolados dados de parceiros, campanhas e áreas operacionais; redes sociais são opcionais e a fórmula final do score permanece pendente de definição de negócio.
