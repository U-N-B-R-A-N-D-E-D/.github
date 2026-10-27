<div align="center">

<img src="https://raw.githubusercontent.com/U-N-B-R-A-N-D-E-D/.github/main/profile/assets/unbranded.png" width="76" alt="[ U N B R A N D E D ]"/>

<h1><code>[ U N B R A N D E D ]</code></h1>

<p><code>The R&amp;D lab of KAFEIN</code></p>

Local inference, generative media, and agent systems — built and run in production.

</div>

<p align="center">
  <a href="#selected-work">Selected work</a> ·
  <a href="#capabilities">Capabilities</a> ·
  <a href="#contact">Contact</a>
</p>

---

## Selected work

### Helm

<p align="center">
  <a href="https://youtu.be/MxisBKxoDSQ" title="Watch the Helm demo">
    <img src="https://raw.githubusercontent.com/U-N-B-R-A-N-D-E-D/comfyui-helm/main/docs/images/demo.jpg" alt="Helm — same prompt, same seed, one number changed" width="100%"/>
  </a>
  <br/>
  <sub><b>Same prompt. Same seed. One number changed.</b> · <a href="https://youtu.be/MxisBKxoDSQ">47-second demo</a></sub>
</p>

**A prompt is a switch, not a dial.**

Helm reads a direction the model already knows, captured from two contrast passes, and injects it during sampling with a single scalar. The axis is a ~22 KB `.safetensors` file. No training. No weight modification.

<table>
  <tr>
    <td width="50%" align="center"><img src="https://raw.githubusercontent.com/U-N-B-R-A-N-D-E-D/comfyui-helm/main/examples/hero_strength_0.00.png" alt="Baseline, strength 0.00"/><br/><sub><b>strength = 0.00</b> — baseline</sub></td>
    <td width="50%" align="center"><img src="https://raw.githubusercontent.com/U-N-B-R-A-N-D-E-D/comfyui-helm/main/examples/hero_strength_0.25.png" alt="Steered, strength 0.25"/><br/><sub><b>strength = 0.25</b> — same prompt, same seed</sub></td>
  </tr>
</table>

<p align="center">
  <img src="https://raw.githubusercontent.com/U-N-B-R-A-N-D-E-D/comfyui-helm/main/docs/images/one_axis_any_scene.png" alt="One axis applied across four scenes" width="100%"/>
  <br/>
  <sub>One axis, any scene.</sub>
</p>

Byte-exact zero point · stackable axes · 78 documented axes · 75 tests · MIT

<p align="center">
  <b><a href="https://github.com/U-N-B-R-A-N-D-E-D/comfyui-helm">Repository</a></b> ·
  <b><a href="https://youtu.be/MxisBKxoDSQ">Demo</a></b> ·
  <b><a href="https://github.com/U-N-B-R-A-N-D-E-D/comfyui-helm/blob/main/docs/EXPERIMENTS.md">Experiments</a></b>
</p>

---

### OtaClaw

<p align="center">
  <img src="https://raw.githubusercontent.com/U-N-B-R-A-N-D-E-D/otaclaw/main/src/assets/sprites/otacon_sprite.png_0004_Sprite-5.png" alt="OtaClaw idle sprite" width="96"/>
</p>

**Give any agent a face.** A pixel-art companion that reacts to `agent.*` and `gateway.*` WebSocket events. Runs on a Raspberry Pi, a kiosk, a desktop dashboard, or an iframe.

Node.js · WebSocket · MIT

<p align="center">
  <b><a href="https://github.com/U-N-B-R-A-N-D-E-D/otaclaw">Repository</a></b> ·
  <b><a href="https://github.com/U-N-B-R-A-N-D-E-D/otaclaw/blob/main/QUICKSTART.md">Quickstart</a></b> ·
  <b><a href="https://github.com/U-N-B-R-A-N-D-E-D/otaclaw/blob/main/docs/WEBSOCKET-PROTOCOL.md">Protocol</a></b>
</p>

---

### comfy-api-graphs

**Validate before you queue.** A zero-dependency Python helper to load, mutate, and validate ComfyUI API-format graphs offline — links, schema, seeds — before a bad graph burns GPU time.

142 tests · CLI: `validate` · `seeds` · `show` · `diff` · MIT

<p align="center">
  <b><a href="https://github.com/U-N-B-R-A-N-D-E-D/comfy-api-graphs">Repository</a></b> ·
  <b><a href="https://github.com/U-N-B-R-A-N-D-E-D/comfy-api-graphs/tree/main/docs">Docs</a></b>
</p>

---

### Latent-Resonator

**A recursive neural resampler.** Audio runs through ACE-Step, the output feeds back in, and repeats. The model's timbral bias accumulates into the take. A C++ module inside a Bespoke Synth fork, with a separate Python bridge.

Python · C++ · ACE-Step · MIT

<p align="center">
  <b><a href="https://github.com/U-N-B-R-A-N-D-E-D/Latent-Resonator">Repository</a></b> ·
  <b><a href="https://github.com/U-N-B-R-A-N-D-E-D/Latent-Resonator/blob/main/docs/whitepaper.md">Whitepaper</a></b>
</p>

---

## Capabilities

**Local inference** — model routing and serving on owned hardware.
**Generative media** — image, video, and audio pipelines in production.
**Applied research** — measurement-driven experiments, shipped as tools.

---

## Contact

**Work with KAFEIN** → [kafein.agency/contact](https://www.kafein.agency/contact)
**Collaborate** → [unbranded@kafein.agency](mailto:unbranded@kafein.agency)

<sub>Selected projects are open source. See each repository for its license.</sub>

<details>
<summary><b>Leer en español</b></summary>

<br>

<div align="center">

<p><code>El laboratorio de I+D de KAFEIN</code></p>

Inferencia local, media generativa y sistemas de agentes — construidos y operados en producción.

</div>

## Trabajo seleccionado

**Helm** — un prompt es un interruptor, no un dial. Helm lee una dirección que el modelo ya conoce, capturada de dos pasadas de contraste, y la inyecta durante el sampling con un solo escalar. El eje es un `.safetensors` de ~22 KB. Sin entrenamiento. Sin tocar pesos.

Mismo prompt, misma semilla, un número distinto. Punto cero exacto · ejes apilables · 78 ejes documentados · 75 tests · MIT.

**OtaClaw** — dale cara a cualquier agente. Un compañero pixel-art que reacciona a eventos `agent.*` y `gateway.*` por WebSocket. Corre en una Raspberry Pi, un kiosco, un dashboard o un iframe.

**comfy-api-graphs** — valida antes de encolar. Helper Python sin dependencias para cargar, mutar y validar grafos API-format de ComfyUI offline: links, esquema y semillas. 142 tests.

**Latent-Resonator** — un resampler neuronal recursivo. El audio pasa por ACE-Step, la salida se realimenta y se repite. El sesgo tímbrico del modelo se acumula en la toma. Módulo C++ dentro de un fork de Bespoke Synth, con un puente Python aparte.

## Capacidades

**Inferencia local** — routing y serving de modelos en hardware propio.
**Media generativa** — pipelines de imagen, video y audio en producción.
**Investigación aplicada** — experimentos medidos, convertidos en herramientas.

## Contacto

**Trabajar con KAFEIN** → [kafein.agency/contact](https://www.kafein.agency/contact)
**Colaborar** → [unbranded@kafein.agency](mailto:unbranded@kafein.agency)

<sub>Los proyectos seleccionados son open source. Consultá la licencia de cada repositorio.</sub>

</details>
