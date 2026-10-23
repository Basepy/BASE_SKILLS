---
name: lgpd-saas
description: "LGPD, privacidade, segurança e governança para projetos SaaS, APIs financeiras, pagamentos, PIX, Lightning, Bitcoin, webhooks, dashboards administrativos e produtos que tratam dados pessoais no Brasil. Use quando Codex precisar revisar, planejar ou implementar requisitos de LGPD em arquitetura, backend, frontend, banco de dados, logs, consentimento, retenção, exclusão/exportação de dados, RBAC, auditoria, criptografia, gestão de segredos, uploads, cookies, incidentes, políticas internas ou documentação de compliance."
---

# LGPD SaaS

## Princípio central

Tratar LGPD como arquitetura, segurança operacional e capacidade de prova. Não limitar a resposta a uma política de privacidade genérica: mapear dados, bases legais, controles técnicos, retenção, auditoria, direitos do titular e evidências.

Esta skill não substitui revisão jurídica. Sinalizar quando um texto, contrato, DPA, base legal sensível ou incidente real precisar de advogado/encarregado.

## Fluxo de trabalho

1. Identificar o produto, os fluxos de dados e os papéis envolvidos: controlador, operador, usuário comum, admin, suporte, financeiro, auditor e integrações externas.
2. Mapear dados pessoais e sensíveis por operação: origem, finalidade, base legal, armazenamento, acesso, compartilhamento, retenção e descarte.
3. Revisar controles técnicos: autenticação, RBAC, criptografia, senha, API keys, webhooks, uploads, logs, backups, ambientes, segredos, rate limiting e headers.
4. Revisar direitos do titular: exportação, exclusão, anonimização, opt-out, encerramento de sessões e canal de privacidade.
5. Revisar evidências: consentimentos versionados, audit logs, políticas, inventário de dados, backups testados, revisões de acesso e plano de incidente.
6. Apresentar achados com evidências e planejar correções por risco, considerando impacto, exposição e explorabilidade.
7. Implementar mudanças dentro do escopo autorizado, executar testes proporcionais e revisar regressões. Em pedidos apenas de auditoria, entregar o diagnóstico sem alterar o projeto.
8. Concluir com arquivos alterados, verificações executadas, limitações, riscos residuais e decisões pendentes. Não declarar conformidade integral com a LGPD apenas por testes técnicos aprovados.

## Ao Trabalhar Em Código

- Proteger tanto frontend quanto backend. Não aceitar apenas esconder página ou botão.
- Evitar salvar segredo, token, API key, seed phrase, private key, senha pura, payload sensível de webhook ou documento sem necessidade.
- Para API keys emitidas pela aplicação, preferir mostrar uma única vez e salvar hash verificável. Para credenciais de terceiros que precisem ser recuperadas, usar armazenamento criptografado ou gestor de segredos.
- Para senhas, usar Argon2id ou bcrypt com custo adequado; nunca SHA256/MD5/SHA1 puro.
- Para webhooks, verificar o mecanismo documentado pelo provedor, como assinatura HMAC, assinatura assimétrica ou mTLS; aplicar proteção contra replay, idempotência e retry controlado conforme o protocolo.
- Para admins, preferir permissões granulares a `if user.admin` espalhado.
- Para logs, registrar eventos de segurança sem vazar CPF, token, secrets, payloads completos ou dados bancários.
- Para uploads, validar MIME real, tamanho, antivírus quando aplicável, storage privado, nomes UUID e bloqueio de executáveis.
- Para dados temporários, sessões, tokens revogados e uploads, criar limpeza automatizada.

## Entregáveis Úteis

Escolher o artefato conforme a solicitação:

