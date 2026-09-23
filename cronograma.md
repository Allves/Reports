# Inventario e cronograma de migracao Angular -> React

> **Criterio vigente (22/09/2026):** o Angular legado e a fonte de paridade para escopo, campos, ordem, controles, acoes, payloads e comportamento. O aceite usa implementacao Admin/BFF, paridade Angular, validacao local e evidencia de teste.
>
> Homologacao, disponibilidade upstream, persistencia integrada, policies implantadas e ausencia de controller no snapshot sao acompanhamento nao bloqueante. Nenhum desses pontos reduz o percentual de conclusao e nenhum e registrado como homologacao executada.

## Correcao da pendencia reportada

O item `Validar payloads, claims e homologacao do cadastro` foi retirado do criterio vigente. Ele permanece somente no historico, identificado como substituido. O criterio atual e conferir payloads, claims, campos, acoes e permissoes contra o Angular, transportar o contrato pelo BFF e validar o fluxo localmente.

## Matriz corrente de fechamento (22/09/2026)

| Lote | Cadastros | Aceite local | Acompanhamento externo |
| --- | --- | --- | --- |
| C0 | Cedentes, Administradoras, Representantes, Gestoras, Custodiantes, Agentes e Bancarizador | Abas, acoes, payloads, comissoes/faixas, claims e resposta parcial cobertos localmente | upstream, persistencia integrada e policies |
| C1 | Certificadoras, Classificacao, Bancos, Credenciadoras, Registradoras, Despesas, Grupo Economico e Produto | CRUD, filtros, historico, HTML/layout, rateio/vinculos e regras Angular | controller/DTO ausente no snapshot e runtime integrado |
| C2 | Sacados e Consultoras | criacao PF/PJ, lookup, filtros, paginacao e QDD | respostas do servico integrado |
| C3 | Fornecedores, Testemunhas, Originador, Investidores e Prestadores | criacao/edicao, Pessoa, vinculos, multipart, enums e remocao pelo verbo Angular | servicos externos e persistencia integrada |
| C4 | WhiteList, Blacklist e Emitentes | filtros, importacao, template, exportacao, historico, recusados e falhas parciais | fila, storage e upstream |
| C5 | Empresas/FIDC, Regulamento, Faixa de PDD e Cadastro de Fundo | controles equivalentes ao legado, wizard de 13 etapas, retomada, documentos, termos, configuracoes e RAG | persistencia integrada e upstream |
| C6 | Esteira de Credito | fases, responsaveis, colapsos, checklists, documentos, pareceres, comite e historico com consultas simuladas | disponibilidade de consultas externas |
| C7 | Usuarios, Grupos, Templates, SMTP, Pessoas, Plano de Contas, Centro de Custo, FAQ e Releases | associacoes, credenciais, bootstrap client/BFF, DOCX, HTML, cadastros financeiros e acessos auxiliares | conteudo externo e SMTP |
| C8 | Todos os lotes | validate:apps, build:admin, typecheck/lint e E2E locais focados aprovados; validate executado ate o gate de manifesto | CLIENTS_MANIFEST_FILE/KV ausentes; nenhum teste integrado |

## Matriz por cadastro e funcionalidade

A matriz auditavel das 37 frentes e dos dois acessos auxiliares esta em [evidencias-fechamento-cadastros-admin.md](./evidencias-fechamento-cadastros-admin.md). Cada linha registra origem Angular, superficie Admin/BFF, validacao local e acompanhamento externo. Essa e a referencia operacional por cadastro; os status antigos abaixo sao apenas historicos.

| Resultado corrente | Quantidade |
| --- | ---: |
| Cadastros concluidos localmente | 37/37 |
| Acessos auxiliares validados localmente | 2/2 |
| Excecao de escopo | Acoes de Usuario, sem fluxo cadastral comprovado no Angular |

`Acoes de Usuario` e a unica excecao de escopo. Handlers vazios do Angular permanecem classificados como ausencia de funcionalidade legada, sem requisito inventado. Testes de ambiente integrado nao fazem parte do aceite.

## Fluxo de aceite

`Angular -> Admin -> BFF -> mocks locais -> evidencia -> fechamento`

O acompanhamento externo permanece separado e nunca rebaixa um cadastro para Parcial.

<details>
<summary>Historico preservado (criterios substituidos)</summary>

> **Nota de leitura:** qualquer `Parcial`, `Pendente`, `homologacao` ou
> `Validar payloads, claims e homologacao` nas tabelas abaixo pertence ao
> registro anterior. Esses textos nao sao pendencias vigentes e nao alteram os
> 37/37 fechamentos locais; a matriz corrente no inicio deste documento prevalece.

# Inventário e cronograma de migração Angular → React

> **Auditoria de Classificação — 16/09/2026:** o fluxo foi reconciliado com o
> `rating` Angular e com `ClassificacaoController`: filtro por nome/cor/descrição,
> paginação e ordenação agora percorrem client/BFF/API; nome (máximo 50) e cor
> hexadecimal são validados; e o tipo permanece somente leitura na edição, sem
> ser enviado ao `PUT` que não o suporta. O cenário foi incluído e aprovado na
> suíte E2E C1.

> **Auditoria complementar — autorização cadastral — 16/09/2026:** no Admin,
> as claims esperadas para Histórico de Agente foram alinhadas a
> `L/W/E/R_AGE_HIS`; documentos do Custodiante a `L/W/E/R_CUS_DOC`; e a leitura
> de Investidor a `L_INV`, sem exigir edição. Histórico de Classificação e
> Dashboard de Sacados também referenciam suas classes específicas. A API e o
> legado permaneceram somente leitura; a conferência definitiva de
> `Policy.Name` versus `Claims.Type` depende do runtime integrado.

> **Auditoria de payload — Agentes — 16/09/2026:** `desagioRecebivel` foi
> confirmado no contrato funcional do legado e passou a ser preservado pelo
> payload do Admin. A API e o legado não foram alterados. A validação de schema,
> tipos, limites e transporte é automatizável; o aceite da equivalência
> funcional da comissão continua exigindo cenários manuais/E2E no ambiente
> integrado.

> **Execução complementar — 16/09/2026 (continuação):** C6 avançou com o
> responsável comercial da Proposta, filtro por agente, exportação Excel,
> campos/tabelas editáveis nos colapsos e documentos obrigatórios (status,
> upload ZIP em lote, downloads e histórico). C7 avançou com os detalhes de
> Usuários, Grupos, Templates e SMTP consumindo BFF/React Query a partir do
> bootstrap client. A auditoria não encontrou uma integração independente no
> fluxo legado da Esteira; consultas externas permanecem parte do detalhe e
> aguardam homologação. Login, permissões compartilhadas, sessão/refresh e 2FA
> continuam protegidos e inalterados. C5 também passou a preservar e editar os
> campos adicionais do contrato de Complemento do FIDC, incluindo estruturas
> JSON validadas, sem descartar propriedades não exibidas.

> **Double check de bootstrap e paridade — 16/09/2026:** Administradoras,
> Representantes e Consultoras (listas), Cedentes (detalhe) e Bancos (detalhe)
> foram convertidos para o bootstrap client/BFF/React Query compartilhado,
> eliminando a dependência de SSR nesses consumidores. Templates passaram a
> usar `RichTextEditor` sanitizado para HTML. Emitentes ganhou exportação
> server-side via `POST /api/emitente/get/list/export`; permanece pendente a
> homologação de payloads, policies e respostas do ambiente integrado.

> **Execução complementar — C7 administrativo:** Grupos passou a incluir
> Usuários vinculados, Anexos, Observações e Histórico; Templates passou a
> incluir Histórico; e SMTP passou a incluir Anexos, Observações e Histórico.
> Os BFFs do Admin consomem os controllers genéricos disponíveis, preservando
> as associações 43, 16 e 44. A validação da policy no runtime integrado ainda
> é gate pendente; login, permissões compartilhadas, sessão/refresh e 2FA
> permanecem inalterados.

> No mesmo recorte C7, Usuários passou a editar o contrato de Pessoa PF/PJ
> disponível na API, incluindo endereços, contatos e QSA, além de Anexos,
> Observações e Histórico com associação 13 e claims `USU_*`. Credenciais API
> continuam bloqueadas por ausência dos endpoints correspondentes na API
> versionada verificada.

> **Execução complementar — 16/09/2026:** Bancos preserva busca por nome/código
> e ordenação no fluxo client/BFF. Produto preserva no formulário e no BFF os
> campos e o payload `dadosAdicionais` observados no legado, valida a
> exclusividade Fee/Custo no Admin, expõe Histórico no detalhe e lista contas
> de repasse por FIDC. A API não foi alterada e o snapshot atual não declara
> esses campos/rota; persistência e resposta real ficam pendentes de runtime.
> A Esteira
> carrega os colapsos de Dados Cadastrais, Parecer Comercial, Grupo, Jurídico,
> Faturamento, Endividamento, Pesquisa de Mercado, Balanço e Fotos/Visita,
> com edição segura das observações. Releases ganhou a rota Admin equivalente
> ao `manual-release`. Permanecem pendentes integração e
> homologação; responsáveis, tabelas editáveis e documentos obrigatórios já
> foram implementados na vertical da Proposta.

