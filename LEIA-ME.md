# Tap Test — aplicativo

Arquivos desta pasta:

| arquivo | função |
|---|---|
| `index.html` | o aplicativo |
| `manifest.webmanifest` | nome, ícone e cores usados na instalação |
| `sw.js` | guarda o app no aparelho para funcionar offline |
| `icon-*.png` | ícones do aplicativo |

## Como funciona a hora

Na **primeira abertura** o app precisa de internet: ele consulta um servidor de hora, mede o
atraso da rede e guarda a diferença para o relógio do aparelho. Daí em diante **funciona
offline** — a correção fica salva e o app abre sem conexão nenhuma.

Ao lado do relógio aparece o estado, que é tocável para sincronizar de novo:

- `hora sincronizada` — acabou de acertar com o servidor
- `sincronizado · corrigido 4s` — o relógio do aparelho estava fora, e o app corrigiu
- `offline · sincronizado em 07/08 22:04` — sem internet agora, usando a última correção
- `sem sincronia · tocar para tentar` — nunca sincronizou; conecte-se uma vez

São três fontes de hora, tentadas em ordem: worldtimeapi, timeapi.io e, por último, a hora do
próprio servidor onde o app estiver hospedado.

## Passo 1 — publicar (necessário para instalar e para gerar o APK)

O app precisa estar num endereço **https**. O caminho gratuito mais simples é o GitHub Pages:

1. Crie um repositório no GitHub e envie os arquivos desta pasta na raiz.
2. Em *Settings → Pages*, escolha a branch `main` e a pasta `/root`.
3. Em um ou dois minutos o endereço fica disponível:
   `https://SEU-USUARIO.github.io/SEU-REPOSITORIO/`

## Passo 2 — instalar direto no celular (já funciona como aplicativo)

Abra esse endereço no Chrome do Android e use **Instalar aplicativo** no menu de três pontos.
Ele ganha ícone na tela inicial, abre em tela cheia sem barra do navegador e funciona offline.
No iPhone, o caminho é Safari → Compartilhar → **Adicionar à Tela de Início**.

Para a maioria dos usos isso substitui o APK.

## Passo 3 — gerar o APK

Se precisar mesmo do arquivo `.apk` (para distribuir por dentro da empresa, por exemplo):

**Opção A — PWABuilder (sem instalar nada)**

1. Acesse `https://www.pwabuilder.com`
2. Cole o endereço publicado no passo 1 e clique em *Start*.
3. Em *Package for stores → Android*, escolha *Generate*.
4. Baixe o pacote: vem o `.apk` para instalar direto e o `.aab` para a Play Store.

Ao instalar um APK fora da loja, o Android pede para autorizar "fontes desconhecidas".

**Opção B — Capacitor (controle total, exige Android Studio)**

```bash
npm init -y
npm install @capacitor/core @capacitor/cli @capacitor/android
npx cap init "Tap Test" com.suaempresa.taptest --web-dir=.
npx cap add android
npx cap sync
npx cap open android      # compila e assina pelo Android Studio
```

## Observações

- **Câmera para ler código de barras**: funciona no Chrome do Android com o app em https.
  No iPhone o navegador não tem esse recurso; ali o número de série é digitado.
- **Download do PDF**: funciona normalmente com o app instalado ou aberto no navegador.
- **Tela ligada**: o app pede ao sistema para não apagar a tela durante o teste. É um pedido,
  não uma garantia — se o aparelho recusar, aumente o tempo de bloqueio nas configurações.
- Ao atualizar o app, troque `tap-test-v1` por `tap-test-v2` na primeira linha do `sw.js`,
  senão os aparelhos continuam abrindo a versão guardada em cache.
