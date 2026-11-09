# EP03 — Profissional (agrônomo)

Escopo do lançamento: identificação, verificação profissional e vínculo técnico. Área de atendimento, carteira de clientes e emissão de receita ficam para evolução.

### EP03-01 Dados profissionais
Como agrônomo, quero ativar o papel profissional na mesma conta, para atuar no Balcão sem repetir dados pessoais.
Telas: A01
**Critérios de aceite**
- Se já tenho conta, os dados pessoais vêm preenchidos e só completo o que falta.
- Se não tenho, crio a conta com nome, e-mail, celular, senha, CPF e aceite de termos.
- Apresentação profissional é opcional.
**Notas técnicas:** `POST /me/roles/PROFISSIONAL/activate`.

### EP03-02 Habilitação profissional
Como agrônomo, quero enviar registro e documentos para análise, para ser reconhecido como profissional habilitado.
Telas: A02
**Critérios de aceite**
- Campos: RNP, número do Crea, Crea/UF, título; anexos: carteira profissional e certidão de registro.
- Posso informar atuação em outros estados.
- Status visível: em análise, aprovado, correção solicitada, recusado (com justificativa e opção de contestar).
- Enquanto em análise, posso navegar e comprar normalmente.
**Notas técnicas:** `POST /me/professional/credentials`; análise pela operação (EP13-02).

### EP03-03 Confirmar vínculo como responsável técnico
Como agrônomo aprovado, quero confirmar ou recusar o convite de uma loja, para ser seu responsável técnico.
Telas: V10 (lado da loja), A02 (lado do profissional)
**Critérios de aceite**
- Dado um convite pendente, quando confirmo, então o vínculo fica "confirmado" para a loja e para a análise.
- Só profissional com credencial aprovada pode confirmar.
- Posso encerrar o vínculo; a loja e a operação são notificadas.
**Notas técnicas:** `POST /seller/{id}/technical-manager/invites`, `POST /professional/invites/{id}/accept|decline`.
