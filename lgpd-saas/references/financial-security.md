# Segurança financeira

- Verificar autorização e autenticação proporcional ao risco para pagamentos, saques, mudança de destinatários e movimentações.
- Validar no servidor valores, moedas, precisão decimal ou unidades inteiras mínimas, destinatários, limites e transições de estado. Não confiar em cálculos exclusivos do frontend.
- Verificar idempotência vinculada à operação e ao titular, incluindo payload divergente, retries, falhas parciais e concorrência. Usar garantias transacionais e restrições persistentes para impedir duplicações.
- Investigar race conditions, replay e gasto lógico duplicado. Testar com mocks ou sandbox do provedor.
- Distinguir aceitação, pendência e liquidação confirmada segundo o protocolo. Separar sucesso financeiro de falhas em notificações e efeitos auxiliares.
- Proteger credenciais e aplicar o mecanismo de autenticação de webhook realmente suportado pelo provedor. Conferir corpo assinado, janela de tempo quando existente, deduplicação e reconciliação.
- Distinguir carteiras custodiais e não custodiais. Não coletar seed ou chave privada se não houver necessidade de custódia; quando houver, avaliar gestão especializada de chaves, acesso e recuperação.
- Minimizar logs de invoices, preimages, credenciais Lightning, dados Pix e identificadores financeiros; nunca incluir segredos em evidências de auditoria.
