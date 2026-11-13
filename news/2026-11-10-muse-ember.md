# Introducing Our Smallest, Most Efficient Model: Muse Ember

- **Fonte:** Meta AI Research
- **Data:** 9 de novembro de 2026
- **Link:** https://research.meta.ai/blog/muse-ember

## Resumo
A Meta lançou o Muse Ember, modelo pequeno pensado para o que agentes repetem o dia todo: tool calls, subtarefas de código, roteamento, extração e parsing de documentos longos. Na API da Meta custa US$ 0,10 por milhão de tokens de entrada e US$ 0,50 de saída em prompts de até 200K tokens; acima disso o preço sobe para US$ 0,30 / US$ 1,50 (entrada em cache a US$ 0,012). A janela é de 1M de tokens, com até 512K de saída. A Meta afirma, com números da Artificial Analysis, que empata o melhor score do Claude Haiku 5.5 a cerca de um terço do custo por tarefa e fica na fronteira de eficiência do leaderboard. Há depoimentos de parceiros (Box, Cline, Oracle, Cloudflare, You.com) sobre velocidade e uso como subagente.

## Pontos principais
- Faixa barata voltada a passos repetidos do agente, não a um modelo de topo.
- Preço de lista baixo em prompts curtos; o custo sobe acima de 200K tokens, apesar da janela de 1M.
- A comparação anunciada é por custo por tarefa, não só por token.
- É anúncio do fornecedor, com métricas de terceiro e quotes de parceiros.

## Aplicabilidades práticas
- Candidato a comparar, no próprio eval, na faixa de modelo pequeno para tool calls e tarefas repetidas.
- Medir custo por tarefa (e com prompts longos, o preço maior), não copiar o gráfico do post.
- Não generaliza para “todo lançamento de modelo vale a pena olhar”: o recorte aqui é o andar de baixo do agente.

## Relação com meus projetos
- Num atendimento com IA via WhatsApp (orquestrador + servidores MCP): vale um bake-off na faixa barata usada em chamadas repetidas, contra o modelo pequeno atual, no eval próprio.
- No app de aprendizado de inglês: eventual candidato a subtarefas baratas (rotear exercício, extrair sinal da sessão), não ao juiz de fala nem ao simulador de conversa.

## Minha opinião / insight
É o único lançamento de modelo que passou no swipe deste dia, e o recorte importa: modelo pequeno para o trabalho repetido do agente, julgado por custo por tarefa. Os números são do fornecedor e da AA — o teste que conta é no próprio tráfego, inclusive acima de 200K tokens, onde o preço muda.
