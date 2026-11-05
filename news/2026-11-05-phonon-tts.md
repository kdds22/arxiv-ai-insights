# A Closer Look at Phonon TTS

- **Fonte:** Hugging Face Blog (Gradium / Phonon)
- **Data:** 5 de novembro de 2026
- **Link:** https://huggingface.co/blog/phonon-tts

## Resumo
A Gradium detalha o Phonon, TTS pequeno (~65–75 MB) que roda on-device, sem rede. Fala inglês, francês, alemão, espanhol e português; mais de 100 vozes; cloning e design de voz. Phonon 31m (EN) é Apache 2.0; o 40m (cinco línguas) é CC BY-NC. Baseado na linhagem Pocket TTS com flow matching.

No Open TTS Leaderboard da Hugging Face, fica no topo ou no top 3 em inteligibilidade nas línguas avaliadas (1º em alemão e espanhol) e lidera time-to-first-audio em CPU no benchmark de streaming. Integração day-0 no Transformers; framework próprio `ptts` com dezenas de backends (CPU, GPU, NPU, browser). Mais de 200 mil downloads nas duas primeiras semanas.

## Pontos principais
- On-device: texto e voz ficam no aparelho; sem round-trip de nuvem.
- Tamanho ~65–75 MB; lida bem com números de telefone, datas e códigos.
- Leaderboard: inteligibilidade forte vs. modelos até 100× maiores; latência de primeiro áudio em CPU é o destaque.
- Voz = tensor de speaker latents pré-computado; cloning com consentimento; custom models com parceiros.
- Transformers (a partir da v5.21) para throughput em GPU; `ptts` para stream único no device.

## Aplicabilidades práticas
- Prototipar TTS local em português para sessões offline ou com privacidade (sem mandar texto para API de voz).
- Medir time-to-first-audio e WER do próprio pipeline antes de trocar o provedor atual.
- Usar vozes pré-computadas / cloning só com consentimento explícito do falante.
- Separar path “device” (latência/UX) de path “batch GPU” (gerar datasets de áudio).

## Relação com meus projetos
- No app de aprendizado de inglês com shadowing e coach: candidato a TTS local em português/inglês com baixa latência e privacidade, sem depender de API de voz a cada turno do aluno.
- Em atendimento por voz ou áudio assistido: útil quando a resposta precisa falar no device; menos relevante se o canal for só texto.

## Minha opinião / insight
É o pick de fala do dia: on-device + português + números de latência. O Apache 2.0 no 31m EN facilita experimento; o 40m multilíngue (com PT) é NC — checar licença antes de produto comercial. Limitação: post do próprio time Gradium no blog da HF; os números do leaderboard são públicos e revalidáveis, o que eu faria no hardware-alvo antes de decidir.
