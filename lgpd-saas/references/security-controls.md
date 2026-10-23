# Controles de segurança e testes

## Multi-tenant e IDOR/BOLA

- Identificar fronteiras por usuário, conta, organização e tenant. Verificar autorização no backend em toda leitura e escrita de recurso privado.
- Rastrear user_id, account_id, transaction_id, wallet_id e organization_id até consultas e serviços. Não confiar em IDs fornecidos pelo frontend como prova de permissão.
- Incluir downloads, exports, storage, WebSockets, caches e jobs assíncronos. Propagar contexto de tenant com validação; verificar também workers e acessos administrativos.
- Avaliar RLS no PostgreSQL quando adequado, incluindo papéis que a contornam e contexto em conexões reutilizadas; manter autorização da aplicação.

## Supply chain

- Examinar dependências diretas e transitivas com manifests e lockfiles. Consultar alertas atuais e registrar versão afetada, correção disponível e alcance real no projeto.
- Avaliar abandono, pacotes suspeitos, dependency confusion e scripts de instalação. Usar lockfiles e versões controladas; considerar SBOM e integridade no CI/CD conforme risco.
- Avaliar compatibilidade antes de atualizar dependências críticas. Não instalar pacotes suspeitos para investigá-los.

## Verificação proporcional

- Criar testes negativos de acesso entre dois usuários e dois tenants, incluindo leitura, alteração, listagem, arquivos e recursos administrativos.
- Verificar campos desnecessários nas respostas de API, credenciais em logs e acesso a comprovantes e relatórios.
- Testar expiração, revogação e rotação de credenciais, assinatura e idempotência de webhooks e fluxos de exportação e eliminação.
- Usar dados sintéticos e ambiente isolado. Reproduzir falhas sem movimentar dinheiro nem alterar dados reais.
- Registrar comportamento esperado, resultado observado e limitações. Testes aprovados não comprovam ausência de todas as vulnerabilidades.
