# EP10 — Negociação por propostas

Negociação estruturada (sem mensageiro completo). Aceite gera condições versionadas e leva ao checkout; aceite ≠ pagamento.

### EP10-01 Enviar proposta
Como comprador, quero propor quantidade, preço, recebimento, frete, prazo e validade, para negociar uma oferta rural.
Telas: 41
**Critérios de aceite**
- Só para ofertas que aceitam propostas; respeita mínimo e disponível do lote.
- Resumo antes de enviar; observação opcional.
- Proposta registrada como versão 1 com validade; vendedor notificado.
**Notas técnicas:** `POST /negotiations` (listingId, quantity, unitPrice, delivery, freight, desiredDate, validity).

### EP10-02 Listar negociações por papel
Como comprador ou vendedor, quero ver minhas negociações por situação, para saber onde agir.
Telas: 42
**Critérios de aceite**
- Comprador vê enviadas; vendedor vê recebidas (mesma tela, visão por papel ativo).
- Situações: aguardando, contraproposta (sua vez), aceita (com prazo para pagar), recusada, retirada, expirada.
- Expiração automática ao fim da validade.

### EP10-03 Responder: aceitar, recusar, contrapropor, retirar
Como parte da negociação, quero responder à última versão, para chegar a um acordo.
Telas: 43
**Critérios de aceite**
- Histórico de versões com autor, valores e validade.
- Ações permitidas conforme quem respondeu por último e validade.
- Aceitar uma versão válida cria pedido com termos preservados e leva a 33; impede dupla aceitação (concorrência otimista).
- Reserva de estoque por prazo explícito após o aceite; liberada se não houver pagamento no prazo.
- Lote indisponível encerra a negociação com aviso.
**Notas técnicas:** `POST /negotiations/{id}/versions`, `POST /negotiations/{id}/accept|decline|withdraw`; versão aceita imutável.
