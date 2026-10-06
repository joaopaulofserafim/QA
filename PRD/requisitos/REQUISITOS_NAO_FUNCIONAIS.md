# Requisitos Não Funcionais

## Rastreabilidade e escopo

Estes requisitos não funcionais decorrem das jornadas e riscos identificados em:

- [Jornadas do Torcedor](../jornadas/TORCEDOR_JORNADAS.md)
- [Jornadas do Administrador](../jornadas/ADMINISTRADOR_JORNADAS.md)
- [Jornadas do Investidor](../jornadas/INVESTIDOR_JORNADAS.md)

Não definem tecnologias nem parâmetros quantitativos que dependam de decisão de produto/operação. Limiares (por exemplo, disponibilidade, tempos máximos e frequência de atualização) devem ser acordados e mensurados antes dos critérios de aceite finais.

## RNF-001 — Segurança de autenticação e sessão

- **Nome:** Proteção de identidade e sessão.
- **Descrição:** A aplicação deve proteger autenticação, recuperação de acesso, sessão e logout contra acesso não autorizado e exposição de credenciais.
- **Persona relacionada:** Torcedor, Administrador, Investidor/Parceiro.
- **Jornadas de origem:** Torcedor J01–J02; Administrador J01; Investidor J01.
- **Prioridade:** P0.
- **Critério de qualidade:** Estados de sessão são válidos, encerráveis e associados à identidade correta; mensagens de recuperação não revelam existência de conta.

## RNF-002 — Autorização e privilégio mínimo

- **Nome:** Isolamento de permissões e escopos.
- **Descrição:** Consultas e operações devem ser autorizadas por perfil, função, vínculo, entidade e campanha no processamento da solicitação, sem depender apenas de controles visuais.
- **Persona relacionada:** Todas.
- **Jornadas de origem:** Todas, especialmente Administrador J02/J06 e Investidor J01–J07.
- **Prioridade:** P0.
- **Critério de qualidade:** Torcedor não altera dados oficiais; parceiro não acessa dados fora do vínculo; administrador realiza somente ações autorizadas à sua função.

## RNF-003 — Privacidade e minimização de dados

- **Nome:** Proteção de dados pessoais e comerciais.
- **Descrição:** A aplicação deve limitar coleta, exibição e exportação ao mínimo necessário e não expor ao parceiro dados pessoais identificáveis, logs individuais ou informações de terceiros não autorizadas.
- **Persona relacionada:** Todas, com foco em Investidor/Parceiro e Administrador.
- **Jornadas de origem:** Torcedor J01–J02; Administrador J02/J07; Investidor J01–J07.
- **Prioridade:** P0.
- **Critério de qualidade:** Dashboards e exportações usam métricas agregadas; acessos a informação individual respeitam finalidade e permissão.

## RNF-004 — Confidencialidade de informações restritas

- **Nome:** Segregação de conteúdo e campanhas.
- **Descrição:** Conteúdo, métricas, campanhas e dados internos devem ser visíveis somente aos perfis e vínculos autorizados, inclusive por consulta direta, busca, comparação e exportação.
- **Persona relacionada:** Administrador, Investidor/Parceiro, Torcedor.
- **Jornadas de origem:** Administrador J02/J06; Investidor J01–J07; Torcedor J03/J05/J06.
- **Prioridade:** P0.
- **Critério de qualidade:** Respostas não revelam conteúdo restrito por meio de estados, totais, rankings ou mensagens de erro.

## RNF-005 — Integridade e consistência dos dados

- **Nome:** Coerência dos registros e agregações.
- **Descrição:** Dados esportivos, relações entre entidades, métricas comerciais e resultados agregados devem preservar integridade; alterações não podem produzir relações inválidas ou somatórios silenciosamente divergentes.
- **Persona relacionada:** Administrador, Torcedor, Investidor/Parceiro.
- **Jornadas de origem:** Administrador J03–J05; Torcedor J03–J07; Investidor J01–J06.
- **Prioridade:** P0.
- **Critério de qualidade:** Validações identificam dados duplicados ou incompatíveis; indicadores retornam período, denominador e cobertura aplicáveis.

## RNF-006 — Rastreabilidade e auditoria

- **Nome:** Atribuição de mudanças importantes.
- **Descrição:** Alterações importantes devem possuir trilha protegida com responsável, ação, valores anterior/novo, data/hora, entidade e resultado; trilha não pode ser apagada pelo autor da mudança.
- **Persona relacionada:** Administrador.
- **Jornadas de origem:** Administrador J02–J07.
- **Prioridade:** P0.
- **Critério de qualidade:** Operações sensíveis são explicáveis e consultáveis por pessoa autorizada; falha de auditoria não é mascarada como sucesso.

## RNF-007 — Disponibilidade das funções centrais