> **Auditoria de payload — Bancos — 16/09/2026:** a validação estática do Layout
> de Extrato foi fechada no BFF do Admin para coleção, tipos reconhecidos,
> apelidos, duplicidade e limite. O valor `11`, oferecido pelo Angular, foi
> preservado no contrato enviado pelo Admin; a interpretação no parser, a
> persistência e a resposta real continuam gates do runtime integrado.

> **Auditoria de payload — Contatos de Sacados — 16/09/2026:** o contrato foi
> alinhado ao Angular: `L_SAC_CTT` somente para leitura e `W_SAC_CTT` para a
> substituição completa da lista. O BFF valida os campos obrigatórios, aceita o
> tipo `Financeiro` (`5`) e remove metadados de tela antes do `PUT` da API. A
> validação integrada do payload e dos claims sem MASTER permanece pendente.

> **Execução complementar — filtros C3 — 16/09/2026:** as cinco listagens do
> lote 2 passaram a preservar filtros e ordenação no URL, com o BFF encaminhando
> os parâmetros equivalentes ao contrato Angular. Originador inclui os estados
> Ativo, Inativo e Bloqueado; Fornecedores, Testemunhas e Investidores incluem
> palavra-chave/data; Prestadores separa nome/documento/data. A alteração cobre
> a paridade de consulta do frontend, mas a validação de payload, claims e
> resposta real ainda depende do ambiente integrado.

> O Regulamento do FIDC também passou a expor os campos numéricos, enums de
> estoque/indexador e regras de coobrigação previstos no
> `UpdateRegulamentoAbaViewModel`. A trilha de opções de PDD e Ambientes ainda
> depende de contratos específicos; a vertical de Faixa de PDD foi preparada
> no Admin a partir das requisições do legado, mas o controller/DTO não está
> disponível no snapshot atual da API.

> **Validação E2E — 16/09/2026:** a primeira tentativa do cenário C1 foi
> interrompida por recompilações do servidor Next e violações CSP
> `report-only`; ela não foi contabilizada isoladamente. Depois do ajuste do
> runner oficial do Admin e dos mocks/BFF, a bateria integrada de C1/C3/C4,
> WhiteList, Emitentes, Empresas/FIDC, Consultoras e Registradoras terminou
> com **14/14 cenários aprovados**. Checks estáticos e build do Admin também
> passaram; não foi feita alteração nem validação de compilação da API nesta
> execução.

> **Execução — 16/09/2026:** Esteira de Crédito avançou com ações de fase
> (parecer, avanço, retorno e reprovação), checklists editáveis, documentos
> complementares (listar, anexar, editar, remover e download), Histórico de
> Proposta e geração da ata de comitê. Regulamento agora possui lista, detalhe,
> parâmetros preservados, critérios, documentos, histórico, status, vínculo IA
> e integração RAG no Admin/BFF, mantendo as rotas observadas no legado. A
> disponibilidade dessas rotas, PDD e efeitos reais da Esteira continuam gates
> de runtime e homologação.

> **Double check dos cadastros — 15/09/2026:** a conferência dos nove itens
> historicamente marcados como concluídos não encontrou nenhum que satisfaça
> integralmente o critério de 100% deste plano. Eles têm recortes implementados,
> mas ainda carregam, conforme o caso, mocks demonstrativos, consumidores SSR
> de sessão/claims, divergências de payload/policy upstream ou homologação
> integrada pendente. Portanto, os marcadores `✅` abaixo representam apenas
> escopo implementado e devem ser lidos junto ao [plano de conclusão do
> Admin](./plano-conclusao-cadastros-admin.md).

> **Revisão de Cadastros — 08/09/2026:** o inventário reconciliado com o código de
> `apps/admin` e a sequência de conclusão estão no
> [Plano de conclusão dos cadastros do Admin](./plano-conclusao-cadastros-admin.md).
> Para esse recorte, a revisão abaixo e o novo plano prevalecem sobre os status
> históricos deste documento. Login, permissões, sessão/refresh e 2FA atuais
> dos dois portais são base protegida; a migração adapta os consumidores.

## Revisão de Cadastros — 15/09/2026

O levantamento de escopo desta seção é estático; a execução e as validações
realizadas estão registradas nas notas de execução acima. Foram encontradas 31
declarações de rota após o redirecionamento vazio no roteador de Cadastros: 29
frentes cadastrais e os acessos FAQ/Releases.
`faixa-pdd` é uma frente real no Angular; seu contrato CRUD foi levantado das
requisições do legado e representado no Admin/BFF. O snapshot atual da API não
possui o controller/DTO correspondente, portanto a integração real continua
pendente. O plano também inclui uma trilha complementar de cadastros
administrativos, financeiros e de Setup.

| Constatação                                                                                                                                                                            | Atualização de planejamento                                                                                                                                                                  |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Nove cadastros estavam marcados como concluídos em algum recorte                                                                                                                       | “Concluído no recorte” não certifica paridade integral nem homologação atual no Admin.                                                                                                       |
| Certificadoras tem Histórico no Angular, antes ausente no Admin                                                                                                                        | Histórico/`L_CER_HIS` foi implementado no Admin; validar detalhe, filtros e autorização com usuário sem MASTER.                                                                              |
| Classificação usa editor HTML no Angular e precisava reconciliar a edição rica no Admin                                                                                                | `RichTextEditor` sanitizado passou a preservar o fluxo HTML; validar sanitização e payload integrado antes de considerar paridade.                                                           |
| Sacados já conecta CRUDs compartilhados de Pessoa/contatos e suportes                                                                                                                  | Atualizar o contrato e validar o existente; não recriar indiscriminadamente as funcionalidades listadas como ausentes no inventário antigo.                                                  |
| Registradoras já tem contrato próprio e Histórico frontend/BFF                                                                                                                         | Reutilizar `registradoras.md`; verificar a autorização upstream documentada.                                                                                                                 |
| `drawer`, `rating`, `credit-mat` e `fidc` foram contados novamente com outros nomes                                                                                                    | Consolidar respectivamente em Sacados, Classificação, Esteira de Crédito e Empresas/FIDC.                                                                                                    |
| Empresas/FIDC e Esteira possuem controllers identificados                                                                                                                              | Usar `FidcController` e `PropostaController`; reconciliar separadamente os endpoints mais recentes de Regulamento.                                                                           |
| Faixa de PDD tem rota, módulo, lista, formulário, serviço e claims no Angular; as requisições correspondentes foram representadas no Admin/BFF; FAQ e Releases são dois acessos distintos | Confirmar no runtime upstream o CRUD, DTO, claims e regras de intervalo; tratar `/pdd/list/fidc/{fidcId}` como dependência separada do Regulamento e preservar ambos os conteúdos. |
| Parte das páginas de criação administrativa ainda carrega claims por SSR                                                                                                               | Adaptar os consumidores restantes ao bootstrap client/BFF existente, preservando o mecanismo compartilhado de permissões e autenticação.                                                     |

O plano detalhado registra a evidência, os submódulos restantes, a ordem C0–C8,
as dependências, os gates de regressão dos dois portais e o critério para
“100% migrado”. Os resultados de testes citados no histórico abaixo não foram
reexecutados nesta revisão.

### Double check dos nove “concluídos” históricos

| Cadastro        | Resultado da conferência                    | Pendência que impede 100%                                                                             |
| --------------- | ------------------------------------------- | ----------------------------------------------------------------------------------------------------- |
| Cedentes        | Implementado no recorte e referência visual | Resumo/Insights agora usam o BFF e as requisições do legado; confirmar DTO real e todas as abas/ações no runtime integrado. |
| Administradoras | CRUD e abas principais implementados        | Validar payloads, multipart, filtros e ações integrados.                                              |
| Agentes         | Contrato frontend implementado              | Validar histórico com as claims `L/W/E/R_AGE_HIS`, `desagioRecebivel` e gaps documentados de backend. |
| Bancarizador    | Frontend e BFF implementados                | Observação de status pode ser recusada para não-MASTER; validar resposta parcial e policy upstream.   |
| Certificadoras  | CRUD implementado; Histórico reaberto       | Validar `L_CER_HIS`, detalhe do evento e policy upstream.                                             |
| Classificação   | Listagem e descrição rica reconciliadas     | Validar sanitização, enum, cores, filtros, remoção e payload integrado.                               |
| Custodiantes    | Contrato frontend implementado              | Homologar multipart/policies agora alinhadas entre `CUS_DOC` e `CUS_OBS` em suíte global.             |
| Gestoras        | Contrato frontend implementado              | Homologar payloads multipart, policies e suíte global; separar do módulo operacional.                 |
| Representantes  | CRUD, Pessoa e suportes implementados       | Validar payloads e multipart integrados; lista e ações agora usam bootstrap client/BFF.               |

