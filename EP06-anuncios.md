# EP06 — Publicação de anúncios

### EP06-01 Cadastrar produto da loja
Como lojista, quero cadastrar um produto com categoria, unidade, imagens e atributos, para vendê-lo por compra imediata.
Telas: 28
**Critérios de aceite**
- Campos: categoria, SKU, título, unidade, condição (novo/usado nas categorias permitidas), descrição, até N imagens, atributos condicionais (registro, exige receita).
- Posso salvar rascunho a qualquer momento.
- Item integrado ao ERP mostra preço/estoque bloqueados com a origem.

### EP06-02 Criar oferta rural
Como produtor vendedor, quero criar uma oferta de lote com origem, classificação e quantidade, para vender minha produção.
Telas: 29
**Critérios de aceite**
- Origem própria ou de terceiros por lote; propriedade ou fornecedor obrigatórios.
- Identificação do lote, produto, classificação, unidade, peso da saca, quantidade, disponibilidade, fotos e comprovantes.

### EP06-03 Condições, revisão e publicação
Como vendedor, quero definir preço e condições e revisar antes de publicar, para evitar erros.
Telas: 30
**Critérios de aceite**
- Forma: preço fixo, somente propostas ou ambos; preço por unidade, mínimo, recebimento, validade, documentos exigidos do comprador.
- Resumo legível e prévia (26).
- "Publicar" só disponível com cadastro aprovado e categoria habilitada; caso contrário, envia para análise ou salva rascunho.
- Categorias sensíveis passam pela operação (EP13-02).

### EP06-04 Gerenciar meus anúncios
Como vendedor, quero ver e gerenciar anúncios por status, para manter o catálogo correto.
Telas: 31
**Critérios de aceite**
- Status: rascunho, em análise, publicado, pausado, esgotado, bloqueado (com motivo).
- Ações: ver, editar, pausar, reativar, completar rascunho.
- Editar preço/estoque de anúncio publicado não altera propostas aceitas nem pedidos confirmados.
**Estados:** nenhum anúncio.
