<p align="center">
  <a href="https://manimater.vercel.app/">
    <img src="https://raw.githubusercontent.com/Manimater/.github/main/profile/assets/manimater-org-banner.svg" alt="Manimater: any concept, one video away" width="100%">
  </a>
</p>

<p align="center">
  <b>Describe a concept. Get a narrated, animated explainer video.</b><br>
  Manimater plans the scenes, voices them with Kokoro and animates them with <a href="https://www.manim.community/">Manim</a>. The animations come from an open source library of tested components.
</p>

<p align="center">
  <a href="https://github.com/Manimater/manimater-components/blob/main/LICENSE"><img alt="License: MIT" src="https://img.shields.io/badge/library-MIT-000000?style=flat-square&labelColor=000000"></a>
  <a href="https://github.com/Manimater/manimater-components/blob/main/CONTRIBUTING.md"><img alt="Contributions welcome" src="https://img.shields.io/badge/contributions-welcome-ffffff?style=flat-square&labelColor=000000&color=ffffff"></a>
</p>

<p align="center">
  <a href="https://manimater.vercel.app/">Try Manimater</a> ·
  <a href="https://github.com/Manimater/manimater-components">Component library</a> ·
  <a href="https://github.com/Manimater/manimater-components/blob/main/docs/WRITING_A_COMPONENT.md">Write a component</a> ·
  <a href="https://github.com/Manimater/manimater-components/blob/main/catalog.json">Catalog</a> ·
  <a href="https://github.com/Manimater/manimater-components/issues/new/choose">Request a component</a>
</p>

---

## What it does

Type a topic such as "phase lag in a series RL circuit" and Manimater returns an MP4 in about a minute: a script that opens on a hook, a voice that speaks every on-screen step, and animation timed to that voice. You see the plan before anything is rendered, and planning is free.

The part that makes it dependable is what the AI is allowed to do. It never writes code. It chooses components from a library and fills in their parameters as JSON. The renderer checks every value against the library's catalog before anything runs, so a bad plan is rejected instead of executed.

<table>
  <tr>
    <td width="33%" align="center"><img src="https://raw.githubusercontent.com/Manimater/.github/main/profile/assets/synchronous_motor.gif" alt="Synchronous motor component" width="100%"><br><sub><code>synchronous_motor</code><br>electrical</sub></td>
    <td width="33%" align="center"><img src="https://raw.githubusercontent.com/Manimater/.github/main/profile/assets/cpu_pipeline.gif" alt="CPU pipeline component" width="100%"><br><sub><code>cpu_pipeline</code><br>microelectronics</sub></td>
    <td width="33%" align="center"><img src="https://raw.githubusercontent.com/Manimater/.github/main/profile/assets/neural_network.gif" alt="Neural network component" width="100%"><br><sub><code>neural_network</code><br>machine learning</sub></td>
  </tr>
  <tr>
    <td width="33%" align="center"><img src="https://raw.githubusercontent.com/Manimater/.github/main/profile/assets/pid_response.gif" alt="PID response component" width="100%"><br><sub><code>pid_response</code><br>control systems</sub></td>
    <td width="33%" align="center"><img src="https://raw.githubusercontent.com/Manimater/.github/main/profile/assets/binary_search_tree.gif" alt="Binary search tree component" width="100%"><br><sub><code>binary_search_tree</code><br>computer science</sub></td>
    <td width="33%" align="center"><img src="https://raw.githubusercontent.com/Manimater/.github/main/profile/assets/order_book_matching.gif" alt="Order book matching component" width="100%"><br><sub><code>order_book_matching</code><br>finance</sub></td>
  </tr>
</table>

<p align="center"><sub>Six of the components, rendered from their own example parameters.</sub></p>

## The component library

[`manimater-components`](https://github.com/Manimater/manimater-components) is the open source library behind every video, released under the MIT licence. A component is a name plus parameters:

```jsonc
// No animation code. The renderer validates this against the catalog.
{ "component": "synchronous_motor", "params": { "poles": 2, "frequency_hz": 50 } }
```

| Subject | Components | Subject | Components |
|---|---:|---|---:|
| General | 14 | Control systems | 7 |
| Computer science | 14 | Microelectronics | 7 |
| Finance | 13 | Machine learning | 6 |
| Electrical | 9 | Physics | 6 |
| Power systems | 6 | Study content | 4 |
| Chemistry | 3 | Databases | 2 |

That is 91 components in the current catalog, 27 of which wrap community Manim plugins that are credited in [`THIRD_PARTY.md`](https://github.com/Manimater/manimater-components/blob/main/docs/THIRD_PARTY.md). Every component carries an example that must render, and CI dry-runs all of them against a real Manim scene.

The library also ships a [Claude skill](https://github.com/Manimater/manimater-components/tree/main/skills/manimater-components) that teaches Claude to pick components, write valid storyboards and author new components that follow the rules.

## Contribute

New components are the best way to help, and you do not have to write code.

- **Developers.** Copy [`_template.py`](https://github.com/Manimater/manimater-components/blob/main/manimate/components/community/_template.py) into `manimate/components/community/`, then follow [CONTRIBUTING.md](https://github.com/Manimater/manimater-components/blob/main/CONTRIBUTING.md) and [Writing a component](https://github.com/Manimater/manimater-components/blob/main/docs/WRITING_A_COMPONENT.md).
- **Everyone else.** Describe the animation you want to any LLM, paste the result into a form, and we turn it into a pull request. Start with [Generate with an LLM](https://github.com/Manimater/manimater-components/blob/main/docs/GENERATE_WITH_AN_LLM.md).

Every component follows the same design rules:

1. One idea per component, with a description a planner can match to a topic.
2. Computed, not drawn. Algorithms, formulas and layouts are plain functions that can be tested without Manim.
3. The finished picture fades in as a whole in 1.2 to 1.5 seconds, then the parts that carry the meaning animate.
4. Fill the time the scene is given and do not run over it.
5. Forgiving parameters. Clamp and trim instead of crashing on empty lists, huge numbers or long labels.
6. Plain labels, under 28 characters where possible.
7. Pure drawing code. No network, files, subprocesses, `eval` or `exec`.

```bash
git clone https://github.com/Manimater/manimater-components && cd manimater-components
pip install -e ".[dev]"
python -m manimate.preview --list     # every component
```

---

<p align="center">
  <a href="https://manimater.vercel.app/"><img src="https://raw.githubusercontent.com/Manimater/.github/main/profile/assets/logo.svg" alt="Manimater" width="40"></a><br>
  <sub>The hosted studio is a proprietary product. The component library is open source under the MIT licence.</sub>
</p>
