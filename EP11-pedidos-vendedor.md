# EP11 — Pedidos do vendedor

### EP11-01 Listar pedidos recebidos
Como vendedor, quero ver pedidos por status, incluindo documentos e pagamento, para priorizar o trabalho.
Telas: 44
**Critérios de aceite**
- Abas: para preparar, aguardando documento, aguardando pagamento, enviados, concluídos, cancelados.
- Situação de pagamento sempre vinda do parceiro.
- Atalho para atendimentos abertos. Estado vazio.

### EP11-02 Conferir documentos do pedido
Como vendedor de item que exige receita, quero conferir o documento vinculado, para liberar ou pedir correção.
Telas: 45
**Critérios de aceite**
- Abrir documento (URL assinada), aprovar ou pedir correção com motivo.
- Aprovação libera pagamento/conclusão para o comprador (EP08-03).
- Decisão auditada.

### EP11-03 Preparar, enviar e concluir
Como vendedor, quero registrar nota, envio/retirada e entrega com evidência, para concluir o pedido.
Telas: 45
**Critérios de aceite**
- Só prepara pedido com pagamento confirmado.
- Anexar nota fiscal ou chave; previsão de entrega; marcar enviado/pronto para retirada.
- Confirmação de entrega com evidência (foto/assinatura do recebedor).
- Cancelamento e estorno conforme permissões e regras, executados pelo parceiro.
