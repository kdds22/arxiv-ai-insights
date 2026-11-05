# New context engineering challenges in late 2026

- **Fonte:** LangChain Blog (série "Harrison's In the Loop")
- **Autor:** Harrison Chase (CEO da LangChain)
- **Data:** 2 de novembro de 2026
- **Link:** https://www.langchain.com/blog/context-engineering-challenges-late-2026

## Resumo
Harrison observa que o mercado convergiu para a mesma arquitetura de agente: um LLM em loop, chamando ferramentas, dentro de um sandbox. Por isso muitos engenheiros acham que "os problemas difíceis estão resolvidos". As práticas de engenharia de contexto já viraram quase padrão: resumir threads longas, descarregar resultados grandes de ferramentas, skills para revelação progressiva, busca de ferramentas, subagentes para isolar contexto e bash como ferramenta principal.

O argumento dele é que agentes **proativos, sempre ligados e orientados a objetivos** trazem uma nova leva de problemas em aberto, sem solução geral ainda.

## Pontos principais
- **Proatividade sem ser chato:** agentes que acordam por eventos ou "heartbeats" precisam calibrar quanto notificar.
- **Memória:** a estrutura de dados é simples (arquivos, uma string); o difícil é decidir *o que* lembrar, sem guardar nada nem guardar detalhe demais.
- **Assíncrono:** trabalho em subagentes e ferramentas de longa duração. Como avisar o agente principal quando termina? E se ele estiver rodando, já tiver encerrado ou estiver esperando aprovação humana?
- **Acompanhar objetivos:** quebrar metas em experimentos, iterar sem repetir e manter coerência em horizontes longos.
- **Alinhamento:** metas que o agente pode "trapacear" (ex.: "remova todos os bugs" → apaga o código).
- **Navegador** como a nova ferramenta principal (o que o bash é para agentes de código), com o desafio de lidar com DOM ou imagem no contexto.

## Aplicabilidades práticas
- Checklist de design para qualquer agente que for ficar rodando sozinho: política de notificação, política de memória, fluxo assíncrono e critérios anti-trapaça.
- Ao definir metas para agentes de código (ex.: "deixe o CI verde"), escrever restrições explícitas (não apagar testes, não desativar lint) e revisar os diffs.
- Para notificações (Slack, apps), começar com um resumo agrupado e limites de frequência, e ajustar com feedback.
- Em memória, guardar decisões e preferências, não transcrições; revisar o que o agente "aprendeu".

## Minha opinião / insight
É um texto curto e opinativo, sem dados nem soluções, mas útil como **mapa dos problemas** de quem vai além de agentes de código. A lista bate com o que se vê na prática; alinhamento e proatividade costumam ser os que mais quebram a confiança dos usuários. Limitações: é um CEO que vende infraestrutura para exatamente esses problemas, e o texto não traz evidência nem recomendações concretas. Vale como pauta de discussão no time, não como guia de implementação.
