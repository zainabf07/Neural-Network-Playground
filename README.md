# Neural Network Playground

An interactive tool to train a small neural network in your browser, using real backpropagation. Inspired by [playground.tensorflow.org](https://playground.tensorflow.org).

## Demo

<!-- Record a short screen capture and drag it into a GitHub issue/PR/discussion (even a draft) — GitHub hosts it and gives you a link like the one below. Paste that link here. -->
https://github.com/user-attachments/assets/YOUR-VIDEO-ID-HERE

## Features

- Real gradient descent training, not a scripted animation
- 4 datasets (Circle, XOR, Gaussian, Spiral) with adjustable noise
- Adjustable hidden layers (1-5) and neurons per layer (2-8)
- 4 activation functions and 5 learning rates
- Live decision boundary, loss curve, and test accuracy
- Hover neurons or connections to inspect activations, biases, and weights

## Usage

Open `neural-network-playground.html` in your browser. No setup required.

Pick a dataset, hit **Run**, and watch the boundary fit the points. Use **Step** to advance one batch at a time, and **Reset** to reinitialize weights without changing the dataset.

## How it works

The network is fully connected: `2 inputs → hidden layers → 1 output`. Loss is mean squared error, trained via backprop with mini-batches of 10. Orange means positive (label, weight, or activation); blue means negative.

## License

Do whatever you want with this code.