- **Nome:** Disponibilidade e comunicação de indisponibilidade.
- **Descrição:** Jornadas centrais devem permanecer acessíveis conforme metas de serviço a definir; indisponibilidade de uma fonte ou área não deve ocultar o estado de outras funções independentes.
- **Persona relacionada:** Todas.
- **Jornadas de origem:** Torcedor J01/J03–J08; Administrador J01/J05/J07; Investidor J01–J07.
- **Prioridade:** P1.
- **Critério de qualidade:** Falhas parciais são identificadas e não são representadas como resultados completos ou atuais.
- **Decisão pendente:** Definir metas de disponibilidade e janelas aceitáveis por função.

## RNF-008 — Desempenho percebido

- **Nome:** Resposta adequada em consultas e filtros.
- **Descrição:** Dashboards, buscas, filtros e detalhes devem fornecer feedback tempestivo e não bloquear a navegação durante processamento.
- **Persona relacionada:** Todas.
- **Jornadas de origem:** Todas.
- **Prioridade:** P1.
- **Critério de qualidade:** Cada solicitação longa exibe Loading e, se exceder metas futuras, oferece estado de espera/erro sem duplicar ações críticas.
- **Decisão pendente:** Estabelecer limites mensuráveis de resposta por classe de consulta.

## RNF-009 — Escalabilidade

- **Nome:** Capacidade de absorver crescimento.
- **Descrição:** A aplicação deve manter comportamento e consistência à medida que crescem usuários, clubes acompanhados, temporadas, partidas, consultas e eventos agregados.
- **Persona relacionada:** Todas.
- **Jornadas de origem:** Torcedor J03–J07; Administrador J03–J07; Investidor J01–J07.
- **Prioridade:** P2.
- **Critério de qualidade:** Crescimento de volume não deve degradar a integridade, autorização ou comparabilidade dos resultados.
- **Decisão pendente:** Definir projeções de volume e metas sob carga.

## RNF-010 — Confiabilidade e recuperação de falhas

- **Nome:** Resultado operacional explícito e recuperável.
- **Descrição:** Operações devem distinguir sucesso total, parcial, falha e estado não confirmado; falhas não devem deixar alterações silenciosas ou resultados com aparência de sucesso.
- **Persona relacionada:** Administrador, Torcedor, Investidor/Parceiro.
- **Jornadas de origem:** Todas, especialmente Administrador J03–J07 e Investidor J04/J07.
- **Prioridade:** P0.
- **Critério de qualidade:** Após falha, o usuário sabe se a operação foi realizada; ações repetidas não geram duplicidade ou efeito inesperado.

## RNF-011 — Atualidade, origem e cobertura

- **Nome:** Transparência temporal e proveniência dos dados.
- **Descrição:** Dados esportivos, comerciais e externos devem apresentar instante conhecido de atualização, origem conceitual e cobertura quando disponíveis; diferença entre dado atrasado, ausente e zero deve ser preservada.
- **Persona relacionada:** Todas.
- **Jornadas de origem:** Torcedor J03–J08; Administrador J03–J05; Investidor J01–J06.
- **Prioridade:** P0.
- **Critério de qualidade:** Usuário não interpreta dado antigo ou indisponível como atual ou igual a zero.
- **Decisão pendente:** Definir periodicidade e limites máximos de defasagem aceitáveis por categoria de dado.

## RNF-012 — Acessibilidade

- **Nome:** Acesso perceptível e operável.
- **Descrição:** Conteúdo, controles, tabelas, gráficos, estados e feedback devem permitir compreensão e operação por usuários com diferentes capacidades e contextos de uso.
- **Persona relacionada:** Todas, com atenção à familiaridade digital variável do torcedor.
- **Jornadas de origem:** Torcedor J01–J08; Administrador J01–J07; Investidor J01–J07.
- **Prioridade:** P1.
- **Critério de qualidade:** Métricas e estados não dependem exclusivamente de cor; controles e explicações são perceptíveis, identificáveis e operáveis.

## RNF-013 — Usabilidade e clareza semântica

- **Nome:** Interpretação consistente de métricas e estados.
- **Descrição:** A aplicação deve usar rótulos, unidades, definições, períodos e feedback compreensíveis para evitar confusão entre estatística observada, avaliação, projeção, impressões, alcance, usuários e acessos.
- **Persona relacionada:** Todas.
- **Jornadas de origem:** Todas.
- **Prioridade:** P0.
- **Critério de qualidade:** Cada métrica pode ser interpretada sem depender de documentação externa; previsões e scores têm contexto/limitações acessíveis.

## RNF-014 — Responsividade e legibilidade

