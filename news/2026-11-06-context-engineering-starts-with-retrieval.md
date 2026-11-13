# Context Engineering Starts with Retrieval

- **Fonte:** LangChain Blog
- **Autores:** Jess Weng
- **Data:** 23 de outubro de 2026
- **Link:** https://www.langchain.com/blog/context-engineering-starts-with-retrieval

## Resumo
Post prático (distinto do “late 2026 challenges” já no repositório) sobre retrieval no harness do agente. A busca quebra de três jeitos: procura ineficiente, payload grande demais de uma vez, e contexto irrelevante ou stale. No harness dos Deep Agents, as tools de filesystem buscam antes de ler: `glob` no nome, `grep` nas linhas, `read_file` paginado. Resultados grandes de tool são offloaded — o resultado inteiro vai para arquivo e o agente recebe o caminho e um preview. Para busca própria (RAG), o padrão é retrieve → offload → delegate: salvar, devolver paths e deixar subagentes lerem; o agente principal só vê as conclusões.

## Pontos principais
- Três falhas de retrieval: busca repetida/cega, contexto demais, evidência errada ou velha.
- Buscar pouco (nome e palavra-chave) antes de abrir o arquivo.
- Offload de tool results grandes; o contexto leva path + preview, não o dump.
- Subagente que filtra a leitura; o orquestrador não come o corpus.

## Aplicabilidades práticas
- Em qualquer agente com tools e arquivos, expor busca por nome/linha e leitura paginada.
- Nunca colar export ou transcript inteiro no contexto: salvar, devolver o caminho, resumir à parte.
- Para RAG, o mesmo padrão: recuperar, offload, delegar a leitura.

## Relação com meus projetos
- No app de aprendizado de inglês: coach e simulador que puxam material do aluno devem usar paths + subagente resumidor, em vez de colar transcript ou export inteiro no contexto.
- Num atendimento com IA via WhatsApp e tools MCP: retornos grandes de tool seguem o mesmo offload, para o orquestrador não estourar a janela no meio do turno.

## Minha opinião / insight
Fecha a nota de context engineering late 2026: de desafios abertos para técnicas concretas de retrieval no harness. Combina com compactação e compressão de tools já no repositório — aqui o corte acontece *antes* da janela encher. É texto de produto, mas os três modos de quebra e o trio buscar/offload/delegar são reproduzíveis em qualquer stack.
