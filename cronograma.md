# Inventário e cronograma de migração Angular → React

> Atualizado em 24/07/2026 (v2 — Cadastros Register). Este documento compara os módulos funcionais em
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
| Onde estamos bem? | Fundação da aplicação, Cedentes, Operações base, Cadastros (CRUD principal + lookup) e avanço visual/funcional de Sacados. |
| O que está quase virando entrega fechada? | Cadastros Register (faltam apenas submódulos e filtros avançados), Sacados, Recebíveis, Movimentação Financeira, Consultas, Relatório Financeiro e Administrativo. |
| Onde mora o maior risco? | Fluxos financeiros, Gestora, importações/exportações, documentos, permissões e módulos que ainda não têm contrato. |
| O que não deve ser vendido como pronto? | Stubs, listas isoladas sem CRUD completo, submódulos de Cadastros (representantes, complemento, comissão, QDD, layout extrato) e módulos marcados como parcial sem validação de paridade. |
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

- A migração tem fundação consistente: autenticação básica, shell, Cedentes, Operações base e **Cadastros Register com CRUD principal completo** (Administradoras, Agentes, Bancarizador, Bancos, Blacklist, Certificadoras, Classificação, Consultoras e Credenciadoras).
- **Cadastros Register** em 24/07/2026: CRUD principal entregue — formulários, páginas `/new` e `/[id]/edit`, BFFs POST/PUT, hooks React Query, dialog de lookup de CNPJ/CPF para os módulos com PessoaViewModel (ADM, AGE, CON) e ações de status/observação na Blacklist. Pendências remanescentes: submódulos (representantes, complemento, comissão, QDD, layout extrato), filtros avançados, exportação server-side, Credenciadora activate e Blacklist delete (ambos A INVESTIGAR NA API).
- Os módulos mais próximos de completar são Cadastros Register (submódulos restantes), Recebíveis, Movimentação Financeira, Consultas, Relatório Financeiro e Administrativo; todos têm contrato e BFF, mas mantêm lacunas explicitamente documentadas.
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
| Cedentes | ✅ Concluído no escopo atual | Listagem, criação, detalhe por abas e BFF extenso; referência visual declarada | Auditar lacunas de contrato e paridade antes de usar como modelo de novos módulos. |
| Sacados | 🟡 Parcial — alinhamento visual concluído | Listagem, BFFs, indicadores, ações, exportação/classificação em lote e detalhe client-side por abas; composição alinhada a Cedentes | Fechar mutações e formulários dos submódulos legados: representantes, anexos, observações e detalhe de histórico; validar todos os campos do cadastro, complemento e contatos. |
| Administradoras | 🟡 Parcial — CRUD + lookup CNPJ concluídos | Lista, BFF `/api/register/administradoras`, formulário (RHF+Zod, 15 campos PJ), `/new` + `/[id]/edit`, dialog de lookup CNPJ, BFF `/lookup`, activate/deactivate/delete | Submódulos: representantes, complemento (`nomeApresentacao`), tipos-recebíveis; filtros avançados; exportação server-side. |
| Agentes | 🟡 Parcial — CRUD + lookup CPF/CNPJ concluídos | Lista, BFF `/api/register/agentes`, formulário PF/PJ com toggle `tipoPessoa`, `/new` + `/[id]/edit`, dialog de lookup CPF/CNPJ, BFF `/lookup`, activate/deactivate/delete | Submódulos: comissão (sub-aba financeira); filtros avançados; exportação server-side. |
| Bancarizador | 🟡 Parcial — CRUD concluído | Lista, BFF `/api/register/bancarizador`, formulário (criação com nome+CNPJ; edição só observação), `/new` + `/[id]/edit`, activate/deactivate/delete | Filtros avançados; exportação server-side. |
| Bancos | 🟡 Parcial — CRUD concluído | Lista, BFF `/api/register/bancos`, formulário, `/new` + `/[id]/edit`, activate/deactivate/delete | Layout de extrato (claims `L_BAN_LAY`/`E_BAN_LAY`) adiado; filtros avançados. |
| Blacklist | 🟡 Parcial — ações de status/observação concluídas | Lista, BFF `/api/register/blacklist`, modals “Definir status” e “Adicionar observação” com upload de arquivo | Criação via Excel import (adiado); delete: A INVESTIGAR NA API; histórico de importação; filtros avançados. |
| Certificadoras | ✅ Concluído no escopo atual | Lista, BFF `/api/register/certificadoras`, formulário, `/new` + `/[id]/edit`, activate/deactivate/delete | Sem submódulos documentados. Filtros avançados e exportação server-side se necessário. |
| Classificação | ✅ Concluído no escopo atual | Lista, BFF `/api/register/classificacoes`, formulário (nome, cor, descrição, tipoClassificacao), `/new` + `/[id]/edit`, delete | Sem ações de status no Angular; sem submódulos. |
| Consultoras | 🟡 Parcial — CRUD + lookup CNPJ concluídos | Lista, BFF `/api/register/consultoras`, formulário (15 campos PJ), `/new` + `/[id]/edit`, dialog de lookup CNPJ, BFF `/lookup`, activate/deactivate/delete | Submódulos: complemento (`nomeApresentacao`, `gestoraBackendUrl`), QDD, representantes; filtros avançados; exportação server-side. |
| Credenciadoras | 🟡 Parcial — CRUD + inativação concluídos | Lista, BFF `/api/register/credenciadoras`, formulário, `/new` + `/[id]/edit`, deactivate/delete | Activate: **A INVESTIGAR NA API** (endpoint não localizado); filtros avançados; exportação server-side. |
| Custodiantes | 🟡 Parcial — lista concluída | Listagem e BFF (`/api/register/custodiantes`) do lote 2 | Completar criação, edição, filtros, ações e abas; o lote 2 declara lista como escopo concluído, não o módulo integral. |
| Emitentes | 🟡 Parcial — lista concluída | Listagem e BFF do lote 2 | Idem Custodiantes. |
| Fornecedores | 🟡 Parcial — lista concluída | Listagem e BFF do lote 2 | Idem Custodiantes. |
| Gestoras (cadastro) | 🟡 Parcial — lista concluída | Listagem e BFF do lote 2 (módulo distinto de Gestora operacional) | Idem Custodiantes. Confirmar separação de claims com Gestora operacional. |
| Investidores | 🟡 Parcial — lista concluída | Listagem e BFF do lote 2 | Idem Custodiantes. |
| Originador | 🟡 Parcial — lista concluída | Listagem e BFF do lote 2 | Idem Custodiantes. |
| Prestadores de Serviços | 🟡 Parcial — lista concluída | Listagem e BFF do lote 2 | Idem Custodiantes. |
| Produto | 🟡 Parcial — lista concluída | Listagem e BFF do lote 2 | Idem Custodiantes. |
| Representantes (cadastro) | 🟡 Parcial — lista concluída | Listagem e BFF do lote 2 | Idem Custodiantes. |
| Testemunhas | 🟡 Parcial — lista concluída | Listagem e BFF do lote 2 | Idem Custodiantes. |
| WhiteList | 🟡 Parcial — lista concluída | Listagem e BFF do lote 2 | Idem Custodiantes. |
| Despesas | 🟡 Parcial — lista concluída | Listagem e BFF do lote 2 | Idem Custodiantes. |
| Grupo Econômico | 🟡 Parcial — lista concluída | Listagem e BFF do lote 2 | Idem Custodiantes. |
| Registradoras | 🟡 Parcial — CRUD concluído | Lista, criação, edição e BFF (`/api/register/registradoras`) | Extrair contrato do legado e fechar fluxos auxiliares/ações não cobertas. |
| Empresas (FIDC) | ⚪ Stub / bloqueado | Rota mostra “Módulo em desenvolvimento” | Confirmar controller e vínculo de domínio FIDC. |
| Faixa de PDD | ⚪ Stub / bloqueado | Rota mostra “Módulo em desenvolvimento” | Confirmar controller e regras de PDD. |
| Regulamento | ⚪ Stub / bloqueado | Rota mostra “Módulo em desenvolvimento” | Confirmar controller e vínculo de domínio FIDC. |
| Esteira de Crédito | ⚪ Stub / bloqueado | Rota mostra “Módulo em desenvolvimento” | Confirmar controller e pipeline de crédito. |
| FIDC (contexto/cadastro geral) | 🔴 Não migrado | Não há módulo/BFF dedicado localizado | Inventariar dependências do contexto FIDC antes de estimar. |
| Gavetas / Drawer | 🔴 Não migrado | Sem rota/BFF dedicado | Decidir se é submódulo de FIDC ou tela independente. |
| E-mail de cadastro | 🔴 Não migrado | Sem rota/BFF dedicado | Mapear templates e triggers antes de migrar. |
| Notificações de cadastro | 🔴 Não migrado | Sem rota/BFF dedicado | Consolidar com módulo de Comunicações/Administrativo. |
| Ações de usuário | 🔴 Não migrado | Sem rota/BFF dedicado | Inventariar logs e permissões antes de estimar. |
| FAQ / Manual | 🟡 Parcial | Rota `/home/register/manual-faq` e Ajuda | Verificar paridade do conteúdo, gestão e permissões do FAQ legado. |
| Materiais de crédito (`credit-mat`) | 🔴 Não migrado | Sem rota/BFF dedicado | Extrair contrato e confirmar backend antes de desenhar UI. |
| Rating | 🔴 Não migrado | Sem rota/BFF dedicado | Definir se é submódulo de Materiais de crédito ou tela independente. |

