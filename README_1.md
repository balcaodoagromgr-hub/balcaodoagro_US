# Balcão do Agro — Histórias de usuário do MVP

Especificação para implementação com **Java + Spring Boot (backend)** e **React (frontend)**, usando o **Claude Code** como agente de implementação.

- Fonte de verdade de produto: `balcao-do-agro-escopo-mvp.md` (escopo fechado de 28/10/2026).
- Fonte de verdade de interface: protótipo "Balcão do Agro — Protótipo MVP" no canvas (58 telas-base + roteiros). Cada história cita o ID da tela (ex.: `T33`, `V05`).
- Dados entre colchetes no protótipo (`[Café arábica]`, `R$ [0,00]`) são exemplos, não regras.

## Índice de épicos

| Épico | Arquivo | Telas |
|---|---|---|
| EP00 Fundação técnica | `EP00-fundacao.md` | — |
| EP01 Acesso, conta e papéis | `EP01-acesso-conta.md` | E01, 24, 52 |
| EP02 Cadastro do comprador/produtor | `EP02-produtor.md` | P01, P02, P03 |
| EP03 Profissional (agrônomo) | `EP03-agronomo.md` | A01, A02, V10 (vínculo) |
| EP04 Cadastro do vendedor | `EP04-vendedor-cadastro.md` | V01–V17 |
| EP05 Catálogo e descoberta | `EP05-catalogo.md` | 25, 26, 27 |
| EP06 Publicação de anúncios | `EP06-anuncios.md` | 28–31 |
| EP07 Integração ERP | `EP07-integracao-erp.md` | I18–I23 |
| EP08 Carrinho e checkout | `EP08-checkout.md` | 32–38 |
| EP09 Pós-venda do comprador | `EP09-pos-venda.md` | 39, 40 |
| EP10 Negociação por propostas | `EP10-negociacao.md` | 41–43 |
| EP11 Pedidos do vendedor | `EP11-pedidos-vendedor.md` | 44, 45 |
| EP12 Atendimento | `EP12-atendimento.md` | 46, 47 |
| EP13 Operação interna | `EP13-operacao-interna.md` | 48–50 |
| EP14 Recebimentos do vendedor | `EP14-recebimentos.md` | 51 |

## Ordem sugerida de implementação (fatias verticais)

1. EP00 → EP01 → EP05 (catálogo navegável com dados de seed).
2. EP04 (núcleo: V01–V07, V15–V17) → EP06 (cadastro manual) → EP13.49 (aprovação) — vendedor consegue publicar.
3. EP08 + EP09 com Pix no sandbox do parceiro — **jornada 1 (compra imediata) fechada**.
4. EP10 reaproveitando o checkout — **jornada 2 (negociação) fechada**.
5. EP11, EP12, EP13, EP14 — operação do piloto.
6. EP02 (P02/P03), EP03, EP04 condicionais (V08–V14), EP07 — habilitações e integração.

## Convenções

**Formato de cada história**

```
### EPxx-NN Título
Como <papel>, quero <ação>, para <benefício>.
Telas: <IDs do protótipo>
Critérios de aceite (Dado/Quando/Então)
Estados obrigatórios
Notas técnicas (API, dados, regras)
Dependências
```

**Papéis:** `VISITANTE`, `COMPRADOR`, `VENDEDOR`, `PROFISSIONAL`, `OPERADOR` (interno). Uma conta pode ter vários papéis ativos.

**Definition of Ready**
- Tela do protótipo referenciada e critérios de aceite testáveis.
- Dependências externas (parceiro de pagamento, assinatura, ERP) com sandbox disponível ou marcadas como mock.

**Definition of Done**
- Testes: unitários (JUnit 5 / Vitest), integração da API (Spring Boot Test + Testcontainers PostgreSQL) e e2e do fluxo feliz (Playwright) quando a história fecha uma jornada.
- Estados de carregamento, vazio, erro e confirmação implementados.
- Acessibilidade: rótulos, foco visível, navegação por teclado, contraste AA.
- Responsivo: 1920, 1366 e 390 px.
- Logs e auditoria nas decisões sensíveis (documentos, pagamentos, aprovações).
- Code review aprovado; nenhuma credencial no repositório.

## Arquitetura de referência (proposta — validar com o time)

- **Backend:** Java 21 + Spring Boot 3.x, Spring Web, Spring Security (OAuth2 Resource Server/JWT), Spring Data JPA, Flyway, PostgreSQL. Monólito modular por domínio: `identity`, `seller`, `professional`, `catalog`, `listing`, `cart`, `order`, `payment`, `signature`, `negotiation`, `support`, `backoffice`, `integration`, `payout`, `document`.
- **Arquivos:** armazenamento de objetos compatível com S3 (documentos privados com URL assinada de curta duração).
- **Frontend:** React + TypeScript (Vite), React Router, TanStack Query, React Hook Form + Zod, CSS com tokens do design inicial (Figtree, verde #0B5C3B, laranja #C25E00 para etapa atual).
- **Integrações por porta/adaptador:** `PaymentGateway`, `SignatureProvider`, `ErpConnector`, `DocumentStorage`, `Notifier`. Cada uma com implementação fake para dev/test.
- Versões exatas e bibliotecas devem ser confirmadas na documentação atual antes de iniciar.

## Como usar com o Claude Code

1. Coloque esta pasta em `docs/historias/` no repositório e o escopo em `docs/escopo-mvp.md`.
2. Crie um `CLAUDE.md` na raiz com: stack, comandos de build/teste, convenções de pacote e a regra "implementar uma história por vez, com testes, citando o ID".
3. Peça por história: _"Implemente EP08-03 conforme docs/historias/EP08-checkout.md. Primeiro proponha o plano e os testes."_
4. Revise o plano antes do código; rode os testes; só então siga para a próxima.
5. Integrações externas começam pelos adaptadores fake; troque pelo real quando o contrato do parceiro estiver definido.

## Pendências de produto que bloqueiam histórias específicas

- Documento "INCRA" (EP02-03): definir qual documento concreto é.
- Parceiro de pagamento, prestador de assinatura e conector ERP do piloto (EP08, EP07, EP14).
- Regras documentais por produto/UF (EP04-09, EP08-03).
- Prazos de reserva de estoque, validade de propostas, cancelamento, devolução e estorno (EP08, EP10, EP12).
