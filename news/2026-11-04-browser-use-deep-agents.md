# How We Optimized Browser Use for Deep Agents

- **Fonte:** LangChain Blog
- **Autor:** Sydney Runkle
- **Data:** 3 de novembro de 2026
- **Link:** https://www.langchain.com/blog/how-we-optimized-browser-use-for-deep-agents

## Resumo
A LangChain comparou sete conjuntos de ferramentas para agentes controlarem um navegador (Playwright MCP, browser-use, Browserbase MCP, agent-browser, CLI `browse`, Stagehand e Browserbase MCP via código) em benchmarks com sites reais (WebVoyager, HardBench e WebTailBench). Todos passaram entre 78% e 90% das tarefas no WebVoyager, mas custo e velocidade variaram muito: o Stagehand (Browserbase) passou 90% por US$ 1,98 no total, enquanto o Playwright MCP passou 78% por US$ 26,71 (~13x mais caro) e levou 3x mais tempo.

A grande lição: o design das ferramentas pesa mais do que se imagina. O processo foi iterativo — ler traces no LangSmith, achar desperdício de passos/tokens, mudar a ferramenta e validar com evals.

## Pontos principais
- **Code mode:** o agente escreve um trecho de código que executa vários passos de uma vez; só o resultado final volta para o contexto. Média de 10 passos por tarefa vs. 26 no Playwright MCP; uma navegação devolve ~117 caracteres vs. ~17.000 no `navigate` do Browserbase hospedado.
- Chamar as ferramentas MCP do Browserbase via código (em vez de uma a uma) cortou o custo 4x (US$ 17,87 → US$ 4,52).
- **Snapshots da árvore de acessibilidade** com IDs nos elementos interativos são bem mais baratos que screenshots (mediana de 89 KB por screenshot). Cortar o snapshot depois (limite de 8.000 caracteres) não ajudou: o agente buscava a página de novo. O enxugamento tem que ser na origem.
- Aceitar código no estilo Playwright funcionou melhor que a API nativa do Stagehand (+5,3 pontos de acerto, 19% mais barato por tarefa resolvida), porque os modelos foram treinados com muito Playwright.
- Rodar dentro do navegador (extensão) reduz idas e voltas: um `click` do Playwright são 5 chamadas CDP.
- Os traces mostraram agentes usando `waitForTimeout(8000)`. Trocaram por "termina quando a página fica 500 ms quieta": a mediana no HardBench caiu de 182 s para 124 s sem perda de precisão.
- Disponível no Deep Agents open source via `StagehandMiddleware` (`langchain-stagehand`).

## Aplicabilidades práticas
- Para qualquer agente em produção: medir **custo por tarefa resolvida**, não só taxa de acerto — a diferença de 13x aqui veio só da ferramenta.
- Desenhar ferramentas que devolvem pouco e permitem agrupar ações (padrão "code mode") vale também para agentes que chamam Gradle, adb ou APIs internas.
- No FalaEco, o equivalente ao snapshot é entregar ao coach um estado compacto da sessão (cartões devidos, pontos onde o aluno trava) com IDs, em vez de transcrições cruas.
- Usar traces para achar "esperas fixas" e loops inúteis é uma auditoria barata e de alto retorno.
- Testes E2E de telas web internas (portais, backoffice) podem ser explorados por um agente e depois salvos como script Playwright.

## Minha opinião / insight
É um dos posts mais úteis da semana porque traz números concretos e um método reproduzível (trace → mudança → eval). O insight transferível é que **engenharia de ferramentas é engenharia de contexto**: o que a ferramenta devolve decide custo e qualidade. Limitações: é a LangChain avaliando um parceiro (Browserbase) e promovendo o próprio produto; o WebVoyager está quase saturado; os modelos usados são da Anthropic e não há comparação entre modelos. Os números devem ser revalidados no seu cenário antes de virar decisão.
