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
| **Volume** | Volume geral do instrumento |
| **Vibrato veloc.** | Velocidade do balanço estéreo (0,5–9 Hz) |
| **Vibrato intens.** | Intensidade do balanço entre os alto-falantes |
| **Timbre (bark)** | Do som suave e escuro ao ataque metálico agressivo ("bark") típico do Rhodes tocado forte |
| **Chorus** | Espessamento do som com duas linhas de delay moduladas |
| **Reverb** | Ambiência de sala pequena, com caráter de spring reverb |
| **Preset** | Aplica combinações prontas de todos os controles (veja abaixo) |
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
- [ ] **Outros voicings**: Rhodes Mark II "brilhante", Wurlitzer 200A, piano CP-70;
- [ ] **Knobs giratórios** no lugar dos sliders, fiéis ao painel original.

Contribuições e sugestões são bem-vindas — abra uma *issue*!
