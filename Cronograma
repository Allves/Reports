# Inventário e cronograma de migração Angular → React

> Atualizado em 24/07/2026. Este documento compara os módulos funcionais em
> `BlackArrow.PortalFidc.FrontEnd/src/app/modules` com rotas, BFFs, componentes
> e contratos já presentes em `Black101.FrontEnd`. O Angular é referência
> consultiva; contratos versionados, backend e documentação deste repositório
> permanecem as fontes operacionais.
>
> Para apresentação semanal, use primeiro as seções **Resumo para gerência**,
> **Leitura gerencial dos status** e **Ordem recomendada e cronograma**. O
> inventário por domínio continua logo abaixo para rastrear evidências e
> próximos recortes com mais detalhe.

## Resumo para gerência

A migração saiu da fase de "começar do zero". Já existe uma base reaproveitável
para login, navegação, Cedentes, Operações e parte relevante dos Cadastros. O
ponto de atenção é que vários módulos aparecem na nova plataforma, mas ainda
não cobrem todo o fluxo do legado. Em outras palavras: algumas áreas já são
boas candidatas para fechamento, enquanto outras ainda precisam de descoberta
antes de entrar em desenvolvimento pesado.

Na conversa semanal, a leitura recomendada é:

| Pergunta da gerência | Resposta curta para a semana |
|---|---|
| Onde estamos bem? | Fundação da aplicação, Cedentes, Operações base e avanço visual/funcional de Sacados. |
| O que está quase virando entrega fechada? | Sacados, Recebíveis, Movimentação Financeira, Consultas, Relatório Financeiro e Administrativo. |
| Onde mora o maior risco? | Fluxos financeiros, Gestora, importações/exportações, documentos, permissões e módulos que ainda não têm contrato. |
| O que não deve ser vendido como pronto? | Stubs, listas isoladas sem CRUD completo e módulos marcados como parcial sem validação de paridade. |
| Qual é a prioridade prática? | Fechar o que já começou antes de abrir frentes grandes novas. |

## Leitura gerencial dos status

| Status | Leitura executiva | Como comentar na reunião |
|---|---|---|
| ✅ Concluído no escopo atual | Entrega utilizável dentro do recorte combinado. | "Está pronto para o que foi contratado neste ciclo; ainda pode ter melhorias mapeadas." |
| 🟡 Parcial | Já existe algo concreto, mas ainda falta parte do fluxo. | "Tem avanço real, mas não substitui 100% o legado ainda." |
| ⚪ Stub / bloqueado | A página existe mais para reservar espaço do que para operar. | "Aparece no menu, mas ainda depende de contrato, backend ou decisão." |
| 🔴 Não migrado | Ainda não há entrega funcional na nova plataforma. | "Precisa entrar como frente futura, começando por descoberta e contrato." |
| 🧭 Em descoberta | Precisa mapear legado, API, permissões e dependências antes de estimar com segurança. | "Ainda estamos tirando a névoa do caminho; estimativa firme vem depois da descoberta." |

## Leitura do status

| Status | Significado prático |
|---|---|
| ✅ Concluído no escopo atual | Existe contrato e implementação do escopo explicitamente definido. Pode ainda haver lacunas registradas no contrato. |
| 🟡 Parcial | Há rota, BFF ou tela migrada, mas faltam fluxos, detalhe, CRUD, submódulos ou validação de paridade. Não deve ser tratado como substituto integral do legado. |
| ⚪ Stub / bloqueado | Existe rota de placeholder, mas não há fluxo funcional; depende de controller, contrato ou decisão identificada. |
| 🔴 Não migrado | Nenhuma implementação funcional ou contrato de migração foi localizada na base nova. |

## Resultado executivo

- A migração já tem uma fundação consistente: autenticação básica, shell, Cedentes, Operações base e parte relevante de Cadastros possuem implementação.
- Os módulos mais próximos de completar são Financeiro, Relatório Financeiro, Consultas e Administrativo; todos têm contrato e BFF, mas mantêm lacunas explicitamente documentadas.
- O maior volume ainda não iniciado está em Gestora, Financeiro complementar, Relatórios complementares, Ativos, Debêntures, Setup e submódulos especializados de Operações.
- Páginas de Empresas, Faixa de PDD, Regulamento e Esteira de Crédito são apenas stubs e não contam como módulo migrado.

