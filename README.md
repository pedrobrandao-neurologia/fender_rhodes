# 🎹 Suitcase 73 — Emulador de Fender Rhodes

Emulação do **Fender Rhodes Suitcase Seventy Three** — o piano elétrico tocado por Billy Preston com os Beatles nas sessões de *Get Back* (1969) — direto no navegador, sem instalar nada.

Todo o app é um único arquivo `index.html`: sem dependências, sem build, sem servidor. O som é 100% sintetizado em tempo real com a **Web Audio API** (nenhum sample de áudio é carregado).

---

## 🚀 Como executar

**Opção 1 — abrir localmente**

1. Baixe ou clone este repositório.
2. Abra o arquivo `index.html` em qualquer navegador moderno (Chrome, Edge, Safari, Firefox).
3. Toque em **Ligar** — os navegadores exigem um gesto do usuário para iniciar o áudio.

**Opção 2 — publicar no GitHub Pages**

Em *Settings → Pages*, selecione a branch principal e a pasta raiz (`/`). O piano ficará disponível em `https://<seu-usuario>.github.io/fender_rhodes/` e poderá ser tocado de qualquer celular ou computador.

> 💡 **Use fones de ouvido ou caixas estéreo.** O vibrato do Suitcase é um efeito de *auto-pan* que balança o som entre os canais esquerdo e direito — em alto-falante mono o efeito se perde.

---

## 🎛️ Como usar

### Na tela (celular e tablet)

- **Dinâmica por posição do toque:** quanto mais perto da **borda de baixo** da tecla, mais forte a nota — imitando a resposta de velocidade de um piano real.
- **Glissando:** deslize o dedo pelas teclas.
- **Acordes:** o teclado é multitoque — use quantos dedos quiser.
- **Oct − / Oct +** deslocam a região visível do teclado (o indicador mostra o intervalo atual, ex.: `C3–C5`).

### Controles do painel

| Controle | O que faz |
|---|---|
| **Instrumento** | Seleciona o instrumento emulado: **Rhodes 73** ou **Lowrey ’68 · Baba O’Riley** (veja o módulo abaixo) |
| **Volume** | Volume geral do instrumento |
| **Vibrato veloc.** | Velocidade do balanço estéreo (0,5–9 Hz) |
| **Vibrato intens.** | Intensidade do balanço entre os alto-falantes |
| **Timbre (bark)** | Do som suave e escuro ao ataque metálico agressivo ("bark") típico do Rhodes tocado forte |
| **Chorus** | Espessamento do som com duas linhas de delay moduladas |
| **Reverb** | Ambiência de sala pequena, com caráter de spring reverb |
| **Preset** | Aplica combinações prontas de todos os controles (veja abaixo) |
| **Tempo (BPM)** | Só no modo Lowrey: andamento da grade de semicolcheias do *marimba repeat* (padrão 117, como na gravação) |
| **Sustain** | Trava o pedal de sustain (as notas continuam soando após soltar as teclas) |
| **▶ Demo** | Toca um vamp de demonstração para você ouvir o timbre |
| **● Rec** | Grava o que você toca; ao parar, baixa o arquivo de áudio (`.webm`/`.m4a`) |
| **MIDI** | Luz indicadora — acende quando um teclado MIDI é detectado |
| **?** | Abre a ajuda com todos os atalhos |
| **Tela cheia** | Modo imersivo, sem as barras do navegador |

### Presets de timbre

| Preset | Caráter |
|---|---|
| **Get Back ’69** | O voicing padrão: escuro, vibrato médio, pouco efeito — o som das sessões de 1969 |
| **Balada Suave** | Vibrato lento e sutil, timbre macio, bastante chorus e reverb |
| **Funk Setentão** | Vibrato rápido e fundo, ataque agressivo ("bark"), som seco |
| **Sonho Estéreo** | Auto-pan profundo, chorus e reverb generosos — som flutuante |

Qualquer ajuste manual nos sliders volta o seletor para **Manual**. Todas as configurações (incluindo a oitava) são **salvas automaticamente** no navegador e restauradas na próxima visita.

### Atalhos do teclado do computador

| Tecla | Ação |
|---|---|
| `A S D F G H J K L ;` | Teclas brancas (a partir da nota mais grave visível) |
| `W E T Y U O P` | Teclas pretas |
| `Z` / `X` | Desce / sobe uma oitava |
| `Espaço` (segurar) | **Pedal de sustain** — segure para sustentar, solte para abafar |

As letras aparecem discretamente sobre as teclas quando o app detecta mouse/teclado físico.

### 🎹 Teclado MIDI

Em navegadores com **Web MIDI** (Chrome e Edge), conecte um controlador MIDI por USB ou Bluetooth e toque com dinâmica real:

- *Note on/off* com velocidade → dinâmica completa do timbre;
- **Pedal de sustain (CC64)** do controlador funciona normalmente;
- A luz **MIDI** no painel acende quando um dispositivo é detectado (o nome aparece no *tooltip*), inclusive ao conectar/desconectar com o app aberto.

---

## 🎚️ Módulo Lowrey ’68 — o som de "Baba O'Riley"

Selecione **Instrumento → Lowrey ’68 · Baba O’Riley** e o app deixa de ser um Rhodes para emular o equipamento que criou o intro mais famoso do The Who.

### A história real (a pesquisa por trás do módulo)

O "sintetizador" hipnótico de *Baba O'Riley* (álbum *Who's Next*, 1971) **não é um sintetizador**: é um **órgão doméstico Lowrey Berkshire Deluxe TBO-1 (1968)** tocado por Pete Townshend em seu estúdio caseiro, usando o recurso **"marimba repeat"** do próprio órgão. Townshend chegou a tentar o mesmo resultado com um sequenciador/sintetizador ARP, mas não conseguiu o som que queria — o padrão veio todo do Lowrey. O sinal do órgão ainda passava por um sintetizador **EMS VCS3 mk1**, usado como processador/filtro.

Funcionalmente, o *marimba repeat* é um **note-repeater**: um LFO em onda quadrada retriggerando a amplitude — ele "picota" cada nota segurada em subdivisões rápidas de **semicolcheia (1/16)**, no andamento de **~117 BPM** da gravação. E o segredo do padrão entrelaçado **não é um arpejador programado**: a síncope vem do **timing manual** de quando cada nota é pressionada. Cada nota repete na fase em que foi tocada — em *Baba O'Riley*, **F e C caem no tempo forte** e as outras notas no **contratempo**, gerando a alternância rápida F–C–F–C. A tonalidade é **Fá maior**, com a figura básica F–C e o **Bb** aparecendo nos acordes; os floreios mais rápidos chegam a fusas (1/32).

### Como o módulo emula isso

- **Chopper de semicolcheias sincronizado ao toque**: um relógio interno roda a grade de 1/16 no BPM escolhido; a **primeira nota pressionada define o tempo forte** e cada nota seguinte herda a fase do ponto da grade mais próximo do momento em que foi tocada — toque F no tempo e C logo depois (no contratempo) e a figura F–C–F–C surge sozinha, exatamente como no órgão real;
- **Timbre brilhante e flautado**: cada batida é sintetizada por 4 parciais harmônicos (1×, 2×, 3×, 4×) com ataque de 3 ms e *gate* curto — notas percussivas e distintas, imitando o registro de marimba do Lowrey;
- **Filtro no papel do EMS VCS3**: o controle **Timbre** abre/fecha um lowpass com leve ressonância, do abafado ao brilhante;
- **Tempo (BPM)** ajusta o andamento da grade de semicolcheias — o padrão de fábrica é 117 BPM, o andamento da gravação original (~116–119);
- **Sustain trava o padrão**: com o pedal ativo (botão ou `Espaço`), as notas soltas continuam repetindo na fase original — deixe o "loop" rodando e sole por cima, como na música;
- **Pulso visual**: as teclas piscam em âmbar a cada batida, mostrando o entrelaçamento tempo/contratempo;
- Os efeitos do gabinete (chorus, reverb, vibrato estéreo) continuam disponíveis — ao entrar no modo Lowrey o app aplica um ajuste sóbrio (vibrato desligado, reverb leve), fiel à gravação, e o **Demo** passa a demonstrar a técnica do stagger.

> 🎵 **Receita clássica:** entre no modo Lowrey, ligue o **Sustain**, toque **F** no tempo e **C** logo em seguida (uma semicolcheia depois) e segure — a figura F–C–F–C continua sozinha. Adicione **Bb** nos acordes e improvise floreios em Fá por cima, no melhor estilo *teenage wasteland*.

### Referências da pesquisa