- **Nome:** Experiência adaptável a diferentes telas.
- **Descrição:** Dashboards, comparações, calendários, perfis e gráficos devem permanecer legíveis e utilizáveis em telas pequenas e grandes.
- **Persona relacionada:** Todas, especialmente Torcedor.
- **Jornadas de origem:** Torcedor J03–J08; Administrador J01–J07; Investidor J01–J07.
- **Prioridade:** P1.
- **Critério de qualidade:** Conteúdo prioritário, filtros e estados não são encobertos nem exigem leitura de gráfico ilegível em tela reduzida.

## RNF-015 — Reprodutibilidade e comparabilidade

- **Nome:** Definições estáveis para comparações.
- **Descrição:** Comparações e relatórios devem manter definições, filtros, períodos, unidades, denominadores e cobertura visíveis; mudanças de definição devem ser identificáveis.
- **Persona relacionada:** Torcedor e Investidor/Parceiro.
- **Jornadas de origem:** Torcedor J04/J07; Investidor J01–J07.
- **Prioridade:** P0.
- **Critério de qualidade:** Resultados comparados podem ser reproduzidos a partir dos filtros e contexto exibidos; diferenças de base não ficam ocultas.

## RNF-016 — Observabilidade operacional

- **Nome:** Visibilidade de falhas e estado de processamento.
- **Descrição:** Operações internas e integrações devem produzir informações suficientes para detectar falha, atraso, impacto, escopo e resultado sem expor detalhes sensíveis ao usuário não autorizado.
- **Persona relacionada:** Administrador.
- **Jornadas de origem:** Administrador J01/J04/J05/J07.
- **Prioridade:** P1.
- **Critério de qualidade:** Administrador autorizado consegue relacionar alerta a execução/entidade afetada; usuário público recebe mensagem segura e compreensível.

## RNF-017 — Proteção de exportações

- **Nome:** Escopo seguro de relatórios.
- **Descrição:** Relatórios exportados devem preservar permissões, agregação, filtros, definições e limitações da visualização de origem.
- **Persona relacionada:** Investidor/Parceiro.
- **Jornadas de origem:** Investidor J03–J07.
- **Prioridade:** P0.
- **Critério de qualidade:** Saída não contém dados pessoais identificáveis, campanhas ou clubes não autorizados e informa período, filtros, fontes e atualização.

## RNF-018 — Compatibilidade de acesso

- **Nome:** Compatibilidade com contextos de navegação suportados.
- **Descrição:** A aplicação deve permitir a execução das jornadas em contextos de acesso suportados pelo produto, mantendo funções, legibilidade e controles de segurança equivalentes.
- **Persona relacionada:** Todas.
- **Jornadas de origem:** Torcedor J01–J08; Administrador J01–J07; Investidor J01–J07.
- **Prioridade:** P2.
- **Critério de qualidade:** Não há perda silenciosa de função ou proteção ao alternar entre contextos oficialmente suportados.
- **Decisão pendente:** Definir dispositivos, navegadores e versões que serão oficialmente suportados.

## RNF-019 — Recuperação e continuidade operacional

- **Nome:** Preparação verificável para recuperação.
- **Descrição:** Rotinas de backup e recuperação devem ter estado, cobertura, resultado e evidência de verificação disponíveis a administradores autorizados.
- **Persona relacionada:** Administrador.
- **Jornadas de origem:** Administrador J01/J07.
- **Prioridade:** P1.
- **Critério de qualidade:** A existência de cópia não é apresentada como recuperação comprovada; ações de restauração têm escopo, autorização e auditoria.
- **Decisão pendente:** Definir objetivos de recuperação, retenção e frequência de verificação.

## RNF-020 — Tratamento transparente de previsões

- **Nome:** Comunicação responsável de estimativas.
- **Descrição:** Previsões devem ser diferenciadas de fatos, acompanhar dados/tempo de referência e informar incerteza, limitações e indisponibilidade quando aplicável.
- **Persona relacionada:** Torcedor.
- **Jornadas de origem:** Torcedor J08.
- **Prioridade:** P0.
- **Critério de qualidade:** Nenhuma estimativa é apresentada como resultado garantido ou dado oficial; projeção vencida é marcada como desatualizada.

## Revisão de cobertura

- Segurança, privacidade e autorização: RNF-001–RNF-004 e RNF-017.
- Integridade, auditoria, confiabilidade e recuperação: RNF-005, RNF-006, RNF-010 e RNF-019.
- Disponibilidade, desempenho, escala e observabilidade: RNF-007–RNF-009 e RNF-016.
- Atualização, origem, comparabilidade e previsões: RNF-011, RNF-015 e RNF-020.
- Acessibilidade, usabilidade, responsividade e compatibilidade: RNF-012–RNF-014 e RNF-018.

Os critérios quantitativos foram deixados como decisões pendentes porque ainda não há metas de negócio/operação fornecidas. Esta etapa não escolhe tecnologias nem inventa limites mensuráveis.