## Inventário por domínio

### Plataforma, acesso e Home

| Módulo legado | Status | Evidência na nova plataforma | Próximo recorte |
|---|---|---|---|
| Autenticação: login, recuperação de senha, contexto FIDC | 🟡 Parcial | Rotas `/login`, `/login/remind-password`, `/setFidcContext` e BFF de autenticação | Validar seleção de tipo de usuário, 2FA, ambiente bloqueado e não autorizado. |
| Home, menu, perfil, notificações e insights | 🟡 Parcial | Shell autenticado, menu, perfil, notificações, dashboard e endpoints `/api/home`, `/api/notifications` | Comparar cards, bankruptcy home e integrações realtime com o legado. |
| Will | 🟡 Parcial | Componente `will-assistant` e BFF `/api/will/message` | Formalizar contrato de conversa, disponibilidade, permissões e estados de erro. |
| Insights | 🟡 Parcial | Componentes de insights e dados de Home | Mapear as telas e serviços próprios do Angular antes de ampliar o fluxo. |

### Cadastros

| Módulo legado | Status | Evidência na nova plataforma | Próximo recorte |
|---|---|---|---|
| Cedentes | ✅ Concluído no escopo atual | Listagem, criação, detalhe por abas e BFF extenso; é a referência visual declarada | Auditar lacunas de contrato e paridade antes de usar como modelo de novos módulos. |
| Sacados | 🟡 Parcial — alinhamento visual concluído | Listagem, BFFs, indicadores, ações, exportação/classificação em lote e detalhe client-side por abas; composição alinhada a Cedentes (`TableSurface`, cards de indicador, `EntityInfoCard` e abas verticais) | Fechar as mutações e formulários dos submódulos legados: representantes, anexos, observações e detalhe de histórico; validar todos os campos do cadastro, complemento e contatos. E2E é acompanhamento posterior e não bloqueia a conclusão funcional. |
| Administradoras, Agentes, Bancarizador, Bancos, Blacklist, Certificadoras, Classificação, Consultoras e Credenciadoras | 🟡 Parcial | Listagens e BFFs em `/api/register/*`; Bancos e Registradoras têm rotas de formulário | Completar formulários, filtros, ações de status, exportação e submódulos conforme contrato. |
| Custodiantes, Emitentes, Fornecedores, Gestoras, Investidores, Originador, Prestadores de Serviços, Produto, Representantes, Testemunhas, WhiteList, Despesas e Grupo Econômico | 🟡 Parcial | Listagens/BFFs do lote 2 | Completar criação, edição, filtros e abas; o lote 2 declara listas como escopo concluído, não o módulo integral. |
| Registradoras | 🟡 Parcial | Lista, criação, edição e BFF | Extrair contrato do legado e fechar fluxos auxiliares/ações não cobertas. |
| Empresas (FIDC), Faixa de PDD, Regulamento e Esteira de Crédito | ⚪ Stub / bloqueado | Rotas mostram “Módulo em desenvolvimento” | Confirmar controllers e vínculo de domínio: Empresas/FIDC, Regulamento/FIDC, Faixa de PDD e Esteira. |
| FIDC, cadastros gerais (`registers`), gavetas/drawer, e-mail de cadastro, notificações de cadastro e ações de usuário | 🔴 Não migrado | Não há módulo/BFF dedicado localizado | Inventariar dependências do contexto FIDC e decidir se cada item é submódulo ou tela independente. |
| FAQ / Manual | 🟡 Parcial | Rota `/home/register/manual-faq` e Ajuda | Verificar paridade do conteúdo, gestão e permissões do FAQ legado. |
| Materiais de crédito (`credit-mat`) e rating | 🔴 Não migrado | Sem rota/BFF dedicado | Extrair contrato e confirmar backend antes de desenhar UI. |

### Operações, recebíveis e ativos

