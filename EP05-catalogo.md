# EP05 — Catálogo e descoberta

### EP05-01 Navegar e buscar no catálogo
Como visitante ou comprador, quero buscar e filtrar produtos e ofertas sem cadastro, para encontrar o que preciso.
Telas: 25
**Critérios de aceite**
- Busca por texto; filtros: categoria, modalidade, forma de compra, UF/município, recebimento; ordenação por relevância e menor preço por unidade.
- Cada cartão mostra preço **com unidade** (unidade, saco 50 kg, litro, saca de N kg).
- Itens que exigem receita mostram o aviso no cartão.
- Só aparecem anúncios publicados de vendedores e categorias habilitados na localidade.
**Estados:** sem resultado, carregando (esqueleto), falha com "tentar novamente".
**Notas técnicas:** `GET /catalog/search?q=&category=&modality=&mode=&uf=&city=&delivery=&sort=&page=`; índice textual no PostgreSQL no MVP.

### EP05-02 Ver detalhe do produto ou oferta
Como comprador, quero ver fotos, características, condições e restrições, para decidir comprar ou propor.
Telas: 26
**Critérios de aceite**
- Exibe vendedor (link para 27), disponibilidade, unidade, preço, pedido mínimo, recebimento, validade e documentos exigidos.
- Botões conforme modalidade: "Comprar agora", "Fazer proposta" ou ambos.
- Variantes: esgotado/pausado (botões desativados), categoria indisponível na localidade (venda bloqueada), lote rural.
- Quantidade respeita mínimo e disponível.
- A mesma tela serve de prévia do anúncio para o vendedor (sem botões de compra).

### EP05-03 Ver loja/perfil público
Como comprador, quero ver identificação, contatos e itens de um vendedor, para confiar e comprar.
Telas: 27
**Critérios de aceite**
- Identificação (nome/razão social, CPF/CNPJ conforme política), município, contatos comerciais, como atende, políticas de troca.
- Abas: todos, produtos da loja, ofertas rurais; busca interna; estado sem itens.
- Sem avaliações ou selos no lançamento; nenhum documento pessoal exibido.
