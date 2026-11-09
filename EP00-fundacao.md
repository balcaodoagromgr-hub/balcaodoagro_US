# EP00 — Fundação técnica

Habilita todas as jornadas. Sem tela própria.

### EP00-01 Repositório, build e CI
Como time de desenvolvimento, quero um repositório com backend e frontend que compilam e testam no CI, para entregar com segurança desde a primeira história.
**Critérios de aceite**
- Dado um push em qualquer branch, quando o CI roda, então executa build, testes unitários e lint do backend e do frontend e falha se algum quebrar.
- Dado o repositório clonado, quando sigo o README, então subo backend, frontend e PostgreSQL localmente com um comando (Docker Compose).
**Notas técnicas:** monorepo `backend/` (Spring Boot, Maven ou Gradle) e `frontend/` (React + Vite + TS); Flyway para migrações; perfis `dev`, `test`, `prod`; `CLAUDE.md` com comandos.

### EP00-02 Autenticação e autorização por papel
Como plataforma, quero autenticar usuários e autorizar ações por papel, para proteger dados e operações.
**Critérios de aceite**
- Dado um usuário sem token, quando chama uma rota protegida, então recebe 401.
- Dado um usuário com papel `COMPRADOR`, quando chama uma rota de `VENDEDOR`, então recebe 403.
- Dado um recurso de outro usuário (pedido, documento), quando tento acessar pelo ID, então recebo 404 (sem vazar existência).
**Notas técnicas:** JWT com refresh; papéis por conta (`account_roles`); verificação de dono em toda consulta por ID (prevenir IDOR); rate limit em login e recuperação.

### EP00-03 Design system React
Como desenvolvedor frontend, quero componentes base no design inicial, para montar as 58 telas com consistência.
**Critérios de aceite**
- Existem componentes: `AppHeader` (por papel), `Stepper` (etapas na lateral verde), `FormField`, `Select`, `Checkbox`, `OptionCard`, `DocumentUpload` (com estados), `StatusChip`, `DataTable`, `Timeline`, `EmptyState`, `ErrorState`, `Skeleton`, `PrimaryButton`, `SecondaryButton`.
- Tokens: Figtree; verde #0B5C3B; laranja #C25E00 (etapa atual); fundo #F4F8F5; bordas #DCE7E0.
- Cada componente tem estados de foco, desabilitado e erro, e passa em teste de acessibilidade automatizado (axe).

### EP00-04 Armazenamento seguro de documentos
Como plataforma, quero guardar documentos com acesso restrito, para cumprir necessidade e minimização de dados.
**Critérios de aceite**
- Dado um upload, quando o arquivo é PDF/JPG/PNG até o limite configurado, então é salvo em bucket privado e associado ao dono e à finalidade.
- Dado outro usuário sem permissão, quando pede o arquivo, então não obtém URL.
- URLs de download são assinadas e expiram em poucos minutos.
**Notas técnicas:** entidade `Document` (owner, purpose, status: ENVIADO/EM_ANALISE/APROVADO/CORRECAO/RECUSADO, validade, versão); antivírus/varredura assíncrona se disponível.

### EP00-05 Auditoria e notificações essenciais
Como operação, quero trilha de auditoria e notificações, para rastrear decisões e avisar usuários.
**Critérios de aceite**
- Toda mudança de status de cadastro, documento, anúncio, pedido, pagamento e atendimento gera evento auditável (quem, quando, antes/depois, justificativa).
- E-mails transacionais: código de verificação, cadastro analisado, proposta recebida/respondida, pedido e pagamento, atendimento.
**Notas técnicas:** porta `Notifier` com fake em dev; outbox para não perder eventos.

### EP00-06 Portas de integração com fakes
Como time, quero adaptadores fake para pagamento, assinatura e ERP, para desenvolver as jornadas antes dos contratos.
**Critérios de aceite**
- `PaymentGateway`, `SignatureProvider`, `ErpConnector` têm implementação fake configurável para simular sucesso, recusa, pendência, expiração e falha.
- Webhooks fake disparam os mesmos eventos que os reais (idempotência por `eventId`).
