# EP07 — Integração ERP

Um conector homologado no piloto (a definir; Bling é só exemplo visual). Demais sistemas aparecem como "previsto", sem botão de conexão.

### EP07-01 Selecionar sistema
Como lojista, quero ver o conector disponível e registrar interesse nos previstos, para saber o que posso conectar.
Telas: I18
**Critérios de aceite**
- Só o conector liberado é selecionável; previstos têm "Tenho interesse" (registra lead).
- "Configurar depois" volta ao painel.

### EP07-02 Autorizar conexão
Como lojista, quero autorizar a integração no meu sistema, para que o Balcão leia produtos, estoque e preços e envie pedidos.
Telas: I19
**Critérios de aceite**
- Redireciono ao sistema (OAuth ou equivalente do conector) e volto com o resultado.
- Nunca digito a senha do sistema no Balcão.
- Estados: autorização recusada, retorno com erro, revogação.
**Notas técnicas:** tokens do conector cifrados em repouso; `ErpConnector.authorize/callback/revoke`.

### EP07-03 Estoque, preços e margem por unidade
Como lojista, quero escolher depósito, tabela de preço e margem de segurança por unidade, para não vender o que já saiu no balcão físico.
Telas: I20
**Critérios de aceite**
- Margem configurada por unidade (un, litro, saca…), nunca uma quantidade global aplicada a unidades diferentes.
- Frequência de atualização configurável.
- Atualizações do ERP não alteram preço de proposta aceita nem pedido confirmado.
- Estoque reservado no pedido; liberado no cancelamento.

### EP07-04 Selecionar e vincular produtos
Como lojista, quero escolher itens e vinculá-los a anúncios, para evitar duplicidade.
Telas: I21
**Critérios de aceite**
- Filtros: todos, sem vínculo, já vinculados; conferência de código, unidade e variação.
- Item sem anúncio entra como rascunho; item vinculado atualiza anúncio existente.

### EP07-05 Revisar e iniciar sincronização
Como lojista, quero ver o impacto antes de sincronizar, para não alterar anúncios por engano.
Telas: I22
**Critérios de aceite**
- Mostra valores e saldos reais consultados no momento e o impacto em anúncios existentes.
- Exige confirmação explícita; nova tentativa não duplica itens.

### EP07-06 Acompanhar integração
Como lojista, quero acompanhar resultados por item e o histórico, para corrigir pendências.
Telas: I23
**Critérios de aceite**
- Resultado por item: concluído, ajuste necessário (motivo), reprocessar item.
- Estados: sistema indisponível (não publica dado antigo), autorização expirada, pausada.
- Histórico de sincronizações na mesma área.
- Loja só vende itens integrados após validação de conexão, vínculos e saldos.