| Módulo legado | Status | Evidência na nova plataforma | Próximo recorte |
|---|---|---|---|
| Operações (lista e detalhe base) | ✅ Concluído no escopo atual | Contrato `operacoes.md`, lista, detalhe e abas/BFF | Implementar ações ainda stub (recusar/reabrir), totalizadores e validar todas as abas. |
| Recebíveis | 🟡 Parcial | Listagem, detalhe, filtros, cards e BFF recém-adicionados | Consolidar contrato, validar payload real e completar operações do legado ligadas a recebíveis. |
| Checagem | 🟡 Parcial | Aba de Operações e endpoint de checagem | Migrar a tela/fluxo independente, regras de permissão e ações do legado. |
| Carteira FIDC | 🔴 Não migrado | Há links de navegação, sem rota funcional localizada | Extrair contrato de `wallet-fidc` e suas dependências em Operações/Gestora. |
| Cobrança, Instruções, Ações de Série, Pós-fixadas e Recebíveis pós-fixados | 🔴 Não migrado | Sem rotas/BFFs dedicados | Migrar após Operações e Recebíveis, reutilizando seus contratos e tipos. |
| Document Servicing v1/v2, Monitoramento NFe/v2 e Simulador | 🔴 Não migrado | Sem rotas/BFFs dedicados | Fazer descoberta técnica; v1/v2 exigem decisão explícita de produto para não duplicar fluxos. |
| Ativos: Nota Comercial | 🔴 Não migrado | Sem rota/BFF dedicado | Extrair contrato, controller e documentos envolvidos. |
| Ativos: CCBs / emissão de CCBs | 🔴 Não migrado | Sem rota/BFF dedicado | Extrair contrato, fluxo de emissão e assinaturas/documentos. |
| Ativos: Cartão de Crédito — agenda, contrato e opt-in | 🔴 Não migrado | Sem rota/BFF dedicado | Tratar como uma frente coesa, com contrato comum e entregas por subfluxo. |

### Financeiro e Gestora

| Módulo legado | Status | Evidência na nova plataforma | Próximo recorte |
|---|---|---|---|
| Movimentação Financeira | 🟡 Parcial | Contrato, lista, saldo, filtros, CRUD, lote, extrato, histórico e BFF | Confirmar endpoints de opções/status e concluir anexos, importação avançada e pendências listadas. |
| Plano de Contas, Contas a Pagar, Contas a Receber, Fluxo de Caixa, Centro de Custo e Movimentos Contábeis | 🔴 Não migrado | Sem módulos/BFFs dedicados | Migrar na ordem Plano de Contas → Centro de Custo → Pagar/Receber → Fluxo → Contábil. |
| Extrato, Fechamento de data financeira e Processo de falência | 🔴 Não migrado | Sem módulos/BFFs dedicados | Depende dos contratos de contas/movimentação e de regras de fechamento. |
| Gestora — Cedentes/Assignors | 🔴 Não migrado | Cedentes gerais não equivalem automaticamente ao módulo Gestora | Mapear diferenças de claim, contexto e operações antes de reutilizar telas. |
| Gestora — Aquisição, Operação, Pagamentos de Operações e Recompras | 🔴 Não migrado | Sem rotas/BFFs dedicados | Migrar após Operações e Financeiro; são fluxos transacionais de alto risco. |
| Gestora — Saldo, Extrato Bancário, PL, Movimentos Abertos, Baixados/Pagos e Dívida | 🔴 Não migrado | Sem rotas/BFFs dedicados | Planejar após a camada financeira compartilhada. |
| Gestora — Recebíveis, Lastro, Registros, Garantias e Prestadores de Serviços | 🔴 Não migrado | Sem rotas/BFFs dedicados | Requer contrato de domínio, documentos e permissões próprias. |
| Gestora — Blacklist | 🔴 Não migrado | Blacklist de Cadastros não prova paridade Gestora | Confirmar se há domínio/rota distinta e evitar reaproveitamento indevido. |

### Relatórios, consultas, administrativo, comunicações e setup

