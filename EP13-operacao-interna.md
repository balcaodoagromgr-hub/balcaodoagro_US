# EP13 — Operação interna

Acesso restrito ao papel `OPERADOR`. Mesma aplicação React, área `/backoffice`, sem app separado.

### EP13-01 Fila de pendências
Como operador, quero uma fila filtrável de cadastros, habilitações, anúncios e atendimentos, para tratar o que é mais urgente.
Telas: 48
**Critérios de aceite**
- Filtros: tipo, prioridade, responsável, prazo; contadores por tipo.
- "Assumir" atribui o item; item assumido por outra pessoa mostra aviso (sem análise dupla).
- Habilitações e atendimentos com prazo vencendo sobem para o topo.

### EP13-02 Analisar cadastros, credenciais e anúncios
Como operador, quero conferir identidade, atividade, documentos, profissional e anúncio, para aprovar, recusar ou pedir correção.
Telas: 49
**Critérios de aceite**
- Decisão por documento e decisão final; justificativa obrigatória em recusa/correção.
- Aprovação de habilitação vale para categoria, estabelecimento e localidade analisados, com validade.
- Trilha de decisão completa; usuário notificado.
- Cobre: cadastro de vendedor (EP04), credencial profissional (EP03-02), documentos rurais (EP02-03), anúncios em categorias sensíveis (EP06-03).

### EP13-03 Pedidos e ocorrências
Como operador, quero consultar pedido, pagamento e entrega e registrar decisões em casos encaminhados, para resolver problemas.
Telas: 50
**Critérios de aceite**
- Visão consolidada: pedido, situação no parceiro, entrega, histórico do caso.
- Decisões registradas com motivo; cancelamento/reembolso executado e acompanhado no parceiro.
- Proibido marcar pagamento ou estorno manualmente sem confirmação do parceiro.
- Estorno pendente/falho visível e reprocessável sem duplicar.