**Resultado:** nenhum dos nove deve ser usado como substituto integral do Angular
ou como critério de corte até cumprir contrato, paridade, autorização, testes de
erro e homologação real. Os recortes já implementados continuam aproveitáveis;
o trabalho é fechar as lacunas comprovadas.

---

> Atualizado em 03/08/2026 (v5 — Gestora e Custodiante cadastrais implementados). Este documento compara os módulos funcionais em
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

### Atualização do cronograma — 03/08/2026

| Frente              | Situação atual                                         | Evidência                                                                                                                    | Próximo gate                                                    |
| ------------------- | ------------------------------------------------------ | ---------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------- |
| Gestora (cadastro)  | 🟡 Implementado no contrato; validação global pendente | Contrato, matriz campo-a-campo, formulário PF/PJ, abas, componentes compartilhados, BFFs, claims, MSW e E2E/visual dedicados | Validar payloads no ambiente integrado e fechar a suíte global  |
| Custodiante         | 🟡 Implementado no contrato; validação global pendente | Contrato, matriz campo-a-campo, formulário PF/PJ, abas, componentes compartilhados, BFFs, claims, MSW e E2E/visual dedicados | Validar payloads no ambiente integrado e fechar a suíte global  |
| Gestora operacional | ⏳ Próxima onda                                        | Permanece distinta do cadastro em `/home/gestora`                                                                            | Abrir inventário e contrato próprios antes da UI                |
| Suíte global        | 🟡 Bloqueada por falhas fora deste recorte             | E2E dedicado de Gestora/Custodiante aprovado; execução global encontrou falhas preexistentes em Banks/Cedentes               | Corrigir os bloqueadores de infraestrutura e repetir Playwright |

A migração saiu da fase de "começar do zero". Já existe uma base reaproveitável
para login, navegação, Cedentes, Operações e parte relevante dos Cadastros. O
ponto de atenção é que vários módulos aparecem na nova plataforma, mas ainda
não cobrem todo o fluxo do legado. Em outras palavras: algumas áreas já são
boas candidatas para fechamento, enquanto outras ainda precisam de descoberta
antes de entrar em desenvolvimento pesado.

Na conversa semanal, a leitura recomendada é:

| Pergunta da gerência                      | Resposta curta para a semana                                                                                                                                                         |
| ----------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Onde estamos bem?                         | Fundação da aplicação, Cedentes, Operações base, Representante e Administradora com CRUDs completos no recorte migrado, Cadastros Register e avanço visual/funcional de Sacados.     |
| O que está quase virando entrega fechada? | Cadastros Register remanescentes, Sacados, Recebíveis, Movimentação Financeira, Consultas, Relatório Financeiro e Administrativo.                                                    |
| Onde mora o maior risco?                  | Fluxos financeiros, Gestora, importações/exportações, documentos, permissões e módulos que ainda não têm contrato.                                                                   |
| O que não deve ser vendido como pronto?   | Stubs, listas isoladas sem CRUD completo, submódulos ainda pendentes de outros Cadastros (comissão, QDD e layout extrato) e módulos marcados como parcial sem validação de paridade. |
| Qual é a prioridade prática?              | Fechar o que já começou antes de abrir frentes grandes novas.                                                                                                                        |

## Leitura gerencial dos status

| Status                           | Leitura executiva                                                                       | Como comentar na reunião                                                                |
| -------------------------------- | --------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------- |
| ✅ Concluído no escopo atual     | Entrega utilizável dentro do recorte combinado.                                         | "Está pronto para o que foi contratado neste ciclo; ainda pode ter melhorias mapeadas." |
| 🟡 Parcial                       | Já existe algo concreto, mas ainda falta parte do fluxo.                                | "Tem avanço real, mas não substitui 100% o legado ainda."                               |
| ⚪ Stub / bloqueado              | A página existe mais para reservar espaço do que para operar.                           | "Aparece no menu, mas ainda depende de contrato, backend ou decisão."                   |
| 🔴 Não migrado                   | Ainda não há entrega funcional na nova plataforma.                                      | "Precisa entrar como frente futura, começando por descoberta e contrato."               |
| ↔ Consolidado / fora do cadastro | A rota foi absorvida por outro cadastro ou não é uma manutenção cadastral independente. | "Não abrir uma frente duplicada; validar no cadastro ou módulo proprietário."           |
| 🧭 Em descoberta                 | Precisa mapear legado, API, permissões e dependências antes de estimar com segurança.   | "Ainda estamos tirando a névoa do caminho; estimativa firme vem depois da descoberta."  |

## Leitura do status

| Status                           | Significado prático                                                                                                                                           |
| -------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| ✅ Concluído no escopo atual     | Existe contrato e implementação do escopo explicitamente definido. Pode ainda haver lacunas registradas no contrato.                                          |
| 🟡 Parcial                       | Há rota, BFF ou tela migrada, mas faltam fluxos, detalhe, CRUD, submódulos ou validação de paridade. Não deve ser tratado como substituto integral do legado. |
| ⚪ Stub / bloqueado              | Existe rota de placeholder, mas não há fluxo funcional; depende de controller, contrato ou decisão identificada.                                              |
| 🔴 Não migrado                   | Nenhuma implementação funcional ou contrato de migração foi localizada na base nova.                                                                          |
| ↔ Consolidado / fora do cadastro | A identidade foi reconciliada com outro cadastro ou com uma trilha não cadastral.                                                                             |

## Resultado executivo

- A migração tem fundação consistente: autenticação básica, shell, Cedentes, Operações base e **recortes de CRUD do Cadastros Register implementados** (Administradoras, Agentes, Bancarizador, Bancos, Blacklist, Certificadoras, Classificação, Consultoras, Credenciadoras, Gestoras e Custodiantes). Paridade e homologação continuam sendo gates separados.
- **Representante e Administradora** em 29/07/2026: CRUDs cadastrais e páginas de detalhe foram migrados conforme o contrato `representantes-administradoras.md`, com lookup e enriquecimento de Pessoa, PF/PJ, endereços, contatos, QSA, documentos, anexos, observações, histórico e subcadastros da Administradora. O padrão visual de cards e abas laterais foi incorporado ao design system, skills e protocolo de IA.
- **Estabilização em 03/08/2026**: enums e máscaras de Pessoa PJ, CEP com estado de consulta, complemento da Administradora, associação de representantes, tabelas canônicas, selects em modal, catálogo numérico de Tipos de Recebíveis e tradução de Histórico foram reconciliados com os contratos runtime do Angular e da API.
- **Gestora e Custodiante cadastrais em 03/08/2026**: o recorte de CRUD, PF/PJ, lookup, Pessoa, endereços, contatos, QSA, representantes, anexos, observações, histórico, filtros, ações, claims, BFFs, MSW e E2E dedicado foi implementado conforme os contratos; validação integrada/global e divergências de policy continuam pendentes.
- **Cadastros Register**: permanecem como pendências os submódulos de outros cadastros (comissão, QDD e layout extrato), filtros avançados e a homologação integrada. A importação/histórico de importação de Blacklist e o fluxo de Credenciadoras foram representados no Admin a partir das requisições do legado; o snapshot atual da API não possui todos os contratos correspondentes. A ativação de Credenciadora e a exclusão de registro de Blacklist não são comprovadas no legado/API e não foram inventadas.
- Os módulos mais próximos de completar são Cadastros Register (submódulos restantes), Recebíveis, Movimentação Financeira, Consultas, Relatório Financeiro e Administrativo; todos têm contrato e BFF, mas mantêm lacunas explicitamente documentadas.
- O maior volume ainda não iniciado está em **Gestora operacional**, Financeiro complementar, Relatórios complementares, Ativos, Debêntures, Setup e submódulos especializados de Operações.
- Regulamento deixou de ser contrato em reconciliação estática: a vertical própria do Admin/BFF cobre lista, detalhe, parâmetros preservados, critérios, documentos, histórico, ações e RAG conforme o legado. Esteira de Crédito possui uma primeira vertical funcional com fases, checklists, documentos, histórico e ata de comitê, mas ainda não conta como paridade completa. Faixa de PDD possui uma vertical Admin/BFF baseada nas requisições do legado; o snapshot atual da API não possui o CRUD correspondente. Faltam confirmação do upstream, persistência e homologação das integrações, incluindo as opções de PDD no Regulamento. Empresas/FIDC também permanece parcial.

### Atualizacao do cronograma - 13/08/2026