| Módulo legado | Status | Evidência na nova plataforma | Próximo recorte |
|---|---|---|---|
| Consultas externas | 🟡 Parcial | Contrato, lista, filtros, nova consulta, resultados e BFF | Completar detalhes por fonte, histórico QI Tech, lookup de pessoa e validar DTO de fontes. |
| Relatório Financeiro | 🟡 Parcial | Contrato, grade, parâmetros, geração, histórico e BFF | Resolver pendências de opções, concentração, sacados e atualização do histórico. |
| Relatórios de Operações, Cedentes, Contábeis, PL, Debêntures, Estoque, Carteira, Meus Relatórios, Relatório Gestora e Reciprocidade Serasa | 🔴 Não migrado | Sem rotas/BFFs específicos; apenas Relatório Financeiro existe | Inventariar por família e criar uma plataforma comum de geração, histórico e download. |
| Importação de Carteira | 🔴 Não migrado | Sem rota/BFF dedicado | Definir contrato de upload, validação, processamento assíncrono e histórico. |
| Administrativo — Usuários, Grupos, Templates e Emails SMTP | 🟡 Parcial | Contrato, rotas, listas, formulários e BFFs | Completar lacunas do contrato: 2FA, histórico, editor de template, senha SMTP e DTO Pessoa. |
| Administrativo — Pessoas, Consultas Externas, Log de Integração e Log de Implantação | 🔴 Não migrado | Sem rotas/BFFs dedicados | Migrar depois de Administrativo base e Consultas, reutilizando permissões/auditoria. |
| Comunicações — Emails, Notificações e Carta de Cessão | 🟡 Parcial | Menu/notificações globais e páginas administrativas de SMTP | Separar comunicação operacional de configuração SMTP; extrair contratos para Email, Notification e Carta de Cessão. |
| Dashboard — principal, Fundos, Resumo Operacional, Resumo Diário, Black BI e Monitoramento NFe | 🟡 Parcial | Home dashboard é implementado, porém não há rotas equivalentes por dashboard | Definir quais dashboards substituem Home e quais exigem paridade de dados/visualização. |
| Setup — Cadastro de Fundo e Migração de Dados | 🔴 Não migrado | Sem rota/BFF dedicado | Migrar após FIDC e Cadastros estruturantes; possui impacto administrativo alto. |
| Debêntures — Emissão e Vendas | 🔴 Não migrado | Sem rota/BFF dedicado | Criar descoberta específica de emissão, documentos, agenda e permissões. |

## Ordem recomendada e cronograma

Premissas deste cronograma: sprints de duas semanas, uma squad com capacidade
para uma frente complexa ou duas frentes pequenas em paralelo, e validação do
backend disponível durante cada sprint. As datas devem ser recalculadas se
houver outra capacidade; a ordem e os gates são mais importantes que a duração.

