# arXiv AI Insights

Curadoria pessoal de **papers do arXiv** e **notícias de IA** sobre LLMs, agentes de IA, sistemas multiagente e boas práticas de engenharia de aplicações com IA, com insights de como aplicar cada item nos meus projetos.

## Como funciona

Este repositório é mantido junto com o **Grok Bot**, um assistente que roda três rotinas automáticas. Todos os horários são de Brasília.

| Rotina | Quando | O que faz |
|---|---|---|
| Digest arXiv | dias úteis, 7h50 | Busca os papers novos (cs.CL, cs.AI, cs.LG, cs.MA) e me manda de 10 a 15 itens com resumo |
| Digest de notícias | dias úteis, 12h | Lê as fontes de [`news/SOURCES.md`](news/SOURCES.md) (labs, blogs técnicos, agregadores), ignora clickbait e me manda os destaques |
| Resumo semanal | sextas, 17h | Junta os papers e notícias da semana em tendências e ideias de aplicação, salvas em `weekly/` |

O fluxo de cada dia:

1. **Curadoria.** Os itens chegam agrupados em *Recomendados pra você* (de acordo com meu histórico de gostos), *Outros (TL;DR)* (nada é descartado) e *Correlações* entre itens e notas antigas.
2. **Escolha por swipe.** Os mesmos itens vão para um painel interativo onde deslizo para a direita (curti) ou para a esquerda (passo) e copio as escolhas de volta para o chat.
3. **Registro.** Cada item curtido vira uma nota com link, resumo, aplicações práticas, relação com meus projetos e uma opinião crítica com limitações.
4. **Aprendizado.** As escolhas e os descartes ficam num journal privado, e as próximas recomendações se ajustam a eles.

O contexto dos meus projetos vem de um journal técnico privado. Aqui ele aparece só em termos genéricos.

## Estrutura

- `papers/AAAA-MM-DD-<arxiv-id>-<slug>.md`: uma nota por paper escolhido, listados em [`INDEX.md`](INDEX.md)
- `news/AAAA-MM-DD-<slug>.md`: uma nota por notícia escolhida, listadas em [`news/INDEX.md`](news/INDEX.md)
- `weekly/AAAA-Www.md`: resumos semanais
