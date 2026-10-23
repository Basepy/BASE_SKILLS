# Proteção de dados em IA e agentes

- Mapear dados pessoais e segredos enviados a modelos, agentes, ferramentas MCP e provedores, incluindo prompts, anexos, traces, embeddings e logs.
- Minimizar e remover ou mascarar dados desnecessários antes do envio. Avaliar se a associação entre dados pseudonimizados ainda permite identificar pessoas.
- Conferir políticas e contratos atuais de retenção, treinamento, subprocessadores e localização de processamento; não presumir condições pelo nome comercial do plano.
- Tratar respostas de modelos, documentos e conteúdo recuperado como entradas não confiáveis. Impedir que instruções de conteúdo externo ampliem permissões ou autorizem envio de dados.
- Verificar isolamento de usuários e tenants em memória, busca, RAG, caches e ferramentas. Validar autorização em cada ação do agente no servidor.
- Limitar ferramentas e destinos ao necessário; validar argumentos e saídas. Exigir autorização explícita aplicável à ação antes de operações financeiras reais, exclusões ou mudanças críticas de permissões, respeitando escopo e limites já autorizados.
