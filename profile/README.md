<div align="center">

# [ U N B R A N D E D ]

**R&D lab @ KAFEIN**

Local-first inference, autonomous agents, and generative systems — built, run, and measured on our own hardware.

`not client work` · `not a brand studio`

</div>

---

## What this is

UNBRANDED is where KAFEIN's research lives. We build the infrastructure first — a local inference fleet, a GPU control plane, decision layers, agent loops — and then we run it until it proves itself or it doesn't.

Some of it ships. Some of it stays private. The public repos are the parts that can stand on their own: no internal services, no private dependencies, no hidden context.

**Private by default. Public when it can stand alone.**

## How we work

**1. Local first.**
Inference runs on hardware we own. Client data does not leave it. Cloud is a tool for burst work, not a default.

**2. Measure, then believe.**
Every claim has a date and a source. Local benchmarks are filters, not proof. The live system is the truth; when a document disagrees with it, the document gets fixed in the same commit.

**3. Standalone by design.**
No repo couples to another. Public projects build, test, and document themselves from their own tree. If it needs our internal topology to work, it is not ready to be public.

**4. Structure beats tuning.**
We look for the structural lever before touching a parameter — the deck, not the agent; the instrument, not the preset. Most of the gain is architectural.

---

## Public work

### H E L M

<p align="center">
  <a href="https://youtu.be/MxisBKxoDSQ" title="Watch the Helm demo">
    <img src="https://raw.githubusercontent.com/U-N-B-R-A-N-D-E-D/comfyui-helm/main/docs/images/demo.jpg" alt="Helm — same prompt, same seed, one number changed" width="100%"/>
  </a>
  <br/>
  <sub><b>Same prompt. Same seed. One number changed.</b> · <a href="https://youtu.be/MxisBKxoDSQ">47-second demo</a></sub>
</p>

**A prompt is a switch, not a dial.**

Change one word and the whole frame changes. Mix two prompts and the scene flips instead of blending. Helm takes a different route: it reads a direction the model already knows — `axis = mean_pos − mean_neg` from two contrast passes — saves it as a **~22 KB `.safetensors` file**, and injects it during sampling with a single scalar.

No training. No weight modification. The same axis works across portraits, landscapes, night exteriors, and interiors.

<table>
  <tr>
    <td width="50%" align="center"><img src="https://raw.githubusercontent.com/U-N-B-R-A-N-D-E-D/comfyui-helm/main/examples/hero_strength_0.00.png" alt="Baseline, strength 0.00"/><br/><sub><b>strength = 0.00</b> — baseline</sub></td>
    <td width="50%" align="center"><img src="https://raw.githubusercontent.com/U-N-B-R-A-N-D-E-D/comfyui-helm/main/examples/hero_strength_0.25.png" alt="Steered, strength 0.25"/><br/><sub><b>strength = 0.25</b> — same prompt, same seed</sub></td>
  </tr>
</table>

<p align="center">
  <img src="https://raw.githubusercontent.com/U-N-B-R-A-N-D-E-D/comfyui-helm/main/docs/images/one_axis_any_scene.png" alt="One axis applied across four scenes" width="100%"/>
  <br/>
  <sub>One axis, any scene. Capture a direction once and dial it into a portrait, a forest, a city, or an interior.</sub>
</p>

- **Byte-exact zero point** — at `strength = 0.0`, Helm contributes nothing to the sampled state.
- **Stackable and clamped** — chain axes (`mood` → `density`) with normalized `0.0–1.0` dials and `safe_max` limits.
- **Built for real DiT runtimes** — MiniMax H3 memory-compiler bypass, dual-stream tuple safety, interactive ComfyUI and headless Comfy SDK.
- **78 documented axes · 75 tests · MIT**

<p align="center">
  <img src="https://raw.githubusercontent.com/U-N-B-R-A-N-D-E-D/comfyui-helm/main/docs/images/ui_in_comfyui.png" alt="Helm nodes chained in ComfyUI" width="100%"/>
</p>

<p align="center">
  <b><a href="https://github.com/U-N-B-R-A-N-D-E-D/comfyui-helm">Repository</a></b> ·
  <b><a href="https://youtu.be/MxisBKxoDSQ">Demo</a></b> ·
  <b><a href="https://github.com/U-N-B-R-A-N-D-E-D/comfyui-helm/blob/main/docs/EXPERIMENTS.md">Experiments</a></b> ·
  <b><a href="https://github.com/U-N-B-R-A-N-D-E-D/comfyui-helm/blob/main/docs/ROADMAP.md">Roadmap</a></b>
</p>

---

### OtaClaw

<p align="center">
  <img src="https://raw.githubusercontent.com/U-N-B-R-A-N-D-E-D/otaclaw/main/src/assets/sprites/otacon_sprite.png_0004_Sprite-5.png" alt="OtaClaw idle sprite" width="112"/>
