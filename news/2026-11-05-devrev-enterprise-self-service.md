# DevRev delivers autonomous self-service with GPT-6.1 Sol

- **Fonte:** OpenAI News (customer story)
- **Data:** 4 de novembro de 2026
- **Link:** https://openai.com/index/devrev-enterprise-self-service

## Resumo
A DevRev usa modelos da OpenAI (incluindo GPT-6.1 Sol) nos produtos Computer e Operator para levar pedidos difíceis de clientes e funcionários até o fim. Os agentes raciocinam sobre dados vivos da empresa; ações são reversíveis e as respostas apontam para as fontes. O CTO Ahmed Bashir enfatiza o equilíbrio entre capacidade de raciocínio, confiança/alinhamento e latência/custo sustentável.

No Agent Studio, parte do comportamento das tools é descrita em conversa com a IA e parte fica em regras fixas. A DevRev avalia modelo + harness juntos no Enterprise-Bench (dados versionados, informação espalhada em sistemas, acesso por papel). A ambição seguinte é o Operator assumir pedidos mais longos mantendo rastreabilidade, permissão e reversibilidade — self-service além de FAQ, upgrade e reembolso.

## Pontos principais
- Raciocínio + dados vivos + ações com permissão e reversíveis.
- Tradeoff explícito raciocínio × latência × custo no self-service.
- Agent Studio: regras fixas + descrição conversacional de tools.
- Enterprise-Bench: versão de dados, sistemas distintos, acesso por papel.
- Pedidos devem completar em segundos, não minutos; Decisions API / Ultrafast citados como caminho para passos que não pedem raciocínio profundo.

## Aplicabilidades práticas
- Em atendimento automatizado: separar o que é regra fixa (política, limites de ação) do que o modelo decide em linguagem natural.
- Medir latência e custo por resolução, não só taxa de acerto — o case insiste nisso.
- Benchmark interno com dados versionados e papéis de acesso diferentes do “happy path”.
- Desenhar ações reversíveis + apontar fonte antes de deixar o agente executar mudanças.

## Relação com meus projetos
- Espelho direto de um atendimento com IA via WhatsApp com orquestrador e servidores MCP: intent, tools com permissão, handoff para humano e tradeoff custo-latência no self-service.
- No app de inglês com coach e conversa: o mesmo padrão de “descrever tool em linguagem + regras fixas” ajuda a manter o agente no papel sem hardcodar cada fluxo.

## Minha opinião / insight
É um case de produto OpenAI (com menção a Codex no time interno), então o tom é promocional. O valor está no desenho: permissões, reversibilidade, fonte citável e bench com dados versionados/papéis — checklist útil independente do modelo. Eu usaria a lista como auditoria do próprio harness, sem comprar o framing de “modelo X resolve”.