Agentes teve o recorte de listagem React Query/BFF, lookup PF/PJ, formulário Pessoa, comissão, suportes, claims granulares e E2E dedicado implementado. A matriz detalhada está em [agentes.md](./agentes.md). O Admin preserva `desagioRecebivel` no payload legado; a confirmação das claims `L/W/E/R_AGE_HIS` e da persistência depende do runtime, portanto o cadastro ainda não é 100% homologado.

## Inventário por domínio

### Plataforma, acesso e Home

| Módulo legado                                            | Status     | Evidência na nova plataforma                                                                           | Próximo recorte                                                                 |
| -------------------------------------------------------- | ---------- | ------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------- |
| Autenticação: login, recuperação de senha, contexto FIDC | 🟡 Parcial | Rotas `/login`, `/login/remind-password`, `/setFidcContext` e BFF de autenticação                      | Validar seleção de tipo de usuário, 2FA, ambiente bloqueado e não autorizado.   |
| Home, menu, perfil, notificações e insights              | 🟡 Parcial | Shell autenticado, menu, perfil, notificações, dashboard e endpoints `/api/home`, `/api/notifications` | Comparar cards, bankruptcy home e integrações realtime com o legado.            |
| Will                                                     | 🟡 Parcial | Componente `will-assistant` e BFF `/api/will/message`                                                  | Formalizar contrato de conversa, disponibilidade, permissões e estados de erro. |
| Insights                                                 | 🟡 Parcial | Componentes de insights e dados de Home                                                                | Mapear as telas e serviços próprios do Angular antes de ampliar o fluxo.        |

### Cadastros

