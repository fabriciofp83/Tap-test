# Tap Test — o que foi feito e como o app funciona

## O que é

Um aplicativo de campo que conduz o Tap Test: ele acompanha o relógio do Reino Unido,
avisa a hora exata de cada batida com bipe e sinal na tela, e monta o registro do teste
no fim, pronto para copiar ou salvar em PDF.

---

## Como funciona, na prática

**1. Configuração**
Escolha quantos nodes entram no teste (de 2 a 8). O app calcula sozinho quantos setores
são — dois nodes por setor — e mostra a duração total. Em seguida, o número de série de
cada node, digitado ou lido pela câmera no botão de código de barras. O preenchimento é
obrigatório e a série é conferida: 12 caracteres terminando em NSG ou NCG, ou 14 terminando
em NSGSH ou NCGSH. Fora desse padrão o campo fica em vermelho e o teste não começa. Digitando, o campo seguinte é
alcançado pela tecla Próximo do teclado; pela câmera, o cursor avança sozinho. A identificação já vem preenchida
com a data do dia.

**2. Início**
O botão Iniciar agenda a partida para o próximo minuto cheio, com zero segundos. Nos
cinco segundos finais o app dá bipes de contagem.

**3. Durante o teste**
A tela ocupa a altura do aparelho, sem rolagem, e não se mexe do começo ao fim. Nela:

- o **quadro da próxima ação** — o que bater, em qual node, a que horas e quanto falta;
- o **desenho dos nodes**, com o node da vez aceso e os já testados apagados;
- o botão **Encerrar teste**, que pede dois toques para não parar sem querer.

Cada batida tem cinco bipes de contagem e um som próprio na hora exata, diferente do som
da contagem. A batida no chão de cada setor acende o círculo correspondente.

**4. No final**
Sai o relatório: hora de início, cada node com sua série e suas três batidas, as batidas
no chão e o resumo com início, final e duração. Dá para copiar o texto ou baixar o PDF.

---

## A lógica do teste

Cada node segue sempre a mesma sequência, contada a partir do minuto de início:

| momento | batida |
|---|---|
| +15s | uma ao lado do hidrofone (abre o node) |
| +30s | **Inline** — batida traseira |
| +60s | **Crossline** — batida lateral |
| +90s | **Vertical** — em cima + duas ao lado do hidrofone |

Fechado o node, o app espera 15 segundos e recomeça no seguinte. Terminado o último,
vêm as batidas no chão, uma por setor, a cada 30 segundos, do setor 1 até o último —
essa última batida encerra o teste.

---

## O que foi construído

**Roda em qualquer tela.** Celular, tablet e computador. Os textos, o desenho e os
espaçamentos se ajustam à tela: o texto da próxima ação sempre cresce até o maior tamanho
que ainda cabe, sem empurrar o desenho nem o botão para fora.

**Aplicativo instalável, que funciona offline.** Publicado num endereço https, o app pode
ser instalado pelo navegador: ganha ícone, abre em tela cheia e funciona sem internet. Não
foi possível gerar o APK aqui, mas o formato entregue vira APK em um passo — o caminho
está no LEIA-ME.

**Nada se perde.** O app guarda a sessão no aparelho a cada batida. Se fechar sem querer,
ao reabrir ele oferece o relatório do último teste concluído — e ele continua acessível na
tela inicial mesmo depois de tocar em Novo teste, até você descartá-lo ou iniciar outro
teste. Passadas 24 horas, expira sozinho.

### Além disso

- **Relógio corrigido:** ao abrir com internet, o app compara com um servidor de hora,
  desconta o atraso da rede e guarda a diferença. Daí em diante trabalha offline com essa
  correção. Um selo ao lado do relógio mostra o estado, e avisa em âmbar quando a hora
  ainda não foi acertada.
- **Horário de verão automático:** o app usa o fuso oficial de Londres, então a virada
  entre BST e GMT acontece sozinha na data certa.
- **Registro em PDF** gerado dentro do próprio app, sem depender de internet ou de
  qualquer serviço externo.
- **Leitura de código de barras** pela câmera para os números de série.
- **Tela sempre acesa** durante o teste (o app pede ao sistema; onde for permitido, a tela
  não apaga).

---

## Onde abrir

| forma de abrir | funciona |
|---|---|
| Instalado pelo navegador (https) | tudo |
| Aberto direto no navegador (https) | tudo |
| Arquivo baixado, aberto do gerenciador | teste e relatório; sem sincronia de hora nem câmera |
| Dentro de um visualizador | teste e relatório; sem download de PDF nem câmera |

A recomendação é publicar e instalar — é a única forma em que todos os recursos funcionam,
e a instalação leva um minuto.

---

## Próximo passo

O `LEIA-ME.md` traz o passo a passo para publicar a pasta (GitHub Pages, gratuito) e, a
partir daí, gerar o APK pelo PWABuilder ou pelo Android Studio.

Ao publicar uma versão nova, lembre de subir o número na primeira linha do `sw.js`
(hoje em `tap-test-v42`), senão os aparelhos continuam abrindo a versão guardada.
