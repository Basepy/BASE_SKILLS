# Checklist LGPD Para SaaS

Use este arquivo como referência prática para revisar ou implementar LGPD em SaaS, principalmente produtos com pagamentos, PIX, Lightning, Bitcoin, APIs financeiras, webhooks e dashboards administrativos.

## Dados que normalmente entram no escopo

- Nome, e-mail, CPF, telefone e documentos.
- IP, user agent, device, sessão, localização aproximada e última atividade.
- Carteira Bitcoin, LN address, chaves públicas, transações, cobranças, saques e comprovantes.
- Payloads de webhook, logs técnicos, eventos de segurança e metadados de integrações.
- Dados bancários, fiscais, imagens, uploads e documentos temporários.

## Política de privacidade real

Incluir:

- Quais dados coleta.
- Por que coleta.
- Base legal por finalidade.
- Tempo de retenção.
- Compartilhamentos e operadores.
- Cookies, analytics, pixels e tracking.
- Medidas de segurança.
- Como pedir exportação, correção, anonimização, exclusão e revogação de consentimento.
- Canal do encarregado/DPO.

## Bases legais comuns

| Operação | Base legal provável |
| --- | --- |
| Login e autenticação | Execução de contrato |
| Emissão de cobrança | Execução de contrato |
| Antifraude e segurança | Legítimo interesse |
| Logs de segurança | Legítimo interesse |
| Nota fiscal e obrigações fiscais | Obrigação legal |
| KYC/AML | Obrigação legal ou regulatória |
| Marketing | Consentimento |
| Cookies não essenciais | Consentimento |

Tratar a tabela como hipóteses a investigar, não atribuições automáticas. Validar finalidade e circunstâncias em `bases-legais.md`; marketing, antifraude e KYC/AML não possuem base única universal.

## Consentimento rastreável

Quando consentimento for a hipótese aplicável, registrar prova proporcional da manifestação. Justificar coleta de IP e user agent. Separar consentimento de aceite contratual e ciência de política. Campos possíveis:

- Versão do termo.
- Timestamp.
- IP.
- User ID.
- Ação realizada.
- Idioma.
- Origem.
- User agent.

Tabela sugerida:

```text
user_consents
- id
- user_id
- term_version
- accepted
- accepted_at
- ip_address
- user_agent
- language
- source
```

## Retenção e limpeza

Exemplos operacionais para avaliação, sem valor de prazo legal universal. Definir períodos conforme finalidade e obrigações aplicáveis; consultar `data-retention.md`:

| Tipo | Retenção sugerida |
| --- | --- |
| Logs de acesso | 6 meses |
| Dados financeiros/fiscais | 5 anos ou conforme obrigação aplicável |
| Sessões expiradas | 30 dias |
| Tokens revogados | 90 dias |
| Uploads temporários | 24h |

Implementar jobs de limpeza e anonimização. Não manter dados além do necessário.

## Segurança mínima

### Transporte

- HTTPS/TLS 1.2+.
- HSTS.
- Cookies `Secure`, `HttpOnly` e `SameSite`.
- CORS restritivo.

### Repouso

Criptografar ou proteger fortemente:

- CPF.
- Documentos.
- Tokens.
- API keys.
- Webhook secrets.
- Dados bancários.
- Backups.

Nunca salvar:

- Senha em texto puro.
- Seed phrase ou private key sem arquitetura de custódia que exija gestão especializada.
- Secrets no frontend.
- `.env` versionado.

### Senhas

Usar Argon2id ou bcrypt com custo adequado. Evitar SHA256 puro, MD5 e SHA1.

### API keys

Padrão recomendado:

- Mostrar a chave apenas uma vez.
- Para chaves emitidas pela aplicação, salvar hash verificável. Para credenciais de terceiros que precisam ser recuperadas, usar criptografia ou gestor de segredos.
- Permitir revogação, rotação e escopos.
- Auditar criação, uso e revogação.

## Auditoria

Registrar:

- Login e falhas de login.
- Alteração de senha.
- Criação, rotação e revogação de API key.
- Webhook recebido e validação de assinatura.
- Saque, pagamento e mudança financeira relevante.
- Mudança administrativa.
- Exportação, exclusão ou anonimização de dados.
- Alterações de permissões.

