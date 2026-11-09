# EP08 — Carrinho e checkout

Mesmo checkout para compra imediata e proposta aceita. Um vendedor por pedido; BRL; operação nacional.

### EP08-01 Carrinho por vendedor
Como comprador, quero revisar itens e quantidades no carrinho, para seguir para a compra.
Telas: 32
**Critérios de aceite**
- Itens de um único vendedor por pedido; itens de outros vendedores ficam em carrinhos/pedidos separados.
- Editar quantidade respeitando mínimo e disponível; remover item.
- Mudança de preço ou estoque desde a inclusão é exibida antes de continuar.
- Sem login, "continuar" leva a 24 e retorna ao carrinho.
- Pedido originado de proposta aceita pula o carrinho e preserva os termos.
**Estados:** vazio, item indisponível.

### EP08-02 Entrega ou retirada
Como comprador, quero escolher retirada ou entrega e ver custo e prazo, para saber quando e como recebo.
Telas: 33
**Critérios de aceite**
- Opções conforme o vendedor: retirada (ponto e horário) e entrega própria (endereço, contato, custo, prazo).
- Região não atendida e ausência de entrega são informadas com alternativa.

### EP08-03 Documentos da compra
Como comprador de item que exige documentação, quero anexar a receita/recomendação vinculada ao pedido, para concluir a compra de forma regular.
Telas: 34
**Critérios de aceite**
- Etapa aparece só quando algum item exige documento.
- Documento vinculado a item, comprador, local de uso e versão do pedido.
- Estados: ausente, inválido, enviado, em análise, aprovado, correção.
- **Defensivos:** pagamento/conclusão só libera após conferência pelo vendedor (EP11-02).
- Acesso restrito ao vendedor e à operação.
**Bloqueio:** regras documentais por produto/UF dependem de configuração de produto.

### EP08-04 Revisão do pedido
Como comprador, quero revisar tudo antes de me comprometer, para evitar surpresas.
Telas: 35
**Critérios de aceite**
- Mostra vendedor, itens, quantidade, unidade, frete, prazo, total, origem do preço (anúncio ou proposta aceita vN com validade) e termos.
- Revalida estoque e preço; diferenças exibidas. Preço de proposta aceita é preservado dentro da validade.
- Opção de assinatura eletrônica quando disponível/solicitada.

### EP08-05 Assinatura eletrônica
Como comprador, quero assinar a compra no prestador de assinatura, para formalizar quando solicitado.
Telas: 36
**Critérios de aceite**
- Documento e signatários revisáveis; consentimento explícito antes do envio ao prestador.
- Estados: aguardando, assinado (baixar documento e evidências), recusado, expirado, falha; nova tentativa não duplica documento.
- Alteração posterior das condições gera nova versão e nova assinatura.
**Notas técnicas:** `SignatureProvider`; webhook idempotente.

### EP08-06 Pagamento
Como comprador, quero pagar com Pix ou cartão no parceiro, para concluir o pedido.
Telas: 37
**Critérios de aceite**
- Pix com QR/código copia-e-cola e expiração; cartão em ambiente do parceiro (sem armazenar dados de cartão).
- Estados: pendente, autorizado, recusado, expirado, cancelado, autenticação adicional.
- Nova tentativa usa chave de idempotência: nunca duplica cobrança ou pedido.
**Notas técnicas:** `PaymentGateway`; status só muda por resposta/webhook do parceiro.

### EP08-07 Confirmação e resultado
Como comprador, quero saber o que aconteceu e os próximos passos, para acompanhar o pedido.
Telas: 38
**Critérios de aceite**
- Distingue "pedido recebido", "pagamento confirmado", "aguardando documento".
- Linha do tempo inicial, comprovante para baixar, link para o detalhe (40).
- Falha de confirmação é reprocessada sem nova cobrança.