### Operações, recebíveis e ativos

| Módulo legado | Status | Evidência na nova plataforma | Próximo recorte |
|---|---|---|---|
| Operações (lista e detalhe base) | ✅ Concluído no escopo atual | Contrato `operacoes.md`, lista, detalhe e abas/BFF | Implementar ações ainda stub (recusar/reabrir), totalizadores e validar todas as abas. |
| Recebíveis | 🟡 Parcial | Listagem, detalhe, filtros, cards e BFF recém-adicionados | Consolidar contrato, validar payload real e completar operações do legado ligadas a recebíveis. |
| Checagem | 🟡 Parcial | Aba de Operações e endpoint de checagem | Migrar a tela/fluxo independente, regras de permissão e ações do legado. |
| Carteira FIDC | 🔴 Não migrado | Há links de navegação, sem rota funcional localizada | Extrair contrato de `wallet-fidc` e suas dependências em Operações/Gestora. |
| Cobrança | 🔴 Não migrado | Sem rota/BFF dedicado | Migrar após Operações e Recebíveis, reutilizando seus contratos e tipos. |
| Instruções | 🔴 Não migrado | Sem rota/BFF dedicado | Idem Cobrança. |
| Ações de Série | 🔴 Não migrado | Sem rota/BFF dedicado | Idem Cobrança. |
| Pós-fixadas | 🔴 Não migrado | Sem rota/BFF dedicado | Idem Cobrança. |
| Recebíveis pós-fixados | 🔴 Não migrado | Sem rota/BFF dedicado | Idem Cobrança. |
| Document Servicing v1 | 🔴 Não migrado | Sem rota/BFF dedicado | Decisão explícita de produto necessária para não duplicar com v2. |
| Document Servicing v2 | 🔴 Não migrado | Sem rota/BFF dedicado | Decisão explícita de produto necessária para não duplicar com v1. |
| Monitoramento NFe / v2 | 🔴 Não migrado | Sem rota/BFF dedicado | Fazer descoberta técnica; verificar sobreposição com Dashboard Monitoramento NFe. |
| Simulador | 🔴 Não migrado | Sem rota/BFF dedicado | Extrair contrato e confirmar backend antes de estimar. |
| Ativos: Nota Comercial | 🔴 Não migrado | Sem rota/BFF dedicado | Extrair contrato, controller e documentos envolvidos. |
| Ativos: CCBs / emissão de CCBs | 🔴 Não migrado | Sem rota/BFF dedicado | Extrair contrato, fluxo de emissão e assinaturas/documentos. |
| Ativos: Cartão de Crédito — agenda, contrato e opt-in | 🔴 Não migrado | Sem rota/BFF dedicado | Tratar como uma frente coesa, com contrato comum e entregas por subfluxo. |

