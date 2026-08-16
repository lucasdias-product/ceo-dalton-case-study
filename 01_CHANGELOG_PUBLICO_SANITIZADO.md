# 2026-06-28 - Fase 36E-R1C - Cronogramas de controle manual e por orçamento

- Sistema: CEO Dalton
- Autor / Idealizador: Lucas Dias da Silveira Clemente
- Aplicacao operacional: Dalton Engenharia

## Entregas

- Criadas rotas para listar, abrir, criar manualmente e criar por orcamento os `cronogramas de controle`.
- Criadas colecoes leves em `kv` para `cronogramas_controle` e `cronogramas_controle_itens`, sem migracao destrutiva e sem banco novo pesado.
- Implementado matching seguro entre item de orcamento e escopo base por nome normalizado, grupo/categoria, unidade e sobreposicao simples de termos.
- Implementada tela `Cronogramas` no frontend com filtros, criacao manual, criacao por orcamento, abertura do cronograma e edicao de status/datas/observacao dos itens.
- Mantida separacao total entre cronograma, financeiro, compras, presencas, orcamentos e PCP atual.

## Regras preservadas

- Nenhum cronograma gera financeiro automatico.
- Nenhum cronograma cria lancamento, saida, compra, presenca ou fluxo de caixa.
- Obra continua podendo existir sem cronograma e sem PCP Executivo.
- PCP mensal atual e PCP Vendas foram preservados.

# 2026-06-28 - Fase 36E-R1B - Escopos base do PCP Executivo

- Sistema: CEO Dalton
- Autor / Idealizador: Lucas Dias da Silveira Clemente
- Aplicacao operacional: Dalton Engenharia

## Entregas

- Adicionado carregamento seguro do arquivo `imports/pcp_escopos_cronograma_base_engenheiro.json`.
- Criadas rotas somente leitura para listar e consultar escopos base do PCP Executivo com filtros por grupo, aplicabilidade, controle e busca textual.
- Criada tela frontend `PCP Executivo / Escopos Base` com busca, filtros, cards de selecao e painel de detalhes.
- Mantida separacao total entre escopos base e rotinas operacionais de financeiro, compras, presenca, orcamento e PCP atual.

## Regras preservadas

- Nenhum escopo gera financeiro automatico.
- Nenhum escopo cria custo, compra, presenca, orcamento ou lancamento de caixa.
- Obra continua podendo existir sem PCP Executivo.
- Nao houve deploy nem commit automatico.

# 2026-06-28 - Fase 36E-R1 - Cliente 360, compras e vinculos financeiros

- Sistema: CEO Dalton
- Autor / Idealizador: Lucas Dias da Silveira Clemente
- Aplicacao operacional: Dalton Engenharia

## Entregas

- Implementado painel `Cliente 360` com resumo comercial, financeiro, atendimentos agrupados por tipo, compras relacionadas e pendencias.
- Adicionado backend para `compras` como origem/agregador de custo, com calculo de `valor_pago`, `valor_em_aberto`, `status` e pagamentos vinculados por `compra_id`.
- Ampliado o financeiro para aceitar `compra_id`, `cliente_id` em saidas, `numero_cheque` e filtros por cliente.
- Enriquecida a tela de obra/atendimento com resumo comercial separado de custo interno, compras relacionadas e atalhos cruzados.
- Adicionada navegacao entre cliente, obra, financeiro, compras e orcamentos por contexto interno da interface.
- Mantido cancelamento lógico de orçamentos; validações operacionais foram realizadas sem expor dados de clientes.

## Regras preservadas

- Nao houve deploy.
- Nao houve commit automatico.
- Nao houve alteracao de autenticacao, secrets, `.env` ou credenciais.
- Nao houve exclusao fisica em massa.
- Valores devidos do cliente continuam calculados sobre comercial (`vendido/contratado - recebido`), sem misturar custo interno.
# 2026-06-28 - Fase 36E-R1D - UX Premium, documentos, campo e alertas

- Sistema: CEO Dalton
- Autor / Idealizador: Lucas Dias da Silveira Clemente
- Aplicacao operacional: Dalton Engenharia

## Entregas