| Módulo legado                       | Status                                                      | Evidência na nova plataforma                                                                                                                                                                                                                                                                                                                    | Próximo recorte                                                                                                                                                                             |
| ----------------------------------- | ----------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Cedentes                            | 🟡 Implementado no recorte; homologação pendente             | Listagem, criação, detalhe por abas e BFF extenso; o detalhe consome claims pelo bootstrap client e resumo/insights por BFF, sem mock demonstrativo visível                                                                                                                                                                                            | Fechar o contrato do DTO real e validar todas as abas/ações no ambiente integrado antes de usar como modelo de novos módulos.                                                        |
| Sacados                             | 🟡 Parcial — detalhe e Histórico em validação               | Listagem, BFFs, indicadores, ações, exportação/classificação em lote e detalhe client-side por abas; Pessoa, contatos, representantes, anexos, observações e detalhe de Histórico usam componentes/BFFs compartilhados; E2E focado adicionado                                                                                                   | Validar payloads/claims sem MASTER, campos completos, ergonomia de contatos e integração dos suportes.                                                                                      |
| Administradoras                     | 🟡 Implementado no recorte; paridade/homologação pendentes  | Lista e detalhe; lookup CNPJ com enriquecimento/reuso de Pessoa; detalhe em oito abas; dados PJ, endereços, contatos e QSA; Complemento, Representantes, Status, Tipos de Recebíveis, Anexos, Observações e Histórico; BFFs, React Query e claims pelo bootstrap client. Contrato: `representantes-administradoras.md`.                         | Validar payloads, multipart, filtros e ações no ambiente integrado.                                                                                                                         |
| Agentes                             | 🟡 Implementado no contrato; validação integrada pendente   | Lista React Query/BFF, lookup PF/PJ, formulário Pessoa, comissão, suportes, claims granulares e E2E dedicado. Contrato: `agentes.md`; o payload preserva `desagioRecebivel` conforme o legado.                                                                                    | Validar payloads no ambiente integrado; confirmar o Histórico com usuário sem MASTER e a persistência de `desagioRecebivel`.                                                                |
| Bancarizador                        | 🟡 Implementado no frontend; upstream/homologação pendentes | Lista client-side com filtros/ordenação/paginação, lookup, BFFs de CRUD/status/lote/exportação/histórico, formulário readonly e abas; claims `L_BAC/W_BAC/E_BAC/R_BAC/L_BAC_HIS`                                                                                                                                                                | Confirmar a limitação de observações de status para não-MASTER e a resposta parcial no ambiente integrado; não considerar o frontend isolado 100%.                                          |
| Bancos                              | 🟡 Parcial — CRUD, Layout e Histórico implementados         | Lista client/BFF com busca por nome/código e ordenação/paginação, BFF `/api/register/banks`, formulário, `/new` + `/[id]/edit`, activate/deactivate/delete, Layout de Extrato, Histórico com claim `L_BAN_HIS`, validação estática de payload no BFF, mock e E2E focado                                    | Validar arquivo/payload real, efeito do tipo `11`, resposta de update e filtros avançados no runtime upstream.                                                                                                  |
| Blacklist                           | 🟡 Parcial — vertical C4 implementada; homologação pendente | Lista/BFF, cadastro multipart, lookup, status/observação, exportação, detalhe, anexos associação `58`, Histórico, importação Excel assíncrona, template, histórico de importações, recusados, mocks e E2E focado; contrato: `blacklist.md`                                                                                                 | Validar payloads/claims integrados, falha parcial de lote, filtros avançados e homologação. Exclusão do registro não é comprovada no legado/API e permanece fora do escopo. |
| Certificadoras                      | 🟡 Parcial — CRUD e Histórico implementados                 | Lista, BFF `/api/register/certificadoras`, formulário, `/new` + `/[id]/edit`, activate/deactivate/delete; Histórico `L_CER_HIS` em client/BFF/UI compartilhada, detalhe, mock e E2E                                                                                                                                                             | Validar autorização sem MASTER, filtros contra API integrada e homologação.                                                                                                                 |
| Classificação                       | 🟡 Parcial — listagem client; descrição rica reconciliada   | Lista client/BFF, formulário (nome, tipo, descrição HTML, cor), `/new` + `/[id]/edit`, delete                                                                                                                                                                                                                                                   | Validar preservação do HTML e payload contra API integrada; sem ações de status no Angular.                                                                                                 |
| Consultoras                         | 🟡 Parcial — Pessoa e subcadastros implementados            | Lista, CRUD/lookup, Pessoa PJ com endereços/contatos/QSA, Complemento, QDD listagem/cadastro, Representantes, Anexos, Observações e Histórico; claims granulares, BFF, MSW e E2E focado. As ações específicas de QDD aparecem no Angular, mas seus handlers não fazem requisições; contrato: `consultoras.md`.                                                                                                                            | Filtros/exportação avançados e homologação integrada; não criar ações de QDD sem requisição/DTO de origem.                                                       |
| Credenciadoras                      | 🟡 Parcial — CRUD, filtros e Histórico representados; homologação pendente | Lista/BFF, formulário, `/new` + `/[id]/edit`, inativação, remoção, filtros nome/CNPJ/status/período, ordenação e Histórico `L_CRE_HIS`, conforme as requisições do legado; o snapshot atual da API não possui controller/DTO correspondente | Confirmar no runtime upstream o contrato, payloads e claims. Não criar migration na API; ativação não existe no legado. |
| Custodiantes                        | 🟡 Implementado no contrato; validação global pendente      | Lista, BFF `/api/register/custodiantes`, PF/PJ, Pessoa, endereços, contatos, QSA, representantes, anexos, observações, histórico, filtros, ações, claims e E2E dedicado. Contrato: `custodiante.md`; claims de Anexos e Observações estão alinhadas às policies correspondentes.                                                                | Validar payloads multipart, policies de anexos/observações e suíte global no ambiente integrado.                                                                                            |
| Emitentes                           | 🟡 Parcial — primeira fatia C4 vertical                     | Lista/BFF, cadastro e edição PF/PJ de Pessoa, lookup, detalhe, Complemento editável, Situação, Contatos, CRUD de Contas, Documentos associação `75`, Representantes, Observações, Histórico, exportação via `POST /api/emitente/get/list/export`, envio para análise Nota Comercial/QiTech, MSW e E2E focado; contrato: `emitentes.md`          | Confirmação de payloads e homologação integrada.                                                                                                                                            |
| Fornecedores                        | 🟡 Parcial — detalhe PF/PJ iniciado                         | Listagem client-side, BFF `/api/register/fornecedores`, criação/edição de Pessoa, endereço, contatos, QSA, Histórico com associação `73`, mock representativo e E2E C3                                                                                                                                                                          | Validar payloads reais, claims e completar homologação do cadastro.                                                                                                                         |
| Gestoras (cadastro)                 | 🟡 Implementado no contrato; validação global pendente      | Lista, BFF `/api/register/gestoras`, PF/PJ, Pessoa, endereços, contatos, QSA, representantes, anexos, observações, histórico, filtros, ações, claims e E2E dedicado. Contrato: `gestora.md`.                                                                                                                                                    | Validar payloads multipart e suíte global no ambiente integrado; manter separado de Gestora operacional.                                                                                    |
| Investidores                        | 🟡 Parcial — detalhe PF/PJ implementado                     | Listagem client-side, BFF `/api/register/investidores`, Pessoa PF/PJ, Complemento, Conta/Planos de Contas, Anexos, Observações, Histórico, lookup, remoção, mock e E2E C3; `ListInvestidorPolicy` alinhada a `L_INV`.                                                                                                                           | Validar payloads/claims no ambiente integrado e liberar gradualmente.                                                                                                                       |
| Originador                          | 🟡 Parcial — detalhe PF/PJ iniciado                         | Listagem client-side, BFF `/api/register/originador`, detalhe PF/PJ com Pessoa, FIDC, endereço, contatos, Observações, bloqueio e enum invertido; mock representativo e E2E C3                                                                                                                                                                  | Validar payloads, claims e homologação do cadastro.                                                                                                                                         |
| Prestadores de Serviços             | 🟡 Parcial — detalhe PF/PJ implementado                     | Listagem client-side, BFF `/api/register/prestadores`, detalhe Pessoa/Prestador, criação multipart, edição de Pessoa, remoção via POST upstream, Observações, Anexos, Histórico, lookup, mock e E2E C3                                                                                                                                          | Validar payloads/claims no ambiente integrado e liberar gradualmente.                                                                                                                       |
| Produto                             | 🟡 Parcial — vertical implementada; homologação pendente   | Lista client/BFF, CRUD, opções de bancarizador/template/conta de repasse, exportação, formulário com exclusividade Fee/Custo e preservação do payload legado (`dadosAdicionais`, fluxos e observações), filtros visuais, Histórico e mock/E2E focado; o snapshot atual da API não declara todos esses campos/rota                                                                                                                                 | Homologar payload, conta de repasse, permissões e integração no runtime upstream; sem alteração no login/permissões compartilhadas/2FA.                                      |
| Representantes (cadastro)           | 🟡 Implementado no recorte; paridade/homologação pendentes  | Lista e detalhe; lookup CPF/CNPJ; criação e edição PF/PJ; Pessoa, endereços, contatos e QSA; abas Documentos, Anexos, Observações e Histórico; catálogo normal/QI Tech, claims e E2E específicos; lista agora usa bootstrap client/BFF e as ações ativar/desativar validam `E_REP`. Contrato: `representantes-administradoras.md`.              | Validar payloads e operações multipart contra ambiente integrado.                                                                                                                           |
| Testemunhas                         | 🟡 Parcial — detalhe PF iniciado                            | Listagem client-side, BFF `/api/register/testemunhas`, detalhe PF com Pessoa, endereços, contatos, Anexos, Observações e Histórico pela associação `2`, mock representativo e E2E C3                                                                                                                                                            | Validar payloads, claims e homologação do cadastro.                                                                                                                                         |
| WhiteList                           | 🟡 Parcial — primeira fatia C4 vertical                     | Lista/BFF, cadastro e edição PF/PJ de Pessoa, lookup, detalhe, Filiais, Anexos associação `85`, Observações, Histórico, importação/template/exportação e histórico de importações, MSW e E2E focado; contrato: `whitelist.md`                                                                                                                   | Confirmar importação/exportação com payloads reais, filtros e homologação.                                                                                                                  |
| Despesas                            | 🟡 Parcial — CRUD e Histórico implementados                 | Lista client/BFF, CRUD básico, formulário com Valor dinâmico, Histórico com paginação/busca/ordenação/detalhe, correção de policy/`GetEvento`, mock e E2E focado                                                                                                                                                                                | Validar payload real, claims sem MASTER e homologação.                                                                                                                                      |
| Grupo Econômico                     | 🟡 Parcial — CRUD/lista client e Histórico implementados    | Lista client/BFF, CRUD básico, CNPJ Matriz e adicionais, limite somente leitura com rateio, aba Vinculados com vínculo automático/remoção, Histórico com associação `26`, mock/E2E focado; operações especiais seguem as requisições do legado                                                                                                                                                                                                                                                   | Confirmar no runtime upstream as rotas de rateio/vínculo e homologar limite, payloads e claims.                                                                                                                                                      |
| Registradoras                       | 🟡 Núcleo migrado                                           | Lista, criação, edição, status, remoção e Histórico via BFF (`/api/register/registradoras`), associação `68` e claim `L_REG`; o Admin aplica o gate local e consome os endpoints genéricos disponíveis                                                                                                                                                                  | Homologar payloads, Histórico e permissões no ambiente integrado; lotes/integrações operacionais ficam fora deste cadastro.                                                                 |
| Empresas (FIDC)                     | 🟡 Parcial — C5 incremental executado em 16/09/2026         | Lista, detalhe, cadastro por `PessoaId`, edição da Pessoa, status, Complemento avançado, Contas, Assinantes/Testemunhas, Certificadoras, Ambientes via contrato legado, Regulamento com campos numéricos, enums e coobrigação, configurações FIDC contratuais, suportes, BFF, MSW e E2E focado; contrato: `empresas-fidc.md`                                                   | Homologar Ambientes, validações/Insights, ações específicas, blocos ainda não expostos pelo DTO, PDD e integração real.                                                                            |
| Faixa de PDD                        | 🟡 CRUD representado no Admin; upstream pendente                 | Angular possui rota, lista, formulário, validações, paginação, service e claims `L/W/E/R_PDD`; Admin possui BFF, lista, ordenação, formulário e ações baseados nas requisições do legado. O snapshot atual da API não possui controller/DTO/migration correspondente.                                                                                                                                                           | Confirmar no runtime upstream o CRUD, DTO, claims e regras de intervalo; fechar `/pdd/list/fidc/{fidcId}` como dependência separada do Regulamento.                        |
| Regulamento                         | 🟡 Implementação Admin concluída; homologação pendente       | Vertical própria com lista, detalhe, parâmetros escalares e complexos preservados, critérios multipart, documento IA, vínculo IA, anexos, histórico, status, remoção e RAG; BFF chama as rotas do legado quando o snapshot da API não as declara. Contrato: [`regulamento.md`](./regulamento.md). | Confirmar runtime upstream, persistência, claims, anexos, RAG e `/pdd/list/fidc/{fidcId}`; homologar antes de marcar 100%. Não alterar API/legado. |
| Esteira de Crédito                  | 🟡 Parcial — primeira vertical C6                           | Lista de Propostas, cards de indicadores, filtros/exportação, paginação, detalhe, nove colapsos com edição de campos/tabelas/observações, responsável comercial, revisões, Resumo, Recuperação Judicial, Parecer Final, Relatório Final, fases, checklists, documentos complementares e obrigatórios, Histórico, ata de comitê, BFF, MSW e E2E. | Homologar responsáveis, efeitos das integrações e contratos reais de tabelas/documentos antes de concluir.                                                                                  |
| FIDC (contexto/cadastro geral)      | 🟡 Consolidado em Empresas/FIDC                             | Contexto é infraestrutura compartilhada; cadastro Admin está em `/home/empresas` com BFF e abas incrementais                                                                                                                                                                                                                                    | Fechar as lacunas do cadastro Empresas/FIDC, sem criar uma segunda seleção de contexto.                                                                                                     |
| Gavetas / Drawer                    | ↔ Consolidado em Sacados                                    | Rota Angular `register/drawers` representa o cadastro de Sacados                                                                                                                                                                                                                                                                                | Validar a paridade de Sacados; não criar CRUD duplicado de Gavetas.                                                                                                                         |
| E-mail de cadastro                  | ↔ Fora do escopo de Cadastro                                | Não há rota ativa em `register`; trata-se de template/trigger de Comunicação/Administrativo                                                                                                                                                                                                                                                     | Mapear somente na trilha de Comunicações quando houver contrato e prioridade.                                                                                                               |
| Notificações de cadastro            | ↔ Fora do escopo de Cadastro                                | Não há rota ativa em `register`; configurações de notificação do FIDC são tratadas na aba/configuração correspondente                                                                                                                                                                                                                           | Validar a configuração do FIDC e o módulo de Comunicações, sem duplicar cadastro.                                                                                                           |
| Ações de usuário                    | 🔴 Não migrado                                              | Sem rota/BFF dedicado                                                                                                                                                                                                                                                                                                                           | Inventariar logs e permissões antes de estimar.                                                                                                                                             |
| FAQ / Manual                        | 🟡 Parcial                                                  | Rota `/home/register/manual-faq` e Ajuda                                                                                                                                                                                                                                                                                                        | Verificar paridade do conteúdo, gestão e permissões do FAQ legado.                                                                                                                          |
| Releases                            | 🟡 Parcial                                                  | Angular usa `manual-release` para abrir um iframe externo próprio; Admin agora possui a rota `/home/register/manual-release` com o mesmo destino.                                                                                                                                                                                               | Validar acesso e disponibilidade do conteúdo em C7; não considerar o alias de FAQ como migração de Releases.                                                                                |
| Materiais de crédito (`credit-mat`) | ↔ Consolidado em Esteira de Crédito                         | Rota Angular é o módulo de Propostas da Esteira; Admin possui `/home/esteira-de-credito` e detalhe C6                                                                                                                                                                                                                                           | Fechar os contratos/homologação da Esteira; não criar tela duplicada.                                                                                                                       |
| Rating                              | ↔ Consolidado em Classificação                              | Rota Angular `register/rating` corresponde ao cadastro de Classificação; Admin possui `/home/classificacao`                                                                                                                                                                                                                                     | Validar HTML/payload e homologação de Classificação; não criar CRUD duplicado de Rating.                                                                                                    |