### Financeiro e Gestora

| Módulo legado | Status | Evidência na nova plataforma | Próximo recorte |
|---|---|---|---|
| Movimentação Financeira | 🟡 Parcial | Contrato, lista, saldo, filtros, CRUD, lote, extrato, histórico e BFF | Confirmar endpoints de opções/status e concluir anexos, importação avançada e pendências listadas. |
| Plano de Contas | 🔴 Não migrado | Sem rota/BFF dedicado | Migrar primeiro; alimenta Centro de Custo, Contas a Pagar/Receber e Contábil. |
| Centro de Custo | 🔴 Não migrado | Sem rota/BFF dedicado | Migrar após Plano de Contas. |
| Contas a Pagar | 🔴 Não migrado | Sem rota/BFF dedicado | Migrar após Plano de Contas e Centro de Custo. |
| Contas a Receber | 🔴 Não migrado | Sem rota/BFF dedicado | Migrar após Plano de Contas e Centro de Custo. |
| Fluxo de Caixa | 🔴 Não migrado | Sem rota/BFF dedicado | Depende de Contas a Pagar e Contas a Receber. |
| Movimentos Contábeis | 🔴 Não migrado | Sem rota/BFF dedicado | Migrar após camada de contas e lançamentos. |
| Extrato financeiro | 🔴 Não migrado | Sem rota/BFF dedicado | Depende dos contratos de contas e movimentação. |
| Fechamento de data financeira | 🔴 Não migrado | Sem rota/BFF dedicado | Requer regras de fechamento e permissões específicas. |
| Processo de falência | 🔴 Não migrado | Sem rota/BFF dedicado | Alto risco legal; extrair contrato antes de estimar. |
| Gestora — Cedentes/Assignors | 🔴 Não migrado | Cedentes gerais não equivalem automaticamente ao módulo Gestora | Mapear diferenças de claim, contexto e operações antes de reutilizar telas. |
| Gestora — Aquisição | 🔴 Não migrado | Sem rota/BFF dedicado | Fluxo transacional de alto risco; migrar após Operações e Financeiro. |
| Gestora — Operação | 🔴 Não migrado | Sem rota/BFF dedicado | Idem Aquisição. |
| Gestora — Pagamentos de Operações | 🔴 Não migrado | Sem rota/BFF dedicado | Idem Aquisição. |
| Gestora — Recompras | 🔴 Não migrado | Sem rota/BFF dedicado | Idem Aquisição. |
| Gestora — Saldo | 🔴 Não migrado | Sem rota/BFF dedicado | Planejar após camada financeira compartilhada. |
| Gestora — Extrato Bancário | 🔴 Não migrado | Sem rota/BFF dedicado | Idem Saldo. |
| Gestora — PL | 🔴 Não migrado | Sem rota/BFF dedicado | Idem Saldo. |
| Gestora — Movimentos Abertos / Baixados / Pagos | 🔴 Não migrado | Sem rota/BFF dedicado | Idem Saldo. |
| Gestora — Dívida | 🔴 Não migrado | Sem rota/BFF dedicado | Idem Saldo. |
| Gestora — Recebíveis | 🔴 Não migrado | Sem rota/BFF dedicado | Requer contrato de domínio, documentos e permissões próprias. |
| Gestora — Lastro | 🔴 Não migrado | Sem rota/BFF dedicado | Idem Recebíveis Gestora. |
| Gestora — Registros | 🔴 Não migrado | Sem rota/BFF dedicado | Idem Recebíveis Gestora. |
| Gestora — Garantias | 🔴 Não migrado | Sem rota/BFF dedicado | Idem Recebíveis Gestora. |
| Gestora — Prestadores de Serviços | 🔴 Não migrado | Sem rota/BFF dedicado | Idem Recebíveis Gestora. Verificar sobreposição com Prestadores em Cadastros. |
| Gestora — Blacklist | 🔴 Não migrado | Blacklist de Cadastros não prova paridade Gestora | Confirmar se há domínio/rota distinta e evitar reaproveitamento indevido. |