- [Songfacts — Baba O'Riley by The Who](https://www.songfacts.com/facts/the-who/baba-oriley)
- [Whotabs — Lowrey Berkshire Deluxe TBO-1 (equipamento de Pete Townshend)](https://www.thewho.net/whotabs/gear/guitar/lowrey.html)
- [KVR Audio Forum — Lowrey Organ Marimba Repeat, aka Baba O'Riley](https://www.kvraudio.com/forum/viewtopic.php?t=354382)
- [Wikipedia — Baba O'Riley](https://en.wikipedia.org/wiki/Baba_O%27Riley)
- [Cherry Audio — módulo "Baba O'Lowrey"](https://store.cherryaudio.com/modules/baba-olowrey)
- [Mixonline — Classic Tracks: The Who's "Baba O'Riley"](https://www.mixonline.com/recording/classic-tracks/the-whos-baba-oriley-classic-tracks)

---

## 🔊 Como funciona o som

Nenhum sample: cada nota é sintetizada por **FM (modulação de frequência)**, a mesma técnica que consagrou os timbres de piano elétrico dos anos 80 — aqui calibrada para o Rhodes de 1969, mais escuro e encorpado.

### A voz de cada nota

```
mod (senoide, razão 1:1) ──▶ índice FM ──▶ frequência do carrier
                                                  │
carrier (senoide na fundamental) ─────────────────┤
                                                  ▼
tine (senoide 4×/6× a fundamental,          filtro lowpass
ataque metálico de ~50 ms) ────────────▶  (abre com a dinâmica)
                                                  │
                                                  ▼
                                         envelope de amplitude
                                        (ataque 4 ms, decay longo,
                                         mais longo nos graves)
```

- O **índice de modulação** cresce com o quadrado da dinâmica (`vel²`) e com o controle *Timbre*: tocando fraco o som é quase uma senoide pura; tocando forte aparece o "bark" metálico característico.
- O oscilador **tine** simula a batida do martelo no tine metálico — um transiente brilhante que some em milissegundos.
- O **filtro lowpass** abre conforme a dinâmica (1,4 kHz → 6 kHz), escurecendo as notas suaves.
- O **decay** é mais longo nos graves e mais curto nos agudos, como no instrumento real.

### A cadeia de efeitos (o "gabinete Suitcase")

```
vozes ──▶ master ──┬─▶ dry ──────────────────┐
                   ├─▶ chorus (2 delays       ├─▶ vibrato estéreo ──▶ compressor ──▶ saída
                   │   modulados em oposição) │    (auto-pan L↔R
                   └─▶ reverb (convolução,    │     por LFO em
                       IR sintética ~1,9 s) ──┘     contrafase)
```

- **Vibrato estéreo:** um LFO senoidal modula o ganho dos canais L e R em **fases opostas** — é o famoso auto-pan do amplificador Suitcase, que faz o som "passear" entre os dois alto-falantes.
- **Chorus:** duas linhas de delay (17 ms e 24 ms) moduladas em contrafase por um LFO de 0,7 Hz.
- **Reverb:** convolução com uma resposta impulsiva **gerada em código** (ruído com decaimento exponencial, ~1,9 s), com caráter de sala pequena/spring.
- **Compressor** final cola tudo e protege contra clipping.

### Interface

O visual reproduz o Suitcase de 1965–69 inteiramente em **CSS** (sem imagens): a tampa *sparkle-top* prateada, o trilho de controles com o logo em script, o feltro verde sobre as teclas e o *grille cloth* do gabinete. O teclado é desenhado dinamicamente em JavaScript e se adapta à largura da tela (de 8 a 22 teclas brancas visíveis), reconstruindo-se ao girar o aparelho.

---

## 📁 Estrutura do projeto

```
fender_rhodes/
├── index.html   ← todo o app: HTML + CSS + JavaScript (zero dependências)
└── README.md
```

---

## 🧭 Compatibilidade

| Recurso | Chrome/Edge | Safari (iOS/macOS) | Firefox |
|---|---|---|---|
| Síntese e efeitos | ✅ | ✅ | ✅ |
| Multitoque + dinâmica | ✅ | ✅ | ✅ |
| Gravação (● Rec) | ✅ `.webm` | ✅ `.m4a` (iOS 14.3+) | ✅ `.webm` |
| Teclado MIDI | ✅ | ❌ (sem Web MIDI) | ⚠️ atrás de permissão |
| Tela cheia | ✅ | ⚠️ (limitado no iPhone) | ✅ |

---

## 🗺️ Ideias futuras

- [ ] **PWA instalável** (manifest + service worker) para funcionar offline e ter ícone na tela inicial;
- [ ] **Pitch bend / modulation wheel** via MIDI;
- [ ] **Metrônomo e loops de bateria** para praticar por cima;
- [ ] **Modo "aprenda a tocar"**: teclas iluminadas guiando progressões clássicas de soul/gospel;
- [ ] **Gravação MIDI** (além do áudio) com exportação `.mid`;
- [x] **Outros instrumentos**: ~~módulo Lowrey ’68 (Baba O'Riley)~~ — feito! Próximos: Rhodes Mark II "brilhante", Wurlitzer 200A, piano CP-70;
- [ ] **Knobs giratórios** no lugar dos sliders, fiéis ao painel original.

Contribuições e sugestões são bem-vindas — abra uma *issue*!
