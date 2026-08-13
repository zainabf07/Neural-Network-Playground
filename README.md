# 🧠 Neural Network Playground

An interactive tool to visualizer a small neural network in your browser, using real backpropagation. Inspired by [playground.tensorflow.org](https://playground.tensorflow.org).

![Vanilla JS](https://img.shields.io/badge/vanilla-JS-f7df1e?logo=javascript&logoColor=black)
![No dependencies](https://img.shields.io/badge/dependencies-none-2f6fed)
![No build step](https://img.shields.io/badge/build%20step-none-ef7d3b)
![License](https://img.shields.io/badge/license-do%20whatever%20you%20want-lightgrey)

## 🎥 Demo

https://github.com/user-attachments/assets/f50c5524-1fab-43c4-a394-7b9f05d5190a

## ✨ Features

- ⚡ Real gradient descent training, not a scripted animation
- 🎯 4 datasets (Circle, XOR, Gaussian, Spiral) with adjustable noise
- 🧩 Adjustable hidden layers (1-5) and neurons per layer (2-8)
- 🔀 4 activation functions and 5 learning rates
- 📉 Live decision boundary, loss curve, and test accuracy
- 🖱️ Hover neurons or connections to inspect activations, biases, and weights

## 🚀 Usage

Open `neural-network-playground.html` in your browser. No setup required.

Pick a dataset, hit **▶ Run**, and watch the boundary fit the points. Use **Step** to advance one batch at a time, and **Reset** to reinitialize weights without changing the dataset.

## 🔬 How it works

The network is fully connected: `2 inputs → hidden layers → 1 output`. Loss is mean squared error, trained via backprop with mini-batches of 10. 🟠 Orange means positive (label, weight, or activation); 🔵 blue means negative.

## 📄 License

Do whatever you want with this code.
