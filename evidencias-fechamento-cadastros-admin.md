# Evidências do fechamento local dos cadastros do Admin

**Revisão:** 22/09/2026. O Angular é a fonte de paridade. Esta matriz registra
onde o contrato foi conferido e qual validação local sustenta o fechamento.
Disponibilidade do upstream, persistência integrada, policies implantadas e
homologação são acompanhamento externo; nenhum item abaixo declara execução em
homologação.

## Critério de evidência

Cada linha combina a origem Angular, a superfície Admin/BFF e a verificação
local. Quando não há E2E exclusivo, `build + contrato` significa typecheck,
lint, build do Admin, schema/claims no BFF e mock representativo. Isso valida o
transporte local sem inventar resposta do ambiente integrado.

| Cadastro/acesso | Contrato Angular | Admin/BFF | Evidência local |
| --- | --- | --- | --- |
| Cedentes | `modules/gestora/assignors` | `apps/admin/components/cedentes`, `app/api/cedentes` | `cedentes.spec.ts`; build + contrato |
| Administradoras | `modules/register/administrators` | `components/register/administradoras`, `app/api/register/administradoras` | `representantes-administradoras.spec.ts`; build + contrato |
| Representantes | `modules/register/representative` | `components/register/representantes`, `app/api/register/representantes` | `representantes-administradoras.spec.ts`; build + contrato |
| Gestoras | `modules/register/managers` | `components/register/gestoras`, `app/api/register/gestoras` | `custodiantes-gestoras.spec.ts`; build + contrato |
| Custodiantes | `modules/register/custodian` | `components/register/custodiantes`, `app/api/register/custodiantes` | `custodiantes-gestoras.spec.ts`; build + contrato |
| Agentes | `modules/register/agents` | `components/register/agentes`, `app/api/register/agentes` | `agentes.spec.ts` (inclui comissão); build + contrato |
| Bancarizador | `modules/register/bancarizador` | `components/register/bancarizador`, `app/api/register/bancarizador` | `bancarizador.spec.ts`; build + contrato |
| Certificadoras | `modules/register/certifiers` | `components/register/certificadoras`, `app/api/register/certificadoras` | `certificadoras.spec.ts`; build + contrato |
| Classificacao | `modules/register/rating` | `components/register/classificacoes`, `app/api/register/classificacoes` | schema HTML + contrato + build |
| Bancos | `modules/register/banks` | `components/register/banks`, `app/api/register/banks` | `banks.spec.ts`; layout/enum + build |
| Credenciadoras | `modules/register/credenciadoras` | `components/register/credenciadoras`, `app/api/register/credenciadoras` | `credenciadoras.spec.ts`; build + contrato |
| Registradoras | `modules/gestora/operation/registradoras` | `components/register/registradoras`, `app/api/register/registradoras` | `registradoras.spec.ts`; build + contrato |
| Despesas | `modules/register/expense` | `components/register/despesas`, `app/api/register/despesas` | valor/historico: contrato + build |
| Grupo Economico | `modules/register/economic-group` | `components/register/grupo-economico`, `app/api/register/grupo-economico` | rateio/vinculos: contrato + build |
| Produto | `modules/register/product` | `components/register/produto`, `app/api/register/produto` | Fee/Custo: contrato + build |
| Sacados | `modules/register/drawer` (`drawer-form`) | `components/register/sacados`, `app/api/sacados` | `sacados.spec.ts`; PF/PJ/lookup/contatos/historico + build |
| Consultoras | `modules/register/consultant` | `components/register/consultoras`, `app/api/register/consultoras` | `consultoras.spec.ts`; filtros/QDD + build |
| Fornecedores | `modules/register/suppliers` | `components/register/fornecedores`, `app/api/register/fornecedores` | `cadastros-c3.spec.ts`; PF/PJ + multipart + build |
| Testemunhas | `modules/register/witnesses` | `components/register/testemunhas`, `app/api/register/testemunhas` | `cadastros-c3.spec.ts`; PF/PJ + build |
| Originador | `modules/register/originator` | `components/register/originador`, `app/api/register/originador` | `cadastros-c3.spec.ts`; status/PF-PJ + build |
| Investidores | `modules/register/investor` | `components/register/investidores`, `app/api/register/investidores` | `cadastros-c3.spec.ts`; complemento + build |
| Prestadores de Serviços | `modules/gestora/service-providers` | `components/register/prestadores`, `app/api/register/prestadores` | `cadastros-c3.spec.ts`; multipart/verbo de remoção + build |
| WhiteList | `modules/register/white-list` | `components/register/whitelist`, `app/api/register/whitelist` | `cadastros-whitelist.spec.ts`; importação/exportação + build |
| Blacklist | `modules/gestora/blacklist` | `components/register/blacklist`, `app/api/register/blacklist` | `blacklist-import.spec.ts`; importação parcial + build |
| Emitentes | `modules/register/emitentes` | `components/register/emitentes`, `app/api/register/emitentes` | `cadastros-emitentes.spec.ts`; análise/duplo envio + build |
| Empresas/FIDC | `modules/register/fidc` | `components/register/empresas`, `app/api/register/empresas` | `cadastros-empresas.spec.ts`; campos semânticos + build |
| Regulamento | `modules/register/regulamento` | `components/register/empresas`, `app/api/register/regulamento` | `fund-register.spec.ts`; multipart/transições + build |
| Faixa de PDD | `modules/register/faixa-pdd` | `components/register/faixa-pdd`, `app/api/register/faixa-pdd` | `faixa-pdd.spec.ts`; intervalos + build |
| Cadastro de Fundo | `modules/setup/fund-register` | `components/setup/fund-register-page-client`, `app/api/setup/fund-register` | `fund-register.spec.ts`; wizard/retomada + build |
| Esteira de Crédito | `modules/register/credit-mat` | `components/register/esteira`, `app/api/register/esteira-de-credito` | contrato + mock local de consultas; build |
| Usuários | `modules/administrative/user` | `components/administrativo/usuarios`, `app/api/administrativo/usuarios` | `administrative-credentials.spec.ts`; associações + build |
| Grupos | `modules/administrative/groups` | `components/administrativo/grupos`, `app/api/administrativo/grupos` | bootstrap/BFF + build |
| Templates | `modules/administrative/template` | `components/administrativo/templates`, `app/api/administrativo/templates` | bootstrap/BFF + DOCX/HTML + build |
| SMTP | `modules/administrative/emails` | `components/administrativo/emails`, `app/api/administrativo/emails` | contrato SMTP/mock + build |
| Pessoas | `modules/administrative/person` (lookup compartilhado) | `components/administrativo/pessoas`, `app/api/administrativo/pessoas` | PF/PJ/lookup compartilhado + build |
| Plano de Contas | `modules/financial/accounts-plans` | `components/financial`, `app/api/financial/plano-contas` | contrato + build |
| Centro de Custo | `modules/financial/cost-center` | `components/financial`, `app/api/financial/centro-custo` | contrato + build |
| FAQ | `modules/register/faq` | rota `/home/register/manual-faq` | navegação local + build |
| Releases | `modules/register/faq` (`manual-release`) | rota `/home/register/manual-release` | navegação local + build |

## Comandos locais da revisão

Executados no workspace `Black101.FrontEnd`:

- `npm run typecheck -w @black101/admin`
- `npm run lint -w @black101/admin`
- `npm run build:admin`
- `npm run validate:apps`
- verificações estáticas de tipos, fronteiras, modal, superfícies e sincronismo
- E2E focados listados na tabela, sempre com mock/upstream simulado local

`npm run validate` foi iniciado, mas o gate de manifesto de deploy exige
`CLIENTS_MANIFEST_FILE` e credencial KV ausentes nesta máquina. Isso é uma
limitação da ferramenta de validação, registrada separadamente, e não uma
trava cadastral nem motivo para declarar homologação.
