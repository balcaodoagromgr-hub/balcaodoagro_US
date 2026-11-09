# EP04 — Cadastro do vendedor

Etapas no stepper: **Conta** (V01–V03), **Empresa** (V04–V05), **Loja** (V06–V10), **Operação** (V11–V14), **Revisão** (V15–V16). Seções aparecem conforme modalidade, tipo de pessoa e categorias.

### EP04-01 Escolher modalidades
Como vendedor, quero escolher loja/revenda, produção rural ou ambas, para configurar só o que se aplica.
Telas: V01
**Critérios de aceite**
- Posso marcar uma ou as duas modalidades; a escolha define as etapas seguintes.
- Se já tenho conta, entro e o papel `VENDEDOR` é ativado nela.

### EP04-02 Conta e titular PF/PJ
Como vendedor, quero criar a conta e informar se vendo como pessoa física ou jurídica, para receber os requisitos corretos.
Telas: V02, V03
**Critérios de aceite**
- PF segue sem a etapa de empresa e com campos de produtor (CPF, inscrição de produtor rural quando houver).
- PJ segue para V04.
- A modalidade selecionada aparece com opção "Alterar".

### EP04-03 Empresa e representante
Como vendedor PJ, quero informar CNPJ, natureza jurídica e representante legal, para ser identificado corretamente.
Telas: V04
**Critérios de aceite**
- Natureza jurídica não é fixa em LTDA (lista de opções).
- Inscrição estadual opcional com "isento, quando aplicável".
- CNPJ inativo bloqueia o avanço com aviso.

### EP04-04 Documentos do vendedor
Como vendedor, quero enviar documentos conforme minha natureza e atividade, para ser validado.
Telas: V05
**Critérios de aceite**
- Lista dinâmica por natureza jurídica; "poderes de representação" só quando necessário.
- Contador "x de y obrigatórios"; avançar exige todos os obrigatórios ou "salvar e continuar depois".
- Não pedir documentos já coletados pelo parceiro de pagamento (configurável).

### EP04-05 Perfil público e endereços
Como vendedor, quero configurar perfil público e endereços de operação, para que compradores me identifiquem e saibam como recebo pedidos.
Telas: V06, V07
**Critérios de aceite**
- Perfil: logo, nome público, descrição, telefone e e-mail comerciais, horário; prévia abre a tela 27.
- Endereços com finalidades múltiplas: expedição, retirada, devolução; posso cadastrar vários.
- Documentos e receitas nunca aparecem no perfil.

### EP04-06 Categorias e catálogo da loja
Como lojista, quero escolher categorias e o modo de catálogo, para pedir as habilitações certas.
Telas: V08
**Critérios de aceite**
- Categorias com seleção múltipla; defensivos sinalizados como "exige habilitação".
- Modo de catálogo: manual ou ERP; ERP leva às telas I18–I23 depois do cadastro.
- Selecionar defensivos ativa V09 e V10.

### EP04-07 Habilitação de defensivos e responsável técnico
Como lojista de defensivos, quero comprovar a regularização do estabelecimento e vincular o responsável técnico, para vender onde estou habilitado.
Telas: V09, V10
**Critérios de aceite**
- Requisitos documentais variam por UF/atividade (configuração, não código fixo). O exemplo do ES não é checklist nacional.
- Vínculo: escolher agrônomo cadastrado ou convidar por e-mail; status pendente/confirmado (EP03-03).
- Sem aprovação, anúncios de defensivos ficam bloqueados (EP06).

### EP04-08 Origem rural e forma de venda
Como produtor que vende, quero declarar origem própria e/ou de terceiros e a forma padrão de venda, para criar ofertas coerentes.
Telas: V11, V12
**Critérios de aceite**
- Própria e terceiros podem coexistir (seleção múltipla).
- Propriedades vinculadas vêm do cadastro do produtor (EP02-02).
- Forma padrão: compra imediata, propostas ou ambas; unidade e peso da saca definidos por oferta.

### EP04-09 Entrega/retirada e recebimentos
Como vendedor, quero configurar logística e conta de recebimento, para operar pedidos e receber.
Telas: V13, V14
**Critérios de aceite**
- Modalidades: retirada, entrega própria (área e frete) e transportadora informada manualmente.
- Recebimentos conforme o parceiro escolhido; taxas e repasse visíveis antes de ativar vendas; conta em validação até a conferência.

### EP04-10 Revisão, envio e status
Como vendedor, quero revisar só as seções aplicáveis, enviar para análise e acompanhar pendências, para ser liberado.
Telas: V15, V16
**Critérios de aceite**
- Revisão mostra apenas seções aplicáveis com "Editar".
- Envio exige declaração de veracidade e aceite dos Termos do Vendedor; informa que envio não é aprovação.
- Status por item: em análise, aprovado, correção (com motivo e ação), recusado (com recurso), reenvio só dos itens corrigidos.

### EP04-11 Painel e primeiros passos
Como vendedor, quero um painel com tarefas e atalhos, para preparar vendas enquanto a análise termina.
Telas: V17
**Critérios de aceite**
- Indicadores: pedidos a preparar, propostas aguardando, anúncios publicados, pendências.
- Atalhos: cadastrar produto (28), criar oferta (29), conectar sistema (I18), ver status (V16).
- Rascunhos permitidos antes da liberação.