- Revisão de risco LGPD com achados por severidade.
- Checklist de implementação por nível: urgente, intermediário, avançado.
- Matriz de dados: dado, finalidade, base legal, onde entra, onde salva, quem acessa, retenção, exclusão.
- Modelo de tabelas: `user_consents`, `audit_logs`, `data_export_requests`, `deletion_requests`, `api_keys`, `security_events`.
- Plano de implementação técnico com endpoints, migrations, jobs e telas.
- Minutas técnicas para política de privacidade, cookies, retenção, acesso, backup e incidente, sempre marcadas como rascunho para revisão jurídica.

## Referência

Para checklists detalhados, bases legais, campos de tabelas e prioridades, ler `references/lgpd-saas-checklist.md` quando a tarefa envolver revisão profunda, implementação concreta ou criação de documentação.

Carregar somente as referências relevantes ao trabalho:

| Tema | Referência |
| --- | --- |
| Privacy by Design, classificação, bases legais, titulares e terceiros | [bases-legais.md](references/bases-legais.md) |
| Multi-tenant, IDOR/BOLA, dependências e testes | [security-controls.md](references/security-controls.md) |
| Pagamentos, saques, Pix, Bitcoin e Lightning | [financial-security.md](references/financial-security.md) |
| Retenção, backups e descarte | [data-retention.md](references/data-retention.md) |
| Investigação e resposta a incidentes | [incident-response.md](references/incident-response.md) |
| Modelos, agentes, MCP e prompt injection | [ai-data-protection.md](references/ai-data-protection.md) |
| Evidências e relatório de auditoria | [audit-report-template.md](references/audit-report-template.md) |

## Governança de mudanças

Investigar arquitetura e fluxo afetado antes de editar. Priorizar mudanças pequenas, reversíveis e testáveis. Respeitar autorizações já dadas; pedir aprovação adicional apenas quando a ação crítica exceder o escopo autorizado, como exclusão em massa, migração irreversível, alteração de permissões de produção ou operação financeira real. Correções locais autorizadas de autenticação e autorização podem prosseguir com testes proporcionais.

Preservar dados e alterações existentes. Não acessar dados reais ou modificar segredos de produção sem necessidade e autorização. Não executar testes intrusivos em serviços externos ou produção sem autorização específica.

## Fontes técnicas e regulatórias

- [ANPD](https://www.gov.br/anpd/pt-br): consultar regulamentações, orientações e procedimentos atuais quando houver questão regulatória.
- [OWASP ASVS](https://asvs.owasp.org/): apoiar requisitos verificáveis de segurança.
- [OWASP API Security Top 10](https://owasp.org/API-Security/): apoiar análise de riscos de APIs.
- [OWASP Cheat Sheet Series](https://cheatsheetseries.owasp.org/): consultar orientações de implementação.
- [NIST SP 800-63](https://pages.nist.gov/800-63-4/): apoiar decisões de identidade digital e autenticação.

Distinguir obrigações legais verificadas de boas práticas e compromissos contratuais. Registrar edição e requisito consultados quando relevantes. Não apresentar OWASP ou NIST como obrigação legal universal.

## Consulta à legislação brasileira

Consultar o [repositório ctresb/leis](https://github.com/ctresb/leis) para localizar legislação brasileira em Markdown, incluindo a Constituição e normas federais, estaduais, distritais e municipais. Usar o acervo para apoiar pesquisas sobre LGPD e normas relacionadas ao projeto. Consultar [PROGRESSO.md](https://github.com/ctresb/leis/blob/main/PROGRESSO.md) para verificar a cobertura atual e as lacunas; não presumir que todo o ordenamento já esteja disponível nem fixar contagens na skill.

Ao fundamentar uma decisão, conferir o texto na fonte oficial indicada no cabeçalho da norma e verificar vigência, alterações, revogações e âmbito de aplicação. Os arquivos são conversões informativas, inclusive por OCR, e podem conter erros. Citar a norma e o dispositivo aplicável com o link oficial e registrar a data da consulta. Usar o histórico do Git como recurso de navegação do acervo, sem tratá-lo como prova de autenticidade, assinatura oficial ou vigência jurídica.
