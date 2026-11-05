# Introducing Managed Deep Agents (+ Browser Use in Managed Deep Agents)

- **Fonte:** LangChain Blog
- **Autor:** Victor Moreira (post principal); Sydney Runkle (post sobre navegador)
- **Data:** publicado em 13 de maio de 2026 (beta privado) e atualizado em 2 de novembro de 2026 (agora em beta público no LangSmith Cloud); post do navegador de 29 de outubro de 2026
- **Link:** https://www.langchain.com/blog/introducing-managed-deep-agents
- **Relacionado:** https://www.langchain.com/blog/browser-use-in-managed-deep-agents

## Resumo
O Managed Deep Agents roda o harness open source Deep Agents dentro do LangSmith. Um agente é uma pasta de arquivos: `agent.py` (com `define_deep_agent`), `instructions.md`, `skills/` e `tools/`. Você testa local com `mda dev` e publica com `mda deploy`, sem montar servidor, fila, cron ou banco. Capacidades de produção viram arquivos: `memory.py` (memória compartilhada e/ou por usuário), `schedules/` (cron), `channels/slack.py`, `sandbox/`, `identity.py` e conexões OAuth, subagentes assíncronos e evals.

O post do navegador adiciona `browser.py` (`define_browser`) com escopo por thread ou por usuário, desligamento automático por inatividade e a ferramenta `browser_handoff`: quando aparece uma tela de login, o agente passa o navegador para a pessoa, que faz login e devolve, e a senha nunca passa pelo modelo. O navegador roda num sandbox separado, com uma ponte `localhost` para o sandbox do agente, o que permite testes E2E do app que o agente acabou de subir.

## Pontos principais
- Agente como projeto de arquivos; deploy de um comando; endpoint da Agent Server API e também um endpoint MCP (`/mcp`), para ser chamado por clientes como o Claude Code.
- Instruções, skills e memória ficam no LangSmith Context Hub, editáveis sem redeploy; o LangSmith Engine analisa traces e propõe correções.
- A própria LangChain roda GTM Agent, Open SWE e Content Studio nele; o Content Studio encolheu cerca de 80% em código.
- Usos citados: triagem de incidentes via Slack, fluxos de engenharia disparados por webhook, assistentes internos, agentes dentro de produto e trabalho agendado.
- Aprovação humana antes de ferramentas específicas via `interrupt_on`.
- Navegador: os passos testados viram script Playwright reaproveitável, sem chamadas de modelo até a página mudar.

## Aplicabilidades práticas
- Protótipo rápido de agente interno para um time de produto (ex.: triagem de erros postados no Slack, que investiga e abre PR).
- Agente agendado que gera um digest diário (de releases, falhas de CI ou métricas de app) com `schedules/`.
- O padrão "agente = pasta com instruções, skills e ferramentas" serve como modelo de organização mesmo sem usar o produto.
- `browser_handoff` é uma referência de design segura para agentes que precisam acessar sistemas com login.
- Exposição via MCP permite plugar o agente no Claude Code/IDE do time.

## Minha opinião / insight
A proposta é boa: tira da frente o trabalho chato (threads duráveis, cron, sandbox, memória, auth) que realmente atrasa agentes em produção. O ponto forte é o design de *capacidades como arquivos*, que é simples e versionável. Limitações: é beta público e amarra execução, memória e instruções ao LangSmith Cloud (lock-in, custo e dados fora da empresa; para isso existe o BYOC, anunciado à parte). O ecossistema é Python, e não há números de custo ou latência publicados. Para um atendimento por IA em produção eu prototiparia com ele para validar o caso de uso, mas manteria a lógica no Deep Agents open source para poder sair se precisar.
