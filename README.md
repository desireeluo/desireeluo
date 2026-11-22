# desireeluo

Espaço de trabalho para editar vídeos com agentes de IA no Claude Code.

## Ferramentas instaladas

| Ferramenta | Pasta | Para que serve |
|---|---|---|
| [OpenMontage](https://github.com/OpenMontageInc/OpenMontage) | `OpenMontage/` | Produção completa: roteiro, narração, imagens, animação e render (Remotion/HyperFrames). |
| [production-crew](https://github.com/shuffleo/production-crew) | `production-crew/` | Versão do OpenMontage com skills extras (geração via fal.ai, ElevenLabs). A rota DaVinci Resolve não funciona na nuvem. |
| [Rushcut](https://github.com/RFingAdam/rushcut) | `rushcut/` | Servidor MCP com ~100 ferramentas de edição via FFmpeg: cortes, vertical, legendas, áudio, checagem de qualidade. |
| [MakeMyClip Editor](https://github.com/MakeMyClip/editor) | comando `clip` | Tira silêncios e takes repetidos, edita pela transcrição, legenda, reenquadra para 9:16 e exporta para Premiere/Resolve/Final Cut. |

Rushcut e MakeMyClip estão registrados como servidores MCP em `.mcp.json`.
Coloque os vídeos em `videos/` (fora do git).

## Como é instalado

Nada disso fica salvo no repositório (veja `.gitignore`). O ambiente de nuvem
**"desireeluo"** do Claude Code roda um script de setup ao iniciar uma sessão
nova, que:

1. Clona OpenMontage e production-crew, roda `make setup` e aponta o Remotion
   para o Chromium já instalado (`remotion.config.ts`), porque o download do
   navegador do Remotion é bloqueado pela rede.
2. Instala `faster-whisper` e as vozes do Piper `pt_BR-faber-medium` e
   `en_US-lessac-medium`.
3. Instala o Rushcut num venv próprio (`rushcut/server/.venv`).
4. Instala Node 24 (exigido pelo MakeMyClip) em `/opt/node24`, o pacote
   `@makemyclip/editor`, compila o whisper.cpp e baixa o modelo `ggml-base`
   (multilíngue). O comando `clip` em `/usr/local/bin` junta tudo isso.

A rede do ambiente libera os sites de mídia grátis (NASA, Wikimedia,
Archive.org, Pexels, Pixabay, Unsplash, Openverse) e o Hugging Face. A variável
`HF_HUB_DISABLE_XET=1` faz o Hugging Face baixar por um caminho liberado.

Chaves de serviços pagos (ElevenLabs, fal.ai etc.) são opcionais e vão no
`.env` de cada ferramenta, nunca neste repositório.
