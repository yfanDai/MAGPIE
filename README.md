<p align="center">
  <img src="assets/Logo.png" width="620" alt="MAGPIE: Agentic Multi-Reference Image Generation via Executable Scene Construction" />
</p>

<div align="center">
<p>
  <img src="https://img.shields.io/badge/arXiv-Coming%20Soon-red?style=badge&amp;logo=arXiv" alt="arXiv: coming soon" height="25" />
  <img src="https://img.shields.io/badge/%F0%9F%A4%97%20Paper-Coming%20Soon-blue" alt="Hugging Face Daily Papers: coming soon" height="25" />
  <img src="https://img.shields.io/badge/%F0%9F%A4%97%20Dataset-MAGPIE--Instruct--3K%20%7C%20Coming%20Soon-blue" alt="MAGPIE-Instruct-3K: coming soon" height="25" />
  <a href="https://github.com/yfanDai/MAGPIE"><img src="https://img.shields.io/github/stars/yfanDai/MAGPIE?style=social" alt="GitHub Stars" height="25" /></a>
</p>
</div>

## 🔥 News

- **[2026.11.24]** We initialize the MAGPIE repository with the project overview, visual assets, and release roadmap. Stay tuned for the code and dataset release!

## 🎯 Todo List

Project release status:

- [x] Project README and Paper
- [ ] Training and inference code
- [ ] MAGPIE-Instruct-3K dataset

## 🎬 MAGPIE

**MAGPIE: Agentic Multi-Reference Image Generation via Executable Scene Construction** is a framework for composing images from multiple visual references and a natural language instruction. MAGPIE first constructs an executable Blender scene that specifies which subjects appear, how many instances are needed, and how they are arranged and interact. A coding agent checks the geometry and rendered view, then revises the scene before image synthesis. The refined proxy guides composition, while the original references provide each subject's identity and appearance.

<p align="center">
  <img src="assets/overview.png" width="100%" alt="MAGPIE framework: reference-grounded scene planning, Blender construction, geometry and visual checks, and proxy-guided image generation" />
</p>
<p align="center">
  <i>MAGPIE Overview. The agent plans reference-associated entities, constructs an executable 3D proxy, and refines it using geometric and visual feedback. An adapted image generator follows the refined composition while preserving appearance from the bound references.</i>
</p>

## 🔍 Contributions

- **Executable scene construction for multi-reference generation.** MAGPIE instantiates compositional intent as a simplified 3D scene, making entity selection, instance counts, spatial relationships, and interactions available for inspection and correction before synthesis.
- **Geometry- and vision-guided agentic refinement.** A structured coding harness combines reusable procedural builders, explicit reference-to-entity bindings, geometric verification, and visual review to refine scene programs.
- **MAGPIE-Instruct-3K.** We construct **3,187 examples** pairing references and instructions with executable Blender programs, proxy renderings, and target images. Lightweight LoRA adaptation teaches generators to use proxy structure while preserving reference-specific appearance.
- **Improvements across two backbones and benchmarks.** On DreamOmni2, MAGPIE improves overall success by **22.25 percentage points with Qwen** and **28.21 points with FLUX**. On SconeEval, MAGPIE with FLUX achieves **9.05 overall**, the highest score among the models evaluated in the paper.

## 📑 MAGPIE-Instruct-3K

MAGPIE-Instruct-3K provides supervision for proxy-guided, reference-grounded image synthesis. Its **3,187 examples** cover five compositional tasks: **object interaction, shape alignment, pose control, spatial arrangement, and scene composition**. Each example includes reference images, an instruction, an executable Blender program, a proxy rendering, and a target image. Proxy-target pairs are filtered for entity inclusion and counts, spatial arrangements, poses and interactions, and framing and visibility.

**Dataset release: coming soon.**

<p align="center">
  <img src="assets/MAGPIE-Instruct-3K.png" width="100%" alt="MAGPIE-Instruct-3K data sources, five task categories, example pairs, and proxy-aware instruction template" />
</p>
<p align="center">
  <i>MAGPIE-Instruct-3K Overview. Data sources, task distribution, representative examples, and the proxy-aware instruction template for binding reference subjects to proxy entities and separating structural guidance from appearance.</i>
</p>

## 🚀 Quick Start

**Code and model checkpoints are coming soon.** Setup instructions, scene construction, training, and inference commands will be added with the code release.

The paper evaluates MAGPIE with **Qwen-Image-Edit-2511** and **FLUX.2-klein-base-9B**. Both generators are adapted using rank-32 LoRA for five epochs on MAGPIE-Instruct-3K. At inference, the scene-construction agent receives the reference images and instruction, with up to six proxy-refinement rounds and early stopping.

## 📊 Results Analysis

### 1️⃣ Performance Comparison on DreamOmni2

Success rates are reported as percentages; higher is better. Generation and editing each include concrete and abstract tasks. Results include proprietary models, open-weight baselines, and MAGPIE with two backbones.

<p align="center">
  <img src="assets/Table1.png" width="100%" alt="Quantitative comparison on DreamOmni2: generation and editing success rates, overall results, and gains over each backbone" />
</p>
<p align="center">
  <i>Performance comparison on DreamOmni2. Small green numbers indicate percentage-point gains over each backbone; bold follows the paper's main table.</i>
</p>

MAGPIE raises overall success from **42.01% to 64.26%** with Qwen and from **38.87% to 67.08%** with FLUX. The generation / editing / overall gains are **+21.93 / +22.44 / +22.25** percentage points for Qwen and **+31.58 / +26.34 / +28.21** for FLUX.

### 2️⃣ Performance Comparison on SconeEval

Scores range from 0 to 10; higher is better. **COM** denotes composition and **DIS** denotes distinction. The table reports the full set of subtasks and aggregate scores.

<p align="center">
  <img src="assets/Table2.png" width="100%" alt="Full SconeEval comparison including composition, cross-category and intra-category distinction, joint tasks, and aggregate scores" />
</p>
<p align="center">
  <i>Performance comparison on SconeEval, including all composition, distinction, and joint subtasks. COM and DIS denote composition and distinction; higher is better.</i>
</p>

MAGPIE improves both composition and subject distinction with either backbone. With FLUX, the overall score increases from **8.07 to 9.05**.

### 3️⃣ Effect of Proxy Refinement

<p align="center">
  <img src="assets/refinement_rounds.png" width="680" alt="DreamOmni2 generation, editing, and overall success across zero, three, and six proxy-refinement rounds" />
</p>
<p align="center">
  <i>With the adapted FLUX generator fixed, aggregate generation and editing scores improve as the refinement budget increases. Overall success rises from 53.61% without refinement to 67.08% with up to six refinement rounds.</i>
</p>

## 🔭 Visualizations

<details open>
  <summary><i>Click to collapse or expand visual examples.</i></summary>

### Qualitative Comparison on DreamOmni2

<p align="center">
  <img src="assets/dreamomni2_examples.png" width="100%" alt="DreamOmni2 qualitative comparisons for multi-subject composition, instance counting, pose transfer, and text editing" />
</p>
<p align="center">
  <i>Qualitative comparison of Qwen and FLUX with and without MAGPIE, alongside Gemini-2.5-Flash-Image, Seedream-4.0, and DreamOmni2.</i>
</p>

</details>

## 📖 Citation

The paper link and BibTeX citation will be added with the public paper release.

## 📒 License

License information will be provided with the code and dataset releases.
