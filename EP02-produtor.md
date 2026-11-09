# EP02 — Cadastro do comprador/produtor

Regra central: **comprar não exige o cadastro rural completo**. Propriedade e documentos são condicionais.

### EP02-01 Criar conta de comprador
Como produtor, quero criar minha conta só com dados pessoais, para começar a comprar rapidamente.
Telas: P01
**Critérios de aceite**
- Campos obrigatórios: nome, CPF, celular, e-mail, senha, município/UF de entrega principal e aceite de termos.
- Dado CPF já cadastrado, então sou orientado a entrar ou recuperar o acesso.
- Ao concluir, vou ao catálogo (25) com o papel `COMPRADOR` ativo.
- Erros aparecem junto ao campo, com o formato esperado.
**Notas técnicas:** `POST /accounts` (papel inicial COMPRADOR); validação de CPF; senha com política mínima; registro de consentimento.

### EP02-02 Cadastrar propriedade (condicional)
Como produtor, quero cadastrar minha propriedade quando precisar, para vender produção ou informar o local de uso de uma compra.
Telas: P02 (também acionada por V11 e T34)
**Critérios de aceite**
- Campos: nome, UF, município, localidade, CEP opcional, área (ha) e vínculo (proprietário, arrendatário, parceiro, outro).
- Posso pular a etapa ("Fazer depois") sem perder o acesso ao catálogo.
- Propriedade já cadastrada aparece para seleção em vez de duplicar.
**Notas técnicas:** `POST /me/properties`, `GET /me/properties`.

### EP02-03 Documentos rurais (condicional)
Como produtor, quero anexar documentos da propriedade quando a atividade exigir, para ser habilitado sem bloquear compras comuns.
Telas: P03
**Critérios de aceite**
- Itens: CCIR, ITR, documento "INCRA" (em definição), matrícula ou outro comprovante de vínculo, georreferenciamento — cada um marcado como obrigatório só quando a regra da atividade exigir.
- Estados por documento: enviado, em análise, aprovado, correção solicitada (com motivo), recusado.
- Documentos nunca aparecem em perfil público.
**Bloqueio:** a validação obrigatória do campo "INCRA" depende da definição de produto.
**Notas técnicas:** reutiliza EP00-04 com `purpose=RURAL_PROPERTY`; regras configuráveis por atividade.