</p>

**Give any agent a face.**

Every inference stack emits a stream of events. OtaClaw listens to `agent.*` and `gateway.*` WebSocket events and turns them into a pixel-art character that thinks, processes, succeeds, gets surprised, and fails — with the right animation for each state.

It runs as a kiosk on a Raspberry Pi, an always-on desktop dashboard, or an iframe in any UI. OpenClaw is a first-class integration; any custom bridge that speaks the protocol works the same way.

- **Two modes** — public gateway or fully local stack.
- **MIT · CI on every push · no cloud dependency.**
- Node.js 16+ · WebSocket · Raspberry Pi / kiosk / desktop

<p align="center">
  <b><a href="https://github.com/U-N-B-R-A-N-D-E-D/otaclaw">Repository</a></b> ·
  <b><a href="https://github.com/U-N-B-R-A-N-D-E-D/otaclaw/blob/main/QUICKSTART.md">Quickstart</a></b> ·
  <b><a href="https://github.com/U-N-B-R-A-N-D-E-D/otaclaw/blob/main/docs/WEBSOCKET-PROTOCOL.md">WebSocket protocol</a></b>
</p>

---

### comfy-api-graphs

**Validate before you queue.**

ComfyUI's node editor is the right place to design a graph. The exported **API-format JSON** is what automation actually touches — batch runs, seed sweeps, prompt swaps, CI checks. Editing that JSON by hand is where GPU hours go to die.

This is the small, boring layer in between: load the export, mutate specific inputs, check links and schema offline, then write it back or POST it. Not a runtime, not a UI-to-API converter, not a worker stack.

```python
from comfy_api_graphs import ComfyWorkflow, validate_against_object_info, load_object_info

wf = ComfyWorkflow.from_api_json("my_graph_api.json")
wf.set_input_by_class_type("CLIPTextEncode", "text", "a new prompt")
wf.randomize_seeds()

report = validate_against_object_info(wf, load_object_info("object_info.json"))
assert report["valid"], report["errors"]
```

- **Zero runtime dependencies** · Python 3.9+
- **142 tests** · link checks · `/object_info` schema validation · orphan and duplicate-seed detection
- CLI: `validate` · `seeds` · `show` (Mermaid) · `diff`
- **MIT**

<p align="center">
  <b><a href="https://github.com/U-N-B-R-A-N-D-E-D/comfy-api-graphs">Repository</a></b> ·
  <b><a href="https://github.com/U-N-B-R-A-N-D-E-D/comfy-api-graphs/blob/main/docs">Docs</a></b>
</p>

---

### Latent-Resonator

<blockquote>
  <p><i>"We do not create music; we organize sound, and in the process, we allow the machine to reveal its own acoustic unconscious."</i></p>
</blockquote>

**The model's bias is the instrument.**

Latent Resonator captures audio, runs it through ACE-Step, feeds the result back in, and repeats. Each pass drifts a little further from the source, and the model's own timbral tendencies — metallic, granular, smeared — accumulate into the take you play.

It is an asynchronous neural texture generator, not a real-time effect: inference takes seconds and never runs in the audio path. What is real-time is Bespoke Synth's DSP, where you audition and perform the output.

```
S(i+1) = ACE( S(i) + N(mu, sigma), P, gamma )
```

- Built as a C++ module inside a Bespoke Synth fork, with a separate Python bridge.
- Verified only on Apple Silicon macOS; ACE-Step weights (~16 GB) are never bundled.
- **MIT** · research prototype, honest about its limits

<p align="center">
  <b><a href="https://github.com/U-N-B-R-A-N-D-E-D/Latent-Resonator">Repository</a></b> ·
  <b><a href="https://github.com/U-N-B-R-A-N-D-E-D/Latent-Resonator/blob/main/docs/whitepaper.md">Whitepaper</a></b>
</p>

---

## The lab

Most of the work is private because it runs production systems, moves money, or handles client data. The families:

| Family | What runs there |
|---|---|
| **HAL** | Local-first inference fleet: named model tiers over a GPU brain and a pool of Mac mini workers. OpenAI-compatible, no cloud inference, client data stays on our hardware. |
| **KCA Studio** | Demand-driven GPU control plane and image pipeline for generative media — start on demand, stop on idle, account for every job. |
| **HAL Lab** | Competition research with dated result ledgers, reusable measurement tooling, and a bias for structural levers over parameter tuning. |
| **Punto Justo** | Legal lead intake with unauthorized-practice-of-law guardrails and CRM sync. |
| **StockAgent** | Autonomous multi-agent trading system on dedicated hardware, with bracket orders, position monitors, and drawdown protection. |
| **Creative Lab** | Daily generative photojournalism and forensic satellite cartography of mineral extraction. |
| **The Aleph** | A personal brain, media library, and agent stack joined by typed one-token decision heads. |