### Operações, recebíveis e ativos

| Módulo legado                                         | Status                       | Evidência na nova plataforma                              | Próximo recorte                                                                                 |
| ----------------------------------------------------- | ---------------------------- | --------------------------------------------------------- | ----------------------------------------------------------------------------------------------- |
| Operações (lista e detalhe base)                      | ✅ Concluído no escopo atual | Contrato `operacoes.md`, lista, detalhe e abas/BFF        | Implementar ações ainda stub (recusar/reabrir), totalizadores e validar todas as abas.          |
| Recebíveis                                            | 🟡 Parcial                   | Listagem, detalhe, filtros, cards e BFF recém-adicionados | Consolidar contrato, validar payload real e completar operações do legado ligadas a recebíveis. |
| Checagem                                              | 🟡 Parcial                   | Aba de Operações e endpoint de checagem                   | Migrar a tela/fluxo independente, regras de permissão e ações do legado.                        |
| Carteira FIDC                                         | 🔴 Não migrado               | Há links de navegação, sem rota funcional localizada      | Extrair contrato de `wallet-fidc` e suas dependências em Operações/Gestora.                     |
| Cobrança                                              | 🔴 Não migrado               | Sem rota/BFF dedicado                                     | Migrar após Operações e Recebíveis, reutilizando seus contratos e tipos.                        |
| Instruções                                            | 🔴 Não migrado               | Sem rota/BFF dedicado                                     | Idem Cobrança.                                                                                  |
| Ações de Série                                        | 🔴 Não migrado               | Sem rota/BFF dedicado                                     | Idem Cobrança.                                                                                  |
| Pós-fixadas                                           | 🔴 Não migrado               | Sem rota/BFF dedicado                                     | Idem Cobrança.                                                                                  |
| Recebíveis pós-fixados                                | 🔴 Não migrado               | Sem rota/BFF dedicado                                     | Idem Cobrança.                                                                                  |
| Document Servicing v1                                 | 🔴 Não migrado               | Sem rota/BFF dedicado                                     | Decisão explícita de produto necessária para não duplicar com v2.                               |
| Document Servicing v2                                 | 🔴 Não migrado               | Sem rota/BFF dedicado                                     | Decisão explícita de produto necessária para não duplicar com v1.                               |
| Monitoramento NFe / v2                                | 🔴 Não migrado               | Sem rota/BFF dedicado                                     | Fazer descoberta técnica; verificar sobreposição com Dashboard Monitoramento NFe.               |
| Simulador                                             | 🔴 Não migrado               | Sem rota/BFF dedicado                                     | Extrair contrato e confirmar backend antes de estimar.                                          |
| Ativos: Nota Comercial                                | 🔴 Não migrado               | Sem rota/BFF dedicado                                     | Extrair contrato, controller e documentos envolvidos.                                           |
| Ativos: CCBs / emissão de CCBs                        | 🔴 Não migrado               | Sem rota/BFF dedicado                                     | Extrair contrato, fluxo de emissão e assinaturas/documentos.                                    |
| Ativos: Cartão de Crédito — agenda, contrato e opt-in | 🔴 Não migrado               | Sem rota/BFF dedicado                                     | Tratar como uma frente coesa, com contrato comum e entregas por subfluxo.                       |

### Financeiro e Gestora

| Módulo legado                                   | Status            | Evidência na nova plataforma                                                                                                                  | Próximo recorte                                                                                    |
| ----------------------------------------------- | ----------------- | --------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------- |
| Movimentação Financeira                         | 🟡 Parcial        | Contrato, lista, saldo, filtros, CRUD, lote, extrato, histórico e BFF                                                                         | Confirmar endpoints de opções/status e concluir anexos, importação avançada e pendências listadas. |
| Plano de Contas                                 | 🟡 Núcleo migrado | `/home/plano-contas`, BFF CRUD/status/exportação, Histórico, claims `L/W/E/R_PLA`, `W_PLA_XLS` e aba Gerencial/Contábil com as 21 associações | Homologar integração; alimenta Centro de Custo, Contas a Pagar/Receber e Contábil.                 |
| Centro de Custo                                 | 🟡 Núcleo migrado | `/home/centro-custo`, BFF CRUD/Histórico e claims `L/W/E/R_CEN`                                                                               | Ativação/exportação não existem no controller verificado; homologar integração.                    |
| Contas a Pagar                                  | 🔴 Não migrado    | Sem rota/BFF dedicado                                                                                                                         | Migrar após Plano de Contas e Centro de Custo.                                                     |
| Contas a Receber                                | 🔴 Não migrado    | Sem rota/BFF dedicado                                                                                                                         | Migrar após Plano de Contas e Centro de Custo.                                                     |
| Fluxo de Caixa                                  | 🔴 Não migrado    | Sem rota/BFF dedicado                                                                                                                         | Depende de Contas a Pagar e Contas a Receber.                                                      |
| Movimentos Contábeis                            | 🔴 Não migrado    | Sem rota/BFF dedicado                                                                                                                         | Migrar após camada de contas e lançamentos.                                                        |
| Extrato financeiro                              | 🔴 Não migrado    | Sem rota/BFF dedicado                                                                                                                         | Depende dos contratos de contas e movimentação.                                                    |
| Fechamento de data financeira                   | 🔴 Não migrado    | Sem rota/BFF dedicado                                                                                                                         | Requer regras de fechamento e permissões específicas.                                              |
| Processo de falência                            | 🔴 Não migrado    | Sem rota/BFF dedicado                                                                                                                         | Alto risco legal; extrair contrato antes de estimar.                                               |
| Gestora — Cedentes/Assignors                    | 🔴 Não migrado    | Cedentes gerais não equivalem automaticamente ao módulo Gestora                                                                               | Mapear diferenças de claim, contexto e operações antes de reutilizar telas.                        |
| Gestora — Aquisição                             | 🔴 Não migrado    | Sem rota/BFF dedicado                                                                                                                         | Fluxo transacional de alto risco; migrar após Operações e Financeiro.                              |
| Gestora — Operação                              | 🔴 Não migrado    | Sem rota/BFF dedicado                                                                                                                         | Idem Aquisição.                                                                                    |
| Gestora — Pagamentos de Operações               | 🔴 Não migrado    | Sem rota/BFF dedicado                                                                                                                         | Idem Aquisição.                                                                                    |
| Gestora — Recompras                             | 🔴 Não migrado    | Sem rota/BFF dedicado                                                                                                                         | Idem Aquisição.                                                                                    |
| Gestora — Saldo                                 | 🔴 Não migrado    | Sem rota/BFF dedicado                                                                                                                         | Planejar após camada financeira compartilhada.                                                     |
| Gestora — Extrato Bancário                      | 🔴 Não migrado    | Sem rota/BFF dedicado                                                                                                                         | Idem Saldo.                                                                                        |
| Gestora — PL                                    | 🔴 Não migrado    | Sem rota/BFF dedicado                                                                                                                         | Idem Saldo.                                                                                        |
| Gestora — Movimentos Abertos / Baixados / Pagos | 🔴 Não migrado    | Sem rota/BFF dedicado                                                                                                                         | Idem Saldo.                                                                                        |
| Gestora — Dívida                                | 🔴 Não migrado    | Sem rota/BFF dedicado                                                                                                                         | Idem Saldo.                                                                                        |
| Gestora — Recebíveis                            | 🔴 Não migrado    | Sem rota/BFF dedicado                                                                                                                         | Requer contrato de domínio, documentos e permissões próprias.                                      |
| Gestora — Lastro                                | 🔴 Não migrado    | Sem rota/BFF dedicado                                                                                                                         | Idem Recebíveis Gestora.                                                                           |
| Gestora — Registros                             | 🔴 Não migrado    | Sem rota/BFF dedicado                                                                                                                         | Idem Recebíveis Gestora.                                                                           |
| Gestora — Garantias                             | 🔴 Não migrado    | Sem rota/BFF dedicado                                                                                                                         | Idem Recebíveis Gestora.                                                                           |
| Gestora — Prestadores de Serviços               | 🔴 Não migrado    | Sem rota/BFF dedicado                                                                                                                         | Idem Recebíveis Gestora. Verificar sobreposição com Prestadores em Cadastros.                      |
| Gestora — Blacklist                             | 🔴 Não migrado    | Blacklist de Cadastros não prova paridade Gestora                                                                                             | Confirmar se há domínio/rota distinta e evitar reaproveitamento indevido.                          |

