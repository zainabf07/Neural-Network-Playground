# Neural Network Playground

A minimal, in-browser tool for training a small neural network with real backpropagation and watching it learn — inspired by [playground.tensorflow.org](https://playground.tensorflow.org).

Unlike a scripted forward-pass animation, this is an actual training loop: gradients are computed via backpropagation, weights are updated with gradient descent, and everything you see (the decision boundary, the network diagram, the loss curve) is driven by the network's real, current state.

## Demo

<!--
Add a video here once you have one. GitHub renders video files dropped into
an issue/PR/discussion as a playable clip and gives you a URL like:
https://github.com/user-attachments/assets/<id>

1. Record a short screen capture of the app in action (e.g. QuickTime on
   macOS, Xbox Game Bar on Windows, or simplescreenrecorder on Linux).
2. Drag the video file into a new GitHub issue, PR, or discussion comment
   (even a draft one you don't submit) — GitHub uploads it and inserts a
   markdown line like the one below.
3. Copy that markdown line here, replacing this comment block.

https://github.com/user-attachments/assets/YOUR-VIDEO-ID-HERE
-->

Open `neural-network-playground.html` in any browser. No setup, no build step, no server, no dependencies beyond an internet connection for two Google Fonts (the app still works offline, just falls back to system fonts).

## Features

- **Real training** — actual gradient descent / backpropagation, not a scripted animation. You could disconnect the UI entirely and the underlying `NeuralNet` class would still correctly learn XOR, circles, spirals, etc.
- **4 datasets** — Circle, XOR, Gaussian, Spiral. Each dataset button shows a live mini-preview of its point distribution.
- **Adjustable noise** — controls how much random jitter is added to each dataset's points, making the classification task harder.
- **Adjustable network** — 1–5 hidden layers, 2–8 neurons per layer (uniform across layers), rebuilt live as you drag the sliders.
- **4 activation functions** — Tanh, ReLU, Sigmoid, Linear (applied to every hidden layer; the output neuron always uses Tanh since labels are ±1).
- **5 learning rates** — 0.01, 0.03, 0.1, 0.3, 1.
- **Live decision boundary** — the output panel redraws after every training step, colored by the network's prediction across a grid of points, with training points (filled circles) and held-out test points (outlined circles) overlaid on top.
- **Live loss curve** — train loss (orange) vs. test loss (blue), plotted per step, auto-scaling to the current loss range.
- **Live test accuracy** — percentage of held-out points correctly classified, updated every step.
- **Interactive network diagram** — hover any neuron to see its current activation value and bias; hover any connection to see its exact weight. Line thickness encodes weight magnitude, color encodes sign (orange = positive, blue = negative). Hovering also triggers a brief glow animation.
- **Play / Step / Reset controls** — run continuously, advance one mini-batch at a time, or reinitialize the network's weights without touching the dataset.

## Usage

1. Pick a dataset in the left sidebar.
2. Optionally tweak noise, hidden layers, neurons per layer, activation, or learning rate.
3. Click **Run** to start training continuously, or **Step** to advance one mini-batch at a time (useful for watching individual weight updates).
4. Click **Reset** to reinitialize the network's weights from scratch while keeping the current dataset and settings.
5. Hover over the network diagram at any point (paused or running) to inspect specific neuron activations, biases, and connection weights.

**What triggers a full reset vs. applying live:**

| Change | Effect |
|---|---|
| Dataset | Regenerates data, rebuilds network, clears loss history |
| Noise | Regenerates data, rebuilds network, clears loss history |
| Hidden layers / neurons per layer | Rebuilds network, clears loss history (dataset kept) |
| Activation function | Applies immediately to the existing network, no reset |
| Learning rate | Applies immediately to the next training step, no reset |

## How it works

**Data.** Each dataset generator produces 360 points with `(x1, x2)` coordinates in roughly `[-1, 1] × [-1, 1]` and a label of `+1` or `-1`. Points are shuffled and split 80/20 into training and test sets.

**Network.** A standard fully-connected feedforward network: `2 inputs → hidden layer(s) → 1 output`. Weights are initialized with a Xavier/Glorot-style scale (`√(2 / (fan_in + fan_out))` times a Gaussian sample) so gradients start out well-behaved regardless of network size. All hidden layers share the same activation function; the output neuron always uses `tanh` so its range matches the `±1` labels.

**Training.** Every step samples a mini-batch of 10 points from the (shuffled) training set, runs a forward pass to compute activations, then backpropagates the mean-squared-error loss to compute gradients for every weight and bias, and applies a standard gradient descent update scaled by the learning rate. One epoch = one full pass through the shuffled training set.

**Loss.** Mean squared error: `0.5 * (prediction - label)²`, averaged over a batch (for the training step) or over the full set (for the loss curve and readouts).

**Rendering.** The decision boundary is computed by running a forward pass on a 42×42 grid of points spanning the input domain and coloring each cell by the network's output sign and magnitude. The network diagram positions neurons in columns by layer and redraws connections/neurons every animation frame, decaying a "glow" value for whichever neuron/connection was hovered or most recently active.

## Color convention

Orange (`#ef7d3b`) always means positive — positive class label, positive weight, positive activation. Blue (`#2f6fed`) always means negative. This mapping is consistent across the dataset previews, the network diagram, the decision boundary, and the loss curve legend.

## Files

- `neural-network-playground.html` — the entire app: HTML, CSS, and JS in one self-contained file. No build step, no external JS dependencies (only two Google Fonts loaded via `<link>`).
- `README.md` — this file.

## Browser support

Works in any modern browser with Canvas 2D support (Chrome, Firefox, Safari, Edge). No mobile-specific layout is included; the three-column layout assumes a desktop-width viewport.

## Customization ideas

Since everything lives in one file, a few things are easy to change directly in the `<script>` block:

- `state.stepIntervalMs` — how fast **Run** advances (lower = faster).
- `state.batchSize` — mini-batch size (currently fixed at 10, not exposed in the UI).
- The `DATASETS` generators — tweak radii, noise scaling, or add a new dataset function and register it in `DATASET_META`.
- `--pos` / `--neg` CSS variables at the top of the `<style>` block — swap the color scheme.

## License

Do whatever you want with this code.