| Onda | Momento | Foco da semana | Mensagem para gerência | Risco principal | Decisão ou apoio esperado | Critério de saída |
|---|---|---|---|---|---|---|
| 0 — Governança e estabilização | Sprints 1–2 | Auditar Cedentes, Operações, Recebíveis, Cadastros parciais e remover stubs que pareçam entregas. | "Vamos separar o que está pronto de verdade do que só aparece na navegação." | Criar expectativa errada sobre telas parciais. | Validar que paridade e contrato são gates obrigatórios. | Matriz de paridade por tela, contratos atualizados e pendências classificadas. |
| 0A — Fechamento de Sacados | Em curso | Consolidar Sacados sobre a referência Cedentes e concluir CRUD/submódulos existentes no Angular. | "Sacados já ganhou forma; agora falta fechar os fluxos que fazem o módulo ser realmente substituto do legado." | Tratar alinhamento visual como conclusão funcional. | Confirmar que E2E é acompanhamento posterior, não bloqueio deste gate funcional. | Nenhum fluxo existente no legado classificado como `LEGADO MIGRADO`; contrato `sacados.md` com evidência Angular/API/BFF/UI. |
| 1 — Fechar o núcleo em andamento | Sprints 3–5 | Recebíveis, Movimentação Financeira, Consultas, Relatório Financeiro e Administrativo. | "A melhor alavanca agora é terminar o que já começou e reduzir pontas soltas." | Fluxos transacionais sem payload real validado. | Disponibilidade de backend/produto para validar lacunas críticas. | Payload real validado, lacunas críticas resolvidas/aceitas e E2E dos fluxos transacionais. |
| 2 — Cadastros estruturantes | Sprints 6–8 | FIDC/Empresas, Regulamento, Bancos/Registradoras e formulários dos cadastros já listados. | "Aqui a gente organiza a base que alimenta vários outros módulos." | Cadastros incompletos travarem selects, permissões e regras futuras. | Confirmar controllers, claims e prioridade dos cadastros obrigatórios. | Controllers e claims confirmados; uma base de CRUD reutilizável por cadastro. |
| 3 — Financeiro compartilhado | Sprints 9–12 | Plano de Contas, Centro de Custo, Contas a Pagar/Receber, Fluxo de Caixa e Contábil. | "É uma onda de alto impacto: mexe com dinheiro, datas, fechamento e conciliação." | Regra financeira incompleta virar retrabalho caro. | Validação próxima de negócio, financeiro e backend. | Contratos de fechamento, moeda, datas e permissões confirmados. |
| 4 — Operações especializadas | Sprints 13–15 | Carteira FIDC, Cobrança, Instruções, pós-fixados, Checagem completa e documentos/monitoramento. | "Depois do núcleo estável, entramos nos fluxos mais específicos de operação." | Duplicar fluxos v1/v2 ou migrar documentos sem decisão clara. | Decisão explícita para Document Servicing v1/v2 e monitoramentos. | Operações/Recebíveis estáveis; decisão para Document Servicing v1/v2. |
| 5 — Gestora | Sprints 16–20 | Aquisição, Operação, pagamentos, recompras, saldo/extrato/PL e lastro. | "Gestora é uma frente grande e sensível; precisa entrar com base financeira madura." | Reaproveitar telas gerais sem respeitar claims, contexto e regras próprias. | Priorização executiva dos fluxos críticos e agenda de validação de mutações. | Reutilização controlada da camada financeira; E2E de mutações críticas. |
| 6 — Relatórios e dashboards | Sprints 21–23 | Famílias de relatórios, importação de carteira e dashboards com contratos de dados comuns. | "Com os dados transacionais mais estáveis, relatórios deixam de ser chute e viram produto confiável." | Criar visualizações antes de estabilizar origem, histórico e download. | Definir famílias prioritárias e padrão comum de geração. | Plataforma de geração/download e decisões do design system para visualizações ausentes. |
| 7 — Frentes especializadas | Sprints 24–27 | Ativos, Cartão, CCB, Debêntures, Setup, logs administrativos e Carta de Cessão. | "São frentes importantes, mas especializadas; entram melhor quando a espinha dorsal já está pronta." | Compliance, documentos e produto sem contrato aprovado. | Aprovação de contratos de produto, documentos e compliance. | Contratos de produto, documentos e compliance aprovados. |
| 8 — Corte e desativação | Sprints 28–30 | Paridade final, migração de usuários, observabilidade, regressão e retirada gradual do Angular. | "Aqui deixamos de conviver com dois mundos e preparamos a virada com controle." | Desativar Angular com rota crítica ainda dependente do legado. | Aprovar plano de corte, comunicação e rollback. | Nenhuma rota crítica dependente do legado; plano de rollback documentado. |

### Regras de priorização dentro de cada onda

1. Fechar primeiro os módulos parcialmente migrados com contrato existente: reduz risco e evita duplicar a descoberta.
2. Migrar antes os cadastros e domínios que alimentam selects e regras de outros módulos.
3. Tratar transações financeiras, permissões, documentos, exportações e importações como alto risco: exigem contrato, testes e validação de payload real antes de paridade visual fina.
4. Manter dashboards e relatórios dependentes depois que os dados transacionais e os contratos de agregação estiverem estáveis.
5. Não iniciar implementação de módulo ⚪/🔴 sem contrato em `docs/migracao/<modulo>.md`.