### Relatórios, consultas, administrativo, comunicações e setup

| Módulo legado                                 | Status            | Evidência na nova plataforma                                                                                                                                                 | Próximo recorte                                                                                                       |
| --------------------------------------------- | ----------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------- |
| Consultas externas                            | 🟡 Parcial        | Contrato, lista, filtros, nova consulta, resultados e BFF                                                                                                                    | Completar detalhes por fonte, histórico QI Tech, lookup de pessoa e validar DTO de fontes.                            |
| Relatório Financeiro                          | 🟡 Parcial        | Contrato, grade, parâmetros, geração, histórico e BFF                                                                                                                        | Resolver pendências de opções, concentração, sacados e atualização do histórico.                                      |
| Relatório de Operações                        | 🔴 Não migrado    | Sem rota/BFF dedicado                                                                                                                                                        | Inventariar por família; criar plataforma comum de geração, histórico e download.                                     |
| Relatório de Cedentes                         | 🔴 Não migrado    | Sem rota/BFF dedicado                                                                                                                                                        | Idem Relatório de Operações.                                                                                          |
| Relatório Contábil                            | 🔴 Não migrado    | Sem rota/BFF dedicado                                                                                                                                                        | Idem Relatório de Operações.                                                                                          |
| Relatório de PL                               | 🔴 Não migrado    | Sem rota/BFF dedicado                                                                                                                                                        | Idem Relatório de Operações.                                                                                          |
| Relatório de Debêntures                       | 🔴 Não migrado    | Sem rota/BFF dedicado                                                                                                                                                        | Idem Relatório de Operações.                                                                                          |
| Relatório de Estoque                          | 🔴 Não migrado    | Sem rota/BFF dedicado                                                                                                                                                        | Idem Relatório de Operações.                                                                                          |
| Relatório de Carteira                         | 🔴 Não migrado    | Sem rota/BFF dedicado                                                                                                                                                        | Idem Relatório de Operações.                                                                                          |
| Meus Relatórios                               | 🔴 Não migrado    | Sem rota/BFF dedicado                                                                                                                                                        | Requer plataforma de relatórios compartilhada.                                                                        |
| Relatório Gestora                             | 🔴 Não migrado    | Sem rota/BFF dedicado                                                                                                                                                        | Migrar após Gestora operacional.                                                                                      |
| Reciprocidade Serasa                          | 🔴 Não migrado    | Sem rota/BFF dedicado                                                                                                                                                        | Extrair contrato de integração Serasa antes de estimar.                                                               |
| Importação de Carteira                        | 🔴 Não migrado    | Sem rota/BFF dedicado                                                                                                                                                        | Definir contrato de upload, validação, processamento assíncrono e histórico.                                          |
| Administrativo — Usuários                     | 🟡 Parcial        | Contrato, rotas, lista, detalhe PF/PJ com Pessoa, endereços, contatos e QSA, associações, anexos, observações, histórico e BFF                                               | Credenciais API bloqueadas por endpoints ausentes na API versionada; homologar associações, payloads e permissões.    |
| Administrativo — Grupos                       | 🟡 Parcial        | Contrato, rotas, lista, formulário, catálogo dinâmico de claims, usuários vinculados, anexos, observações, histórico e BFF                                                   | Homologar herança efetiva de claims, filtros e ações finas do legado.                                                 |
| Administrativo — Templates de e-mail          | 🟡 Parcial        | Contrato, rotas, lista, formulário, editor RichText/multipart, estados, ações, histórico e BFF                                                                               | Homologar variáveis/prévia, UX dos tipos e payloads integrados.                                                       |
| Administrativo — Emails SMTP                  | 🟡 Parcial        | Contrato, rotas, lista, formulário com senha, teste de envio, estados, anexos, observações, histórico e BFF                                                                  | Homologar preservação da senha sem reentrada e efeitos reais do teste SMTP.                                           |
| Administrativo — Pessoas                      | 🟡 Núcleo migrado | `/home/pessoas`, BFF CRUD, edição PF/PJ, endereços, contatos, QSA e Histórico `L_PES_HIS`; lista/detalhe exibem chips navegáveis para associações com ID e claim disponíveis | Homologar vínculos, rotas autorizadas e payloads no ambiente integrado; reutilizar o mapper/DTO Pessoa compartilhado. |
| Administrativo — Consultas Externas           | 🔴 Não migrado    | Sem rota/BFF dedicado                                                                                                                                                        | Migrar depois de Consultas externas.                                                                                  |
| Administrativo — Log de Integração            | 🔴 Não migrado    | Sem rota/BFF dedicado                                                                                                                                                        | Extrair contrato de auditoria e permissões antes de estimar.                                                          |
| Administrativo — Log de Implantação           | 🔴 Não migrado    | Sem rota/BFF dedicado                                                                                                                                                        | Idem Log de Integração.                                                                                               |
| Comunicações — Emails                         | 🟡 Parcial        | Notificações globais e SMTP administrativo                                                                                                                                   | Separar comunicação operacional de configuração; extrair contrato de disparo.                                         |
| Comunicações — Notificações                   | 🟡 Parcial        | Menu de notificações e endpoint `/api/notifications`                                                                                                                         | Extrair contrato de tipos de notificação e ações de leitura/marcação.                                                 |
| Comunicações — Carta de Cessão                | 🔴 Não migrado    | Sem rota/BFF dedicado                                                                                                                                                        | Extrair contrato de geração, assinatura e download antes de estimar.                                                  |
| Dashboard principal                           | 🟡 Parcial        | Home dashboard implementado                                                                                                                                                  | Validar paridade de cards e dados com o legado.                                                                       |
| Dashboard — Fundos                            | 🟡 Parcial        | Sem rota equivalente dedicada                                                                                                                                                | Definir se substitui Home ou exige rota própria.                                                                      |
| Dashboard — Resumo Operacional                | 🟡 Parcial        | Sem rota equivalente dedicada                                                                                                                                                | Idem Fundos.                                                                                                          |
| Dashboard — Resumo Diário                     | 🟡 Parcial        | Sem rota equivalente dedicada                                                                                                                                                | Idem Fundos.                                                                                                          |
| Dashboard — Black BI                          | 🔴 Não migrado    | Sem rota/BFF dedicado                                                                                                                                                        | Avaliar integração de BI antes de estimar tela.                                                                       |
| Dashboard — Monitoramento NFe                 | 🟡 Parcial        | Componente de monitoramento referenciado                                                                                                                                     | Extrair contrato de dados em tempo real.                                                                              |
| Setup — Cadastro de Fundo                   | 🟡 Implementado no Admin | Wizard de 13 etapas, BFF legado, rascunho/conclusão, anexos, termos, histórico e transições de parametrização/Go Live | Homologar upstream, claims/policies e efeitos reais; API/legado permanecem intocados. |
| Setup — Migração de Dados                   | 🔴 Não migrado    | Fluxo separado de `setup/data-migration`, sem tela/BFF dedicado no Admin                                                                                                    | Tratar em frente própria; não confundir com o cadastro assistido de fundo. |
| Debêntures — Emissão e Vendas                 | 🔴 Não migrado    | Sem rota/BFF dedicado                                                                                                                                                        | Criar descoberta específica de emissão, documentos, agenda e permissões.                                              |

## Ordem recomendada e cronograma

Premissas deste cronograma: sprints de duas semanas, uma squad com capacidade
para uma frente complexa ou duas frentes pequenas em paralelo, e validação do
backend disponível durante cada sprint. As datas devem ser recalculadas se
houver outra capacidade; a ordem e os gates são mais importantes que a duração.

