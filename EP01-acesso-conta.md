# EP01 — Acesso, conta e papéis

### EP01-01 Escolher como usar o Balcão
Como visitante, quero escolher entre comprar, vender ou atuar como profissional, ou só explorar, para começar pelo caminho certo.
Telas: E01
**Critérios de aceite**
- Dado que estou na entrada, quando clico em Produtor, Agrônomo ou Lojista, então vou para P01, A01 ou V01.
- Quando clico em "Explorar o catálogo sem cadastro", então vou para 25 sem login.
- O texto informa que outros papéis podem ser ativados depois, na mesma conta.

### EP01-02 Entrar
Como usuário cadastrado, quero entrar com e-mail ou celular e senha, para acessar minhas compras, vendas e dados.
Telas: 24
**Critérios de aceite**
- Dado credenciais válidas, quando entro, então volto ao ponto de origem (ex.: carrinho) com o contexto preservado.
- Dado credenciais inválidas, então vejo mensagem genérica (sem revelar se a conta existe).
- Após N tentativas falhas, o acesso é temporariamente limitado.
**Estados:** sessão expirada (carrinho e rascunhos preservados).
**Notas técnicas:** `POST /auth/login`, `POST /auth/refresh`; parâmetro `returnTo` validado contra lista de rotas internas.

### EP01-03 Recuperar acesso e verificar contato
Como usuário, quero recuperar a senha por código e verificar meu contato, para voltar a usar a conta com segurança.
Telas: 24
**Critérios de aceite**
- Quando peço recuperação, então recebo código de uso único com validade curta e posso reenviar após o intervalo.
- Dado código inválido ou expirado, então vejo a mensagem e a opção de pedir outro.
- Antes de pagar ou enviar documentos, a verificação de contato é exigida se ainda não feita.
**Notas técnicas:** `POST /auth/recovery`, `POST /auth/recovery/confirm`, `POST /contacts/verify`; códigos com hash e expiração.

### EP01-04 Minha conta e alternância de papéis
Como usuário, quero gerenciar dados, endereços, notificações e papéis, para usar a mesma conta como comprador, vendedor e profissional.
Telas: 52
**Critérios de aceite**
- Vejo cada papel com status (ativo, em análise, não ativado) e o atalho correspondente.
- Ativar um papel não recria a conta nem perde compras, ofertas ou permissões.
- Notificações de pedidos e pagamentos não podem ser desligadas; as demais sim.
- Posso alterar senha, sair, consultar termos e privacidade, solicitar meus dados e ver histórico de consentimentos.
**Notas técnicas:** `GET/PATCH /me`, `GET /me/roles`, `POST /me/roles/{role}/activate`, `GET /me/consents`, `POST /me/data-requests`.