### Relatórios, consultas, administrativo, comunicações e setup

| Módulo legado | Status | Evidência na nova plataforma | Próximo recorte |
|---|---|---|---|
| Consultas externas | 🟡 Parcial | Contrato, lista, filtros, nova consulta, resultados e BFF | Completar detalhes por fonte, histórico QI Tech, lookup de pessoa e validar DTO de fontes. |
| Relatório Financeiro | 🟡 Parcial | Contrato, grade, parâmetros, geração, histórico e BFF | Resolver pendências de opções, concentração, sacados e atualização do histórico. |
| Relatório de Operações | 🔴 Não migrado | Sem rota/BFF dedicado | Inventariar por família; criar plataforma comum de geração, histórico e download. |
| Relatório de Cedentes | 🔴 Não migrado | Sem rota/BFF dedicado | Idem Relatório de Operações. |
| Relatório Contábil | 🔴 Não migrado | Sem rota/BFF dedicado | Idem Relatório de Operações. |
| Relatório de PL | 🔴 Não migrado | Sem rota/BFF dedicado | Idem Relatório de Operações. |
| Relatório de Debêntures | 🔴 Não migrado | Sem rota/BFF dedicado | Idem Relatório de Operações. |
| Relatório de Estoque | 🔴 Não migrado | Sem rota/BFF dedicado | Idem Relatório de Operações. |
| Relatório de Carteira | 🔴 Não migrado | Sem rota/BFF dedicado | Idem Relatório de Operações. |
| Meus Relatórios | 🔴 Não migrado | Sem rota/BFF dedicado | Requer plataforma de relatórios compartilhada. |
| Relatório Gestora | 🔴 Não migrado | Sem rota/BFF dedicado | Migrar após Gestora operacional. |
| Reciprocidade Serasa | 🔴 Não migrado | Sem rota/BFF dedicado | Extrair contrato de integração Serasa antes de estimar. |
| Importação de Carteira | 🔴 Não migrado | Sem rota/BFF dedicado | Definir contrato de upload, validação, processamento assíncrono e histórico. |
| Administrativo — Usuários | 🟡 Parcial | Contrato, rotas, lista, formulário e BFF | Completar 2FA, histórico e DTO Pessoa. |
| Administrativo — Grupos | 🟡 Parcial | Contrato, rotas, lista, formulário e BFF | Completar gestão de permissões e herança de claims. |
| Administrativo — Templates de e-mail | 🟡 Parcial | Contrato, rotas, lista, formulário e BFF | Completar editor de template HTML. |
| Administrativo — Emails SMTP | 🟡 Parcial | Contrato, rotas, lista, formulário e BFF | Completar senha SMTP e validação de conexão. |
| Administrativo — Pessoas | 🔴 Não migrado | Sem rota/BFF dedicado | Migrar depois de Administrativo base; reutilizar DTO Pessoa do módulo de Usuários. |
| Administrativo — Consultas Externas | 🔴 Não migrado | Sem rota/BFF dedicado | Migrar depois de Consultas externas. |
| Administrativo — Log de Integração | 🔴 Não migrado | Sem rota/BFF dedicado | Extrair contrato de auditoria e permissões antes de estimar. |
| Administrativo — Log de Implantação | 🔴 Não migrado | Sem rota/BFF dedicado | Idem Log de Integração. |
| Comunicações — Emails | 🟡 Parcial | Notificações globais e SMTP administrativo | Separar comunicação operacional de configuração; extrair contrato de disparo. |
| Comunicações — Notificações | 🟡 Parcial | Menu de notificações e endpoint `/api/notifications` | Extrair contrato de tipos de notificação e ações de leitura/marcação. |
| Comunicações — Carta de Cessão | 🔴 Não migrado | Sem rota/BFF dedicado | Extrair contrato de geração, assinatura e download antes de estimar. |
| Dashboard principal | 🟡 Parcial | Home dashboard implementado | Validar paridade de cards e dados com o legado. |
| Dashboard — Fundos | 🟡 Parcial | Sem rota equivalente dedicada | Definir se substitui Home ou exige rota própria. |
| Dashboard — Resumo Operacional | 🟡 Parcial | Sem rota equivalente dedicada | Idem Fundos. |
| Dashboard — Resumo Diário | 🟡 Parcial | Sem rota equivalente dedicada | Idem Fundos. |
| Dashboard — Black BI | 🔴 Não migrado | Sem rota/BFF dedicado | Avaliar integração de BI antes de estimar tela. |
| Dashboard — Monitoramento NFe | 🟡 Parcial | Componente de monitoramento referenciado | Extrair contrato de dados em tempo real. |
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
| 2 — Cadastros estruturantes | Sprints 6–8 ✅ CRUD principal concluído | **CRUD principal de todos os 9 módulos entregue.** Restam: submódulos (representantes, complemento, comissão, QDD, layout extrato), filtros avançados, exportação server-side, dialog de lookup para ADM/AGE/CON, FIDC/Empresas, Regulamento. | "Base dos cadastros está operacional; submódulos e módulos legados de contexto FIDC são próxima etapa." | Submódulos bloqueados por componentes shared ainda não criados (histórico, abas, representantes). | Priorizar os submódulos mais usados operacionalmente antes de expandir para FIDC. | Submódulos e filtros avançados entregues; controllers de FIDC/Empresas confirmados. |
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