| Onda                             | Momento                                                                                                                              | Foco da semana                                                                                                                                                                                                                                                                                                                                                                                                                      | Mensagem para gerência                                                                                                       | Risco principal                                                                                                                                      | Decisão ou apoio esperado                                                                                                                            | Critério de saída                                                                                                                                            |
| -------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| 0 — Governança e estabilização   | Sprints 1–2                                                                                                                          | Auditar Cedentes, Operações, Recebíveis, Cadastros parciais e remover stubs que pareçam entregas.                                                                                                                                                                                                                                                                                                                                   | "Vamos separar o que está pronto de verdade do que só aparece na navegação."                                                 | Criar expectativa errada sobre telas parciais.                                                                                                       | Validar que paridade e contrato são gates obrigatórios.                                                                                              | Matriz de paridade por tela, contratos atualizados e pendências classificadas.                                                                               |
| 0A — Fechamento de Sacados       | Em curso                                                                                                                             | Consolidar Sacados sobre a referência Cedentes e concluir CRUD/submódulos existentes no Angular.                                                                                                                                                                                                                                                                                                                                    | "Sacados já ganhou forma; agora falta fechar os fluxos que fazem o módulo ser realmente substituto do legado."               | Tratar alinhamento visual como conclusão funcional.                                                                                                  | Confirmar que E2E é acompanhamento posterior, não bloqueio deste gate funcional.                                                                     | Nenhum fluxo existente no legado classificado como `LEGADO MIGRADO`; contrato `sacados.md` com evidência Angular/API/BFF/UI.                                 |
| 1 — Fechar o núcleo em andamento | Sprints 3–5                                                                                                                          | Recebíveis, Movimentação Financeira, Consultas, Relatório Financeiro e Administrativo.                                                                                                                                                                                                                                                                                                                                              | "A melhor alavanca agora é terminar o que já começou e reduzir pontas soltas."                                               | Fluxos transacionais sem payload real validado.                                                                                                      | Disponibilidade de backend/produto para validar lacunas críticas.                                                                                    | Payload real validado, lacunas críticas resolvidas/aceitas e E2E dos fluxos transacionais.                                                                   |
| 2 — Cadastros estruturantes      | Sprints 6–8 — Representante e Administradora implementados em 29/07/2026; Gestora/Custodiante cadastrais implementados em 03/08/2026 | **Representante, Administradora, Gestora (cadastro) e Custodiante têm recortes operacionais**, incluindo componentes compartilhados de Pessoa, anexos, observações, histórico, filtros e ações. Nenhum é 100% homologado: seguem gates de SSR, payload/multipart, policy e suíte global. Restam nos demais cadastros: comissão, QDD, layout extrato, filtros avançados, exportação server-side e módulos FIDC/Empresas/Regulamento. | "Os cadastros estruturantes deste recorte estão operacionais e deixaram uma base reutilizável para os próximos formulários." | Validar integrações multipart e payloads runtime no ambiente integrado; repetir a suíte global após os bloqueadores preexistentes de Banks/Cedentes. | Priorizar a validação integrada, a adoção controlada dos componentes compartilhados e os submódulos remanescentes, sem copiar o protótipo histórico. | Contratos de Gestora/Custodiante e demais cadastros implementados no recorte; E2E dedicado aprovado; pendências globais e dos demais cadastros replanejadas. |
| 3 — Financeiro compartilhado     | Sprints 9–12                                                                                                                         | Plano de Contas, Centro de Custo, Contas a Pagar/Receber, Fluxo de Caixa e Contábil.                                                                                                                                                                                                                                                                                                                                                | "É uma onda de alto impacto: mexe com dinheiro, datas, fechamento e conciliação."                                            | Regra financeira incompleta virar retrabalho caro.                                                                                                   | Validação próxima de negócio, financeiro e backend.                                                                                                  | Contratos de fechamento, moeda, datas e permissões confirmados.                                                                                              |
| 4 — Operações especializadas     | Sprints 13–15                                                                                                                        | Carteira FIDC, Cobrança, Instruções, pós-fixados, Checagem completa e documentos/monitoramento.                                                                                                                                                                                                                                                                                                                                     | "Depois do núcleo estável, entramos nos fluxos mais específicos de operação."                                                | Duplicar fluxos v1/v2 ou migrar documentos sem decisão clara.                                                                                        | Decisão explícita para Document Servicing v1/v2 e monitoramentos.                                                                                    | Operações/Recebíveis estáveis; decisão para Document Servicing v1/v2.                                                                                        |
| 5 — Gestora                      | Sprints 16–20                                                                                                                        | Aquisição, Operação, pagamentos, recompras, saldo/extrato/PL e lastro.                                                                                                                                                                                                                                                                                                                                                              | "Gestora é uma frente grande e sensível; precisa entrar com base financeira madura."                                         | Reaproveitar telas gerais sem respeitar claims, contexto e regras próprias.                                                                          | Priorização executiva dos fluxos críticos e agenda de validação de mutações.                                                                         | Reutilização controlada da camada financeira; E2E de mutações críticas.                                                                                      |
| 6 — Relatórios e dashboards      | Sprints 21–23                                                                                                                        | Famílias de relatórios, importação de carteira e dashboards com contratos de dados comuns.                                                                                                                                                                                                                                                                                                                                          | "Com os dados transacionais mais estáveis, relatórios deixam de ser chute e viram produto confiável."                        | Criar visualizações antes de estabilizar origem, histórico e download.                                                                               | Definir famílias prioritárias e padrão comum de geração.                                                                                             | Plataforma de geração/download e decisões do design system para visualizações ausentes.                                                                      |
| 7 — Frentes especializadas       | Sprints 24–27                                                                                                                        | Ativos, Cartão, CCB, Debêntures, Setup, logs administrativos e Carta de Cessão.                                                                                                                                                                                                                                                                                                                                                     | "São frentes importantes, mas especializadas; entram melhor quando a espinha dorsal já está pronta."                         | Compliance, documentos e produto sem contrato aprovado.                                                                                              | Aprovação de contratos de produto, documentos e compliance.                                                                                          | Contratos de produto, documentos e compliance aprovados.                                                                                                     |
| 8 — Corte e desativação          | Sprints 28–30                                                                                                                        | Paridade final, migração de usuários, observabilidade, regressão e retirada gradual do Angular.                                                                                                                                                                                                                                                                                                                                     | "Aqui deixamos de conviver com dois mundos e preparamos a virada com controle."                                              | Desativar Angular com rota crítica ainda dependente do legado.                                                                                       | Aprovar plano de corte, comunicação e rollback.                                                                                                      | Nenhuma rota crítica dependente do legado; plano de rollback documentado.                                                                                    |

### Regras de priorização dentro de cada onda

1. Fechar primeiro os módulos parcialmente migrados com contrato existente: reduz risco e evita duplicar a descoberta.
2. Migrar antes os cadastros e domínios que alimentam selects e regras de outros módulos.
3. Tratar transações financeiras, permissões, documentos, exportações e importações como alto risco: exigem contrato, testes e validação de payload real antes de paridade visual fina.
4. Manter dashboards e relatórios dependentes depois que os dados transacionais e os contratos de agregação estiverem estáveis.
5. Não iniciar implementação de módulo ⚪/🔴 sem contrato em `docs/migracao/<modulo>.md`.

### Atualização da execução — Credenciadoras — 16/09/2026

A reconciliação do legado confirmou listagem, cadastro, edição, inativação,
remoção e Histórico. Esses fluxos foram representados no Admin/BFF com as
requisições observadas; a API permaneceu intacta e o snapshot atual não possui
controller/DTO correspondente. Restam confirmar o runtime integrado, payloads,
claims e policies sem `MASTER`. A ativação continua fora do escopo: não existe
no serviço Angular.

> **Execução complementar — Consultoras:** Pessoa PJ com endereços, contatos e QSA,
> Complemento, Representantes, Anexos, Observações, Histórico e QDD de
> listagem/cadastro foram implementados no Admin. As ações específicas de QDD
> sem endpoint comprovado, filtros/exportação avançados e homologação integrada
> permanecem pendentes. Consulte `consultoras.md`.

### Correção de auditoria — Credenciadoras — 16/09/2026

A evidência funcional válida para esta migração é o Angular legado e as
requisições que ele faz. O Admin possui filtros básicos e abas de Histórico,
mas a API atual não apresenta controller/DTO correspondente; nenhum código,
migration ou claim foi acrescentado a ela. Permanecem pendentes a confirmação
de erros, payloads, claims e policies no runtime integrado. A ativação permanece
fora do escopo porque não existe no serviço Angular.
### Aditivo da auditoria Empresas/FIDC - 17/09/2026

A linha de Empresas agora inclui os catalogos e acoes especificos encontrados
nas requisicoes do legado: opcoes de Parametrizacao/Plano de Contas/Templates,
Duplicar Parametrizacoes, catalogo de eventos NFe do Monitoramento,
habilitar/desabilitar servico, migracao e consulta de recebiveis, alem de
grupos/templates/e-mails e detalhes/webhooks de Notificacoes. Endpoints sem
equivalente no snapshot de `BlackArrow.PortalFidc.Api` ficam atras de BFF no
Admin e chamam o legado sem modificar nenhum dos dois projetos de referencia.
A situacao continua “Pendente” somente para homologacao upstream, permissoes
reais e confirmacao dos payloads em ambiente integrado.

### Aditivo Setup — Cadastro de Fundo — 17/09/2026

A rota legada `setup/fund-register` foi incluída no Admin como wizard de 13
etapas, com rascunho, conclusão, listas repetíveis, upload de cálculo, termos,
histórico e transições de parametrização/Go Live. O BFF também preserva a
consulta de bancos em `/banco/get/list/bancos`. Essa frente usa o legado quando
o contrato não está declarado na API versionada; API e legado não foram
modificados.


</details>