- Melhorada a navegacao principal com agrupamento operacional por Comercial, Operacao, Financeiro, Administrativo e Relatorios.
- Lapidado o Cliente 360 com atalhos para cronogramas e novo orcamento, alem da separacao visual entre resumo comercial e resumo interno Dalton.
- Adicionada geracao de PDF do cronograma de controle com itens agrupados, checklist base e cuidados principais.
- Adicionada geracao de carta de campo/checklist do engenheiro em PDF, somente leitura, sem efeitos operacionais automaticos.
- Criada base leve de registros de campo em `cronogramas_controle_checklists`, com API para listar, criar e editar historico por cronograma/item.
- Ampliada a tela de cronogramas para registrar status de campo, motivo de desvio, observacao, servico executado diferente e validacao.
- Melhorada a area de orcamentos com acao para gerar cronograma por orcamento aprovado vinculado a obra/atendimento.
- Reformulada a tela de alertas para criar, editar, concluir e cancelar alertas com vinculos opcionais a cliente, obra, financeiro e cronograma.
- Ajustada exclusao de alertas para cancelamento logico, preservando registros antigos.

## Regras preservadas

- Nenhum documento, cronograma ou registro de campo gera financeiro automatico.
- Nenhum fluxo novo altera compras, presencas, orcamentos ou fluxo de caixa.
- Alertas invalidos ou antigos seguem listaveis com fallback seguro.
- Nao houve deploy nem commit automatico.

# 2026-06-28 - Fase 36E-R1E - Revisao final deploy-ready e seguranca autoral

- Sistema: CEO Dalton
- Autor / Idealizador: Lucas Dias da Silveira Clemente
- Aplicacao operacional: Dalton Engenharia

## Entregas

- Revisada a navegacao entre Cliente 360, Obras/Atendimentos, Financeiro, Compras, Orcamentos e Cronogramas.
- Adicionado atalho direto de Obra/Atendimento para Cronogramas.
- Reforcada a validacao de registros de campo para impedir item associado a cronograma incorreto.
- Adicionado fallback em PDF de cronograma e carta de campo quando nao houver itens planejados.
- Melhorado tratamento de erro no cancelamento logico de alertas pelo frontend.
- Criada documentacao interna de autoria em `docs/autoria`, com manifesto e checklist deploy-ready.

## Validacao esperada

- `python -m py_compile ceo_dalton_app/backend/app/api/v1/empresa_final.py`
- `npm.cmd run build` em `ceo_dalton_app/frontend`
- Busca textual para confirmar que o marcador privado nao foi para frontend/backend operacional.

## Regras preservadas

- Nao houve deploy.
- Nao houve commit automatico.
- Nao houve alteracao de autenticacao, secrets, `.env`, tokens ou credenciais.
- Nenhuma rota nova gera custo financeiro automatico ou altera fluxo de caixa.

# 2026-06-28 - Fase 36E-R1PCP - Motor do PCP Executivo: dias uteis, produtividade e reprogramacao

- Sistema: CEO Dalton
- Autor / Idealizador: Lucas Dias da Silveira Clemente
- Aplicacao operacional: Dalton Engenharia

## Entregas

- Evoluido o motor de cronogramas para calcular duracao por produtividade, tempo fixo, duracao minima e fallback conservador.
- Datas passaram a considerar dias uteis de segunda a sexta, com estrutura pronta para feriados futuros.
- Espera tecnica passou a deslocar o proximo item em vez de misturar a espera na duracao do item anterior.
- Dependencias recomendadas dos escopos passaram a ser respeitadas com aviso quando nao forem encontradas.
- Criada reprogramacao segura de cronograma com nova data inicial e recalc dos itens nao bloqueados.
- Itens agora podem receber quantidade, unidade, ordem executiva, bloqueio manual, recalc posterior e cancelamento logico.
- Adicionada rota para inserir item manual em cronograma existente e rota para cancelar item sem exclusao fisica.
- Tela de cronogramas passou a mostrar inicio, fim, dias uteis, produtividade base, origem do calculo e secao recolhida de calculo.

## Validacao

- `python -m py_compile ceo_dalton_app/backend/app/api/v1/empresa_final.py`
- `npm.cmd run build` em `ceo_dalton_app/frontend`

## Regras preservadas

- Nenhuma rota nova gera financeiro automatico.
- Nenhuma rota nova cria compra, saida, presenca ou lancamento financeiro.
- Nao houve deploy nem commit automatico.
# 2026-06-28 - Fase 36E-R1FINAL - Admin, UX, documentos e deploy-ready

- Sistema: CEO Dalton
- Autor / Idealizador: Lucas Dias da Silveira Clemente
- Aplicacao operacional: Dalton Engenharia

## Entregas

