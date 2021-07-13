# MultiLayerPercepteon
MultiLayerPercepteon
MultilayerPerceptron


MultiLayerPerceptron

Refer to my blog post.

This is a small neural network "library" that's intended for educational purposes. I wanted to develop something that is easily understood and very readable, so this library is far from optimized or efficient.

Installing
You can install this via npm

npm install multilayer-perceptron-js
Creating a neural network
const { MultiLayerPerceptron, ActivationFunction } = require('multilayer-perceptron-js');

let sigmoid = new ActivationFunction(
  x => 1 / (1 + Math.exp(-x)), // sigmoid
  y => y * (1 - y) // derivative of sigmoid
);

let mlp = new MultiLayerPerceptron({inputDimension: 2})
  .addLayer({nodes: 2, activation: sigmoid})
  .addLayer({nodes: 2, activation: sigmoid})
  .addLayer({nodes: 1, activation: sigmoid})
  .randomizeWeights();
Training a neural network
mlp.train({
  trainData: dataset.inputs,
  trainLabels: dataset.targets,
  validationData: validationDataset.inputs,
  validationLabels: validationDataset.targets,
  numEpochs: numberOfEpochs,
  learningRate: learningRate,
  verbose: true
});
Where dataset.inputs, dataset.targets, validationDataset.inputs, and validationDataset.targets are arrays. If you were solving the XOR problem, dataset might look like this (such that the indexes of each array line up):

let dataset = {
  inputs: [
    [0, 0],
    [0, 1],
    [1, 0],
    [1, 1]
  ],
  targets: [
    [0],
    [1],
    [1],
    [0]
  ]
};
You'll see something like this while training if verbose is true:

Epoch 10; Error 1.9860974914165456
...
Epoch 100; Error 0.76609707552872275
...
Epoch 1000; Error 0.166096867598113085
...
Epoch 5000; Error 0.036096035894226
...
Epoch 10000; Error 0.03609582796927307
...
Making predictions
To make a prediction, just call predict on the MultiLayerPerceptron object. You'll receive the predicted guess and the state of the neural network. If you have a model that solved the XOR problem, making predictions would look like this:

console.log(mlp.predict([0, 0]).prediction); // [0.02039202706589195]
console.log(mlp.predict([0, 1]).prediction); // [0.9848467111547554]
console.log(mlp.predict([1, 0]).prediction); // [0.9850631024542238]
console.log(mlp.predict([1, 1]).prediction); // [0.013544196415469074]
Acknowledgements
Much of the implementation is inspired from The Coding Train's videos on neural networks, and the 3Blue1Brown videos on neural networks helped me understand what I was doing a lot better.
