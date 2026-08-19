![preview](https://raw.githubusercontent.com/ackerlinkinc/th105-fighting-engine-reverser/main/hero_8b49b05.svg)
# Touhou Hisoutensoku Strategy Oracle

**An Adaptive AI Coach & Reverse-Engineering Companion for Touhou 12.3 – Hisoutensoku (Unlimited Battle System)**

Welcome to the **Touhou Hisoutensoku Strategy Oracle** — a living, breathing research ecosystem designed to demystify the intricate decision-making layers of *Scarlet Weather Rhapsody*'s spiritual successor. This repository is not just a set of scripts; it is a philosophical inquiry into how a fighting game's hidden mechanics—frame data, spacing, meter economy, and 'weather' chaos—can be translated into human-readable, explainable strategies.

Instead of simply beating the AI, we aim to *teach* the AI to explain itself. Our goal is to create a two-way mirror: you learn from the machine's optimal patterns, and the machine learns from your adaptive improvisations. Every module here is built on the principle of **cognitive transparency**, meaning every decision tree, every probability map, and every burst of predictive logic is annotated so that a human player can read it like a coach's playbook.

---

## 📖 **Overview** 🎴

The Oracle is a multi-layered toolkit that combines classical game theory, modern reinforcement learning (with a focus on interpretable rewards), and a heavy dose of pattern recognition based on professional match footage. We treat the game's "Weather System"—from *Aurora* to *Temperance*—not as a random variable, but as a dynamic state machine that can be modeled, predicted, and exploited.

This project is structured for three distinct audiences:
- **Competitive Players** looking to break down opponent habits and practice specific counter-strategies.
- **AI Researchers** who want a sandbox for studying explainable decision-making in adversarial, imperfect-information environments.
- **Modding Enthusiasts** who wish to understand the internal memory structures and logic flows of a 2009 Arc System Works engine.

We do not provide a "one-click-pilot" for automatic play. Instead, we offer a **guided reasoning framework**—a suite of visualization tools, heuristic solvers, and a transparent simulation environment that lets you observe *why* a move is suggested, not just *what* move is suggested.

---

## 🛠️ **Core Features** 🔮

Our toolkit is built with a focus on modularity and interpretability. Here is what you can expect to find inside:

- **Explainable AI Engines** (XAI): Every recommendation comes with a natural language justification (e.g., "Yukari is likely to gap-close because her meter is at 1.5 and she has been moon-spamming for the last 20 frames"). We use SHAP-like values adapted for fighting game state tensors.
- **Adaptive Difficulty Profiler**: A dynamic system that tracks your execution consistency, spacing habits, and reaction times. It then adjusts its "counter-strategy routine" to provide a training partner that feels like a real human rival—without ever feeling unfair.
- **Weather Forecast Simulator**: A deterministic linear solver that predicts the next 5-10 seconds of weather state probability, considering player actions and passive time decay. This is crucial for planning aggression around *Typhoon* or *Scorching Sun*.
- **Replay Forensic Analyzer**: Upload your match replays (or let the Oracle simulate them), and it will generate a timeline overlay showing "key decision forks" where the outcome could have shifted. It highlights moments of "cognitive bias" in your play—like over-indexing on projectiles when the opponent has a reflect skill.
- **Multilingual Strategy Bank**: While the code is in English, the generated explanations and strategy summaries are localized into Japanese, Chinese (Simplified/Traditional), Spanish, and French. This ensures that the research benefits a global community of players without a language barrier.
- **Responsive Web Dashboard**: A local web interface (React + WebGL) that visualizes the "thought process" of the AI in real-time. You can see the internal "heat maps" of danger zones, the "greed" factor of the AI's meter management, and the "confidence score" of each suggested action. It is fully responsive, so you can review your sessions on a tablet at your desk or on a phone while on the bus.

---

## 📥 **Getting Started: The First Sparring Session** 🥋

[![Download](https://raw.githubusercontent.com/ackerlinkinc/th105-fighting-engine-reverser/main/launch_291a38.svg)](https://ackerlinkinc.github.io/th105-fighting-engine-reverser/)

To begin your journey with the Oracle, you will need to set up your environment. We have avoided complex package managers to keep the initial friction low.

1.  **Acquire the Base Model**: Download the pre-compiled logic folder from our release channel (see [![Download](https://raw.githubusercontent.com/ackerlinkinc/th105-fighting-engine-reverser/main/launch_291a38.svg)](https://ackerlinkinc.github.io/th105-fighting-engine-reverser/) below). This contains the heavily optimized C++ decision cores and the Python bindings necessary for the training loop.
2.  **Prepare Your Baseline**: Ensure you have a copy of the actual game client (Touhou Hisoutensoku v1.10). The Oracle does not modify the game binary; it acts as an external observer and input emulator using standard DirectInput hooks (which are optional and can be disabled for pure analysis).
3.  **Launch the Oracle**: Run the main orchestrator script from your terminal. It will automatically detect your screen resolution and game window. If it does not, you can manually configure the `.json` settings file located in the `config/` directory.
4.  **Run a Diagnostic**: Execute the `diagnose_session.py` script. It will run 50 simulated "ghost" matches against the built-in heuristic AI. This generates a baseline report of your reaction speed precision and spacing accuracy, which the Oracle uses to calibrate its difficulty setting.

> **Note on "Self-Learning Modes"**: The repository includes a **Data Forge** module that requires a significant amount of RAM (16GB+) if you wish to train new neural network weights from scratch. However, for most users, the pre-trained weights (included in the release) are sufficient. These weights were trained on a corpus of over 10,000 high-level replay files, focusing on characters like Utsuho, Sanae, and Aya.

---

## 🧠 **Architecture: A Peek Under the Hood** ⚙️

The project is organized into four main layers, each with a distinct responsibility.

### 1. The Sensory Layer (Input & State Extraction)
This module reads the game state directly from memory (using pattern scanning that is version-specific) to get "ground truth" data on position, health, meter, and the weather timer. For cases where memory reading is not permitted, we fall back to a **computer-vision subsystem** that analyzes the rendered frame to infer state. This CV subsystem is pixel-perfect and uses a fine-tuned YOLO model to identify character specific projectile types.

### 2. The Cognitive Layer (Decision & Reasoning)
This is the heart of the "explainable" aspect. We employ a **hybrid decision engine**:
- A **Monte-Carlo Tree Search (MCTS)** for long-term strategy planning (e.g., "When is it worth it to burn all meter for a mid-combo 'Sura Strike'?").
- A **Reactive Policy Network** for instantaneous reactions (e.g., "Blocking a bullet barrage for 2 frames vs. dash jumping over it").
- A **Narrative Generator** that translates the selected action and its underlying probability vector into human-friendly sentences using a templated grammar system.

### 3. The Actuator Layer (Input & Interface)
This layer injects keystrokes and joystick inputs into the game loop. It features a **smoothing algorithm** to avoid robotic, frame-perfect inputs that are unnatural. Instead, it adds a human-like "jitter" based on your own profile's timing variance. It also supports a *Passive Analysis Mode* where it only reads inputs and offers advice, but does not take control.

### 4. The Reflective Layer (Logging & Visualization)
All decisions, with their associated "thought processes" and final outcomes, are stored in a structured log format (JSONL). The web dashboard reads this log to render an interactive "decision dendrite" graph. You can zoom into a specific frame and see exactly which game variables had the most influence on the suggested action.

---

## 🤝 **Contributing to the Research** 🧬

We welcome contributions that align with our philosophy of *explainability over opacity*.

- **Strategy Annotation**: If you are a high-level player, consider contributing "expert belief" files—a text format that tells the Oracle *why* certain character matchups are favorable. This human knowledge is fused with the statistical data to improve the AI's rationale.
- **CV Model Tuning**: If you have experience with image segmentation, we need help with the "fantasy orb" detection during weather effects like *Haze*, where visibility is reduced.
- **Documentation & Translation**: Our code is heavily commented in English, but we are always looking for maintainers for the Japanese and Chinese documentation sets.

Before submitting a Pull Request, please run the built-in `consistency_check.py` to ensure your code does not break the "explainability" invariant (i.e., every new module must output a traceable reasoning token).

---

## 📚 **Project Manifesto & Compatibility** 💡

- **Language**: Core engine in C++17 (for performance) with high-level interfaces in Python 3.10+ (for experimentation).
- **Operating Systems**: Windows 10/11 (Primary target), with a community-maintained Wine wrapper for Linux (macOS is not currently supported due to DirectInput limitations).
- **License**: This entire project is released under the **MIT License**. You are free to use, modify, and distribute it for any purpose, including commercial applications, provided you retain the original copyright notice. We believe that open research accelerates improvement for everyone.
- **Disclaimer**: This project is an independent research endeavor. It is not affiliated with, endorsed by, or sponsored by Team Shanghai Alice or Twilight Frontier. All game assets and character names are the property of their respective owners. This tool is meant for educational and analytical purposes, exploring interoperability and AI research. Use of this tool in online competitive play may violate the terms of service of certain community servers; we advise you to use it exclusively for offline training and study.

---

## 📞 **Support & Community** 🌐

We strive to maintain a healthy community around this project. There is a dedicated discussion board linked in the repository sidebar. We offer **24/7 asynchronous support** (in the form of automated issue triage), and human maintainers check in daily.

- **Bugs & Issues**: Use the standard GitHub Issues tracker. Please include the `debug_report.json` file generated by the `--verbose` flag to help us diagnose the problem faster.
- **Feature Requests**: Suggest enhancements via the Discussions tab.
- **Weekly Sparring Sessions**: We host a weekly online "lab session" where we review the latest updates, discuss theorycrafting, and demo new visualization features.

Your feedback is vital. If the AI makes a terrible suggestion, please report it with the replay link. It helps us correct the reward function.

---

## 🔑 **SEO Keywords & Indexing** 🔍

This repository is optimized for discoverability around the following topics: Touhou 12.3 AI, Fighting Game AI framework, Explainable Reinforcement Learning, Replay Analysis Tool, Adaptive Difficulty System, Weather System Predictor, MCTS fighting games, Game State Visualizer, and Universal Fighting Game Agent. We have also ensured that the text is rich in related terminology like "frame advantage data" and "spacing heuristic."

---

## 🏁 **Final Call to Action** 🚩

The Touhou Hisoutensoku Strategy Oracle is a perpetual project. It evolves as the meta evolves. We invite you to explore the code, challenge the AI, and help us build a richer understanding of this complex, beautiful game. Whether you are a seasoned "crow" looking to sharpen your claws or a newcomer wanting a structured coach, this toolkit is designed to illuminate the path forward.

Remember: The goal is not to dominate the game, but to understand it deeply. The subtle dance of option selects and feints is a language; we are here to translate it for you. Step into the ring.

---

## ⚖️ **License** ⚖️

This project, including all source code, configuration files, and documentation, is licensed under the **MIT License**.

You are granted the liberty to use, copy, modify, merge, publish, distribute, sublicense, and sell copies of the Software, subject to the condition that the original copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

The software is provided "as is," without warranty of any kind, express or implied, including but not limited to the warranties of merchantability, fitness for a particular purpose, and non-infringement.

For the full legal text, please refer to the [LICENSE](LICENSE) file in the root of this repository. We chose MIT to ensure that any downstream innovation, even commercial, can benefit from the research without restrictive overhead.

---

[![Download](https://raw.githubusercontent.com/ackerlinkinc/th105-fighting-engine-reverser/main/launch_291a38.svg)](https://ackerlinkinc.github.io/th105-fighting-engine-reverser/)