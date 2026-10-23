# BASE_SKILLS

Skills reutilizaveis para agentes de IA. Atualmente, este repositorio publica a **lgpd-saas**, dedicada a privacidade, protecao de dados e seguranca de projetos SaaS.

Cada skill possui sua propria pasta com `SKILL.md` no primeiro nivel. Manter junto os arquivos auxiliares, referencias, scripts e assets usados pela skill.

## LGPD SaaS

A [lgpd-saas](lgpd-saas/SKILL.md) orienta analise de arquitetura, investigacao de codigo, identificacao de riscos, implementacao de controles e documentacao de evidencias. Apoia APIs, sistemas multiusuario, plataformas multi-tenant e aplicacoes financeiras com Pix, Bitcoin e Lightning.

| Modulo | Conteudo |
| --- | --- |
| [Checklist LGPD](lgpd-saas/references/lgpd-saas-checklist.md) | Politicas, consentimento, acesso, logs e seguranca |
| [Bases legais](lgpd-saas/references/bases-legais.md) | Privacy by Design, minimizacao, titulares, terceiros e transferencias internacionais |
| [Controles de seguranca](lgpd-saas/references/security-controls.md) | Multi-tenant, IDOR/BOLA, dependencias e testes |
| [Seguranca financeira](lgpd-saas/references/financial-security.md) | Pagamentos, autorizacao, idempotencia e concorrencia |
| [Retencao](lgpd-saas/references/data-retention.md) | Ciclo de vida, backups e descarte |
| [Incidentes](lgpd-saas/references/incident-response.md) | Contencao, investigacao, recuperacao e comunicacao |
| [IA e agentes](lgpd-saas/references/ai-data-protection.md) | Modelos, MCP, isolamento e prompt injection |
| [Relatorio de auditoria](lgpd-saas/references/audit-report-template.md) | Evidencias, severidade, correcoes e riscos residuais |

## Instalacao

```bash
git clone https://github.com/Basepy/BASE_SKILLS.git
```

Importar ou instalar a pasta `lgpd-saas` completa conforme o procedimento do agente escolhido. Manter os recursos juntos:

```text
lgpd-saas/
|-- SKILL.md
|-- agents/
|   `-- openai.yaml
`-- references/
```

Para ferramentas que exigem ZIP, compactar uma unica pasta de skill, evitando duplicacao como `lgpd-saas/lgpd-saas/SKILL.md`. A descoberta automatica e a execucao de ferramentas dependem do ambiente do agente.

## Exemplos de uso

```text
Use a skill lgpd-saas para auditar o projeto atual.
Apresente os achados com arquivos, linhas, impacto e prioridade.
Nao altere o codigo nesta etapa.
```

```text
Use a skill lgpd-saas para revisar o isolamento entre empresas
e criar testes negativos de autorizacao nos endpoints privados.
```

```text
Use a skill lgpd-saas para mapear os dados pessoais deste SaaS
e propor uma politica de retencao por finalidade.
```

```text
Use a skill lgpd-saas para implementar as correcoes autorizadas,
executar os testes e apresentar os riscos residuais.
```

## Referencias

- [Legislacao brasileira em Markdown](https://github.com/ctresb/leis): localizar normas e conferir cada texto na fonte oficial indicada.
- [ANPD](https://www.gov.br/anpd/pt-br): regulamentacoes e orientacoes oficiais.
- [OWASP ASVS](https://asvs.owasp.org/): requisitos verificaveis de seguranca.
- [OWASP API Security](https://owasp.org/API-Security/): riscos de seguranca em APIs.
- [OWASP Cheat Sheet Series](https://cheatsheetseries.owasp.org/): orientacoes de implementacao.
- [NIST SP 800-63](https://pages.nist.gov/800-63-4/): identidade digital e autenticacao.

A skill distingue obrigacoes legais, boas praticas tecnicas e requisitos contratuais. Testes tecnicos aprovados nao comprovam conformidade integral com a LGPD. Avaliar questoes juridicas conforme a legislacao vigente e o contexto do projeto.