Tabela sugerida:

```text
audit_logs
- id
- actor_id
- action
- resource
- ip
- user_agent
- timestamp
- metadata
```

Redigir logs para evitar vazamento de CPF, token, secret, dados bancários ou payload completo.

## RBAC e sessões

Separar papéis:

- Admin.
- Suporte.
- Financeiro.
- Usuário comum.
- Auditor.

Boas práticas:

- Permissões granulares.
- MFA para admin.
- Sessões rastreáveis por device/IP.
- Botão "encerrar todas as sessões".
- JWT curto e refresh token com rotação.

## Webhooks

Verificar o protocolo documentado pelo provedor. Aplicar assinatura HMAC, assinatura assimétrica, mTLS ou mecanismo suportado, com proteção contra replay e processamento duplicado. Exemplos conforme o protocolo:

- HMAC quando suportado.
- Header de assinatura, por exemplo `X-Signature`.
- Timestamp, por exemplo `X-Timestamp`.
- Janela anti-replay.
- Idempotência por evento.
- Validação de origem quando aplicável.
- Retry controlado.

## Uploads

Implementar:

- Validação de MIME real.
- Limite de tamanho.
- Bloqueio de executáveis.
- Nomes UUID.
- Storage privado.
- Antivírus quando aplicável.

Nunca confiar só na extensão do arquivo.

## Ambientes e segredos

Separar:

- Dev.
- Staging.
- Produção.

Evitar:

- Base real em desenvolvimento.
- Credenciais compartilhadas.
- Secrets no GitHub.
- Secrets no frontend.

Usar mecanismos como Render Secrets, Docker secrets, Vault ou cloud secrets manager.

## Direitos do titular

Permitir:

- Exportação em JSON, CSV ou PDF.
- Exclusão de conta quando possível.
- Anonimização quando retenção legal impedir exclusão total.
- Correção de dados.
- Revogação de consentimento.
- Opt-out de tracking/marketing.

## Cookies e tracking

Se usar Meta Pixel, Google Analytics, Hotjar, fingerprinting ou similares:

- Exibir banner.
- Registrar consentimento.
- Permitir opt-out.
- Bloquear scripts não essenciais antes do consentimento.

## Backup e disaster recovery

Exigir:

- Backup automático.
- Snapshots.
- Criptografia.
- Teste de restauração.
- Redundância.
- Versionamento quando fizer sentido.

Perda de dados também pode se tornar incidente de LGPD.

## Plano de incidente

Conseguir responder:

- Quais dados foram afetados.
- Quais usuários foram afetados.
- Qual vetor causou o incidente.
- Quando começou e quando foi contido.
- Quais mitigações foram aplicadas.
- Se ANPD e titulares precisam ser comunicados.

## Documentação e prova

Manter evidências de:

- Políticas.
- Inventário de dados.
- Acessos.
- Logs.
- Revisões de permissão.
- Consentimentos.
- Backups.
- Incidentes.
- Mudanças de arquitetura.

LGPD exige conseguir provar o controle, não apenas afirmar que o sistema é seguro.

## Prioridade prática

### Nível 1: urgente

- HTTPS.
- Hash seguro de senha.
- Rate limit.
- Backup.
- RBAC.
- Auditoria.
- Autenticação de webhooks conforme o provedor.
- Gestão segura de secrets.
- Proteção de admin com MFA quando possível.

### Nível 2: estrutural

- Consentimento rastreável.
- Exportação.
- Exclusão.
- Retenção automatizada.
- Anonimização.
- Inventário de dados.

### Nível 3: maturidade

- DPA.
- Automação LGPD.
- SIEM.
- Detecção de anomalia.
- Classificação de dados.
- Revisões periódicas de acesso.

## Maiores riscos práticos

- Logs vazando CPF, token ou payload sensível.
- Backup sem criptografia.
- Admin com acesso total desnecessário.
- API sem rate limit.
- Bucket público.
- JWT eterno.
- Webhook sem autenticação adequada ao protocolo do provedor.
- Chave no frontend.
- Ausência de trilha de auditoria.
- Ausência de política de retenção.