## Glossary

**HAL** — the local inference platform, and the name of its universe. Runs the models behind our products.
**KCA** — KAFEIN's full assistant system, whatever the touchpoint.
**Moka** — the WhatsApp and Meet agent inside KCA.
**HAL Lab** — the research wing: competitions as a source of reusable signals for client work.

---

<div align="center">

**[kafein.agency](https://www.kafein.agency/)** · **unbranded@kafein.agency**

<sub>Public projects are MIT unless stated otherwise. Everything else is proprietary.</sub>

</div>

<details>
<summary><b>Leer en español</b></summary>

<br>

## Qué es esto

UNBRANDED es donde vive la investigación de KAFEIN. Primero construimos la infraestructura —una flota de inferencia local, un plano de control de GPU, capas de decisión, loops de agentes— y después la ponemos a correr hasta que se prueba o no se prueba.

Parte se publica. Parte se queda privada. Los repos públicos son las piezas que pueden sostenerse solas: sin servicios internos, sin dependencias privadas, sin contexto escondido.

**Privado por defecto. Público cuando puede sostenerse solo.**

## Cómo trabajamos

**1. Local primero.** La inferencia corre en hardware propio. Los datos de clientes no salen de ahí. La nube es una herramienta para trabajo puntual, no el default.

**2. Medir, después creer.** Cada afirmación tiene fecha y fuente. Los benchmarks locales son filtros, no pruebas. El sistema vivo es la verdad; si un documento lo contradice, se corrige en el mismo commit.

**3. Independiente por diseño.** Ningún repo se acopla a otro. Los proyectos públicos se construyen, se prueban y se documentan desde su propio árbol. Si necesita nuestra topología interna para funcionar, no está listo para ser público.

**4. La estructura gana al tuning.** Buscamos la palanca estructural antes de tocar un parámetro: el deck, no el agente; el instrumento, no el preset. Casi toda la ganancia es arquitectónica.

## Trabajo público

**HELM — un prompt es un interruptor, no un dial.** Cambiar una palabra cambia todo el cuadro. Helm lee una dirección que el modelo ya conoce —`axis = mean_pos − mean_neg` de dos pasadas de contraste— la guarda en un `.safetensors` de **~22 KB** y la inyecta durante el sampling con un solo escalar. Sin entrenamiento, sin tocar pesos. El mismo eje funciona en retratos, paisajes, exteriores nocturnos e interiores. Punto cero exacto en `strength = 0.0`; ejes apilables y limitados; 78 ejes documentados, 75 tests, MIT.

**OtaClaw — dale cara a cualquier agente.** Escucha los eventos `agent.*` y `gateway.*` por WebSocket y los convierte en un personaje pixel-art que piensa, procesa, acierta, se sorprende y falla. Corre en una Raspberry Pi, un kiosco, un dashboard o un iframe. Dos modos, MIT, CI en cada push.

**comfy-api-graphs — valida antes de encolar.** El JSON API-format de ComfyUI es lo que toca la automatización. Esta capa lo carga, lo muta y lo valida offline, sin dependencias de runtime. 142 tests, CLI con `validate`, `seeds`, `show` y `diff`, MIT.

**Latent-Resonator — el sesgo del modelo es el instrumento.** Captura audio, lo pasa por ACE-Step, realimenta la salida y repite. Cada pasada se aleja un poco más de la fuente y acumula las tendencias tímbricas del modelo. No es un efecto en tiempo real: la inferencia tarda segundos y nunca corre en el path de audio. Módulo C++ dentro de un fork de Bespoke Synth, verificado solo en Apple Silicon, MIT.

## El laboratorio

La mayor parte del trabajo es privada porque corre sistemas en producción, mueve dinero o maneja datos de clientes: **HAL** (flota de inferencia local), **KCA Studio** (control plane de GPU y pipeline generativo), **HAL Lab** (investigación de competencias con ledgers fechados), **Punto Justo** (intake legal con guardrails), **StockAgent** (trading autónomo), **Creative Lab** (foto-periodismo generativo y cartografía satelital forense) y **The Aleph** (cerebro personal, biblioteca y agentes con decisiones tipadas).

## Glosario

**HAL** — la plataforma de inferencia local y el nombre de su universo.
**KCA** — el sistema completo de asistencia de KAFEIN, sin importar el punto de contacto.
**Moka** — el agente de WhatsApp y Meet dentro de KCA.
**HAL Lab** — el ala de investigación: competencias como fuente de señales reutilizables.

---

**[kafein.agency](https://www.kafein.agency/)** · **unbranded@kafein.agency**

<sub>Los proyectos públicos son MIT salvo que se indique lo contrario. El resto es propietario.</sub>

</details>
