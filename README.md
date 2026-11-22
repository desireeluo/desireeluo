# desireeluo

Espaço de trabalho para editar vídeos com agente usando o
[OpenMontage](https://github.com/OpenMontageInc/OpenMontage).

## Como funciona

O OpenMontage não fica salvo neste repositório (está no `.gitignore`).
O ambiente de nuvem **"desireeluo"** do Claude Code instala tudo ao iniciar
uma sessão nova:

1. Clona o OpenMontage em `OpenMontage/` e roda `make setup`
   (Python, Remotion, HyperFrames, Piper TTS).
2. Cria `OpenMontage/remotion-composer/remotion.config.ts` apontando o
   Remotion para o Chromium já instalado (`/opt/pw-browsers/...`), porque o
   download do navegador do Remotion é bloqueado pela rede.
3. Baixa as vozes do Piper `pt_BR-faber-medium` e `en_US-lessac-medium`.

A rede desse ambiente libera os sites de mídia grátis (NASA, Wikimedia,
Archive.org, Pexels, Pixabay, Unsplash, Openverse) e o Hugging Face (vozes).

## Instalação manual

```bash
git clone --depth 1 https://github.com/OpenMontageInc/OpenMontage.git
cd OpenMontage
make setup
```

Teste sem chaves de API: `make demo`.

Chaves de serviços pagos (ElevenLabs, fal.ai etc.) são opcionais e vão em
`OpenMontage/.env`, nunca neste repositório.
