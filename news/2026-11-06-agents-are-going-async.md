# Agents Are Going Async

- **Fonte:** LangChain Blog
- **Autores:** Sydney Runkle, Thushanth Bengre
- **Data:** 5 de novembro de 2026
- **Link:** https://www.langchain.com/blog/agents-are-going-async

## Resumo
O post descreve o padrão de subagentes assíncronos nos Deep Agents: um orquestrador fica com o usuário e o contexto da conversa, enquanto workers rodam em background e reportam ao terminar. Num loop ReAct clássico, cada tool longa bloqueia o resto. Aqui o trabalho escala com o número de workers, não com o comprimento de um único loop. O orquestrador gerencia as tarefas com cinco tools (start, check, update, cancel, list). O campo `update_strategy` separa correção (`interrupt`, reinicia com a instrução nova) de acréscimo (`enqueue`, espera o run atual acabar). Notificações cobrem orquestrador ocupado, ocioso ou pausado numa aprovação: o resultado não derruba o pedido de aprovação humana.

## Pontos principais
- Orquestrador responsivo + workers em background que reportam ao concluir.
- Cinco tools de ciclo de vida; steering é separado de “alcançar o orquestrador”.
- `interrupt` vs `enqueue` distingue “para e corrige” de “quando terminar, faça X”.
- Aprovação humana no orquestrador não é interrompida pelo reporte do worker.

## Aplicabilidades práticas
- Em fluxos com tools longas, não prender o loop do usuário no worker.
- Expor status das tarefas em voo e um caminho de cancelar/atualizar.
- Separar correção urgente de acréscimo que pode esperar o fim do run.

## Relação com meus projetos
- Num atendimento com IA via WhatsApp (orquestrador + servidores MCP e papéis de um negociador): workers longos (consulta, conferência) sem travar a conversa; aprovação humana permanece no fio do orquestrador.
- No app de aprendizado de inglês: coach, simulador de conversa e avaliador de fala podem rodar tarefas longas em background sem sumir da conversa do aluno; `enqueue` encaixa “quando terminar, rode os testes”.

## Minha opinião / insight
É o padrão de orquestração que amarra o handoff de requisitos (2611.07483) a workers longos: o contrato não pode se perder só porque o trabalho saiu do loop. Limitação: post de produto da LangChain, descritivo, sem número de qualidade — o valor está no desenho das tools e das estratégias de update.
