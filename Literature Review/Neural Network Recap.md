## Neuron
- Weighted sum: `z = Wx + b`
- Activation: `a = f(z)`
- Weights/biases are the parameters the network learns.

## Forward Pass
- Input → weighted sum → activation → next layer → output
- Compute prediction `ŷ`, then calculate loss `L(ŷ, y)`.

## Loss
- Measures how wrong the prediction is.
- Training goal: minimize `L`.

## Derivatives
- `∂L/∂w` = how much the loss changes when weight `w` changes.
- Positive derivative → increasing `w` increases loss → decrease `w`.
- Negative derivative → increasing `w` decreases loss → increase `w`.

## Chain Rule
- Neural networks are compositions of functions.
- Derivatives propagate through each function:
  
  `∂L/∂w = (∂L/∂a)(∂a/∂z)(∂z/∂w)`

- Think: "How does changing `w` affect the loss?"

## Backpropagation
- Forward pass → calculate prediction + loss.
- Backward pass → use chain rule to calculate gradients.
- Computes gradients for all weights efficiently.

## Gradient Descent
- Update parameters opposite the gradient:
  
  `w_new = w_old - η(∂L/∂w)`

- `η` = learning rate.
- Gradient = direction of greatest increase in loss.
- Negative gradient = direction of greatest decrease.

## Big Picture
`Input → Neural Network → Prediction → Loss`
  
`Loss → Backpropagation → Gradients → Gradient Descent → Updated Weights`