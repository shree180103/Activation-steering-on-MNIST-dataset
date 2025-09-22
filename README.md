# Activation-steering-on-MNIST-dataset

Activation steering is a technique used in interpretability and model editing where you directly manipulate a neural network’s internal activations (the hidden states or feature representations inside the model) to change its behavior in a controlled way.

<img width="669" height="445" alt="image" src="https://github.com/user-attachments/assets/d8fa88b4-723c-46ab-ba75-910f4f2968c5" />

The steps for actiavtion steering:

- Decide on a layer l and transformer module ϕ to apply the activation steering to.
- Define a steering vector v. In the simplest case we just take the difference of the activations
- Add the vector to the activation during the forward pass, i.e ϕ(l)(steered)=ϕ(l)+v
- you can also normalize it or multiply it with some scalar c to control the strength of the activation addition like ϕ(l)(steered)=ϕ(l)+c.v


# why activations and not features ?

<img width="724" height="724" alt="image" src="https://github.com/user-attachments/assets/e0f9acd7-9c6d-4107-a299-d09f7f64f613" />