- Reorganizado formulario de lancamentos financeiros para fluxo rapido, com campos avancados recolhidos e status calculado visivel.
- Criada area `Admin Limpeza Segura` para verificar dependencias, arquivar/cancelar e permitir exclusao permanente somente com confirmacao forte e sem dependencias.
- Criadas rotas admin para diagnostico de dependencias, exclusao permanente controlada e arquivamento/cancelamento seguro.
- Adicionado manifest PWA basico e metatags para app instalavel, sem service worker e sem cache agressivo de API.
- Reforcada localizacao da logo Dalton para documentos PDF.
- Criados manuais e relatorios operacionais de integracao, limpeza, documentos, PWA, performance e checklist deploy-ready.
- Atualizado `.gitignore` para builds, logs, backups, node_modules e env locais.

## Regras preservadas

- Nao houve deploy.
- Nao houve commit automatico.
- Nao houve alteracao de secrets, `.env`, tokens ou credenciais.
- Nenhuma rota nova gera financeiro, compra, presenca, orcamento ou custo automatico.
- Compra continua sendo agregadora e o caixa continua usando saidas/pagamentos.
# 2026-06-28 - Fase 36E-R1G - Engenheiro, sinalizacao financeira e PWA icons

- Sistema: CEO Dalton
- Autor / Idealizador: Lucas Dias da Silveira Clemente
- Aplicacao operacional: Dalton Engenharia

## Entregas

- Criada a aba `Engenheiro` com cards operacionais, acessos rapidos e lista curta de proximas etapas por obra/cronograma.
- Liberado acesso do painel Engenheiro para `ADMIN`, `OPERACIONAL`, permissao operacional existente e cargo compativel com engenheiro.
- Melhorada a sinalizacao visual do financeiro com badges e realce por prazo: atrasado, vence hoje, proximos 7 dias, futuro, realizado e cancelado.
- Mantido o formulario de entradas/saidas rapido, com campos avancados recolhidos.
- Gerados icones PWA quadrados `192x192` e `512x512` a partir da logo Dalton e atualizado o `manifest.webmanifest`.
- Atualizado checklist deploy-ready com comandos de validacao Git (`git rev-parse`, `git diff --stat`, `git status --short`).

## Regras preservadas

- Nao houve deploy.
- Nao houve commit automatico.
- Nao houve alteracao de secrets, autenticacao ou fluxo de caixa.
- Nenhuma rota ou tela nova gera custo financeiro automatico.
# 2026-06-28 - Fase 36E-R1H - Atalho Engenheiro, usuario operacional e validacao Git

- Sistema: CEO Dalton
- Autor / Idealizador: Lucas Dias da Silveira Clemente
- Aplicacao operacional: Dalton Engenharia

## Entregas

- Cadastro de usuarios passou a aceitar `cargo` opcional, mantendo perfis existentes e sem alterar autenticacao.
- Tela `Usuarios` foi ajustada para orientar criacao de usuario `OPERACIONAL` com `cargo Engenheiro` quando necessario.
- Dashboard principal recebeu atalho visivel para o `Painel do Engenheiro`, sem remover o acesso por `Operacao > Engenheiro`.
- Painel do Engenheiro recebeu cabecalho com data atual e refinamento visual de navegacao.
- Validacao Git foi destravada com `safe.directory`, permitindo revisar `git status` e `git diff` no shell atual.

## Regras preservadas

- Nao houve deploy.
- Nao houve commit automatico.
- Nao houve alteracao de secrets, senha ou fluxo de caixa.
- Nenhum ajuste novo gera custo financeiro automatico.
# 2026-06-29 - Fase 36E-R1I - Admin banco, historico financeiro e higiene deploy

- Sistema: CEO Dalton
- Autor / Idealizador: Lucas Dias da Silveira Clemente
- Aplicacao operacional: Dalton Engenharia

## Entregas

- Criada a area `Admin Dados do Sistema` para consulta segura das principais colecoes operacionais.
- Criadas rotas admin somente leitura para listar colecoes, abrir detalhe e consultar vinculos por registro.
- Implementado `Historico Financeiro` administrativo com filtros e visualizacao de antes/depois sob demanda.
- Alteracoes relevantes do financeiro passaram a gerar auditoria em `financeiro_historico`.
- Integrada navegacao de `Admin Dados do Sistema` com `Admin Limpeza Segura`.
- Criados `MANUAL_USO_CEO_DALTON_BASE.md`, `RELATORIO_HIGIENE_DEPLOY_GIT.md` e `RELATORIO_FINAL_RELACIONAMENTOS_UX.md`.
- Endurecido `.gitignore` contra artefatos locais, bancos, logs e arquivos pesados de trabalho.

## Regras preservadas

- Nao houve deploy.
- Nao houve commit automatico.
- Nao houve alteracao destrutiva de autenticacao.
- Nenhuma rota admin nova permite escrita direta perigosa ou exclusao fora do fluxo seguro.
