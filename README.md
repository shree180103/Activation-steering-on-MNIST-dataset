# Activation-steering-on-MNIST-dataset

Activation steering is a technique used in interpretability and model editing where you directly manipulate a neural network’s internal activations (the hidden states or feature representations inside the model) to change its behavior in a controlled way.

<img width="669" height="445" alt="image" src="https://github.com/user-attachments/assets/d8fa88b4-723c-46ab-ba75-910f4f2968c5" />

The steps for actiavtion steering:

- Decide on a layer l of the model with actiations ϕ to apply the activation steering to.
- Define a steering vector v. In the simplest case we just take the difference of the activations. This can be self or cross model activations.
- Add the vector to the activation during the forward pass, i.e ϕ(l)(steered)=ϕ(l)+v
- you can also normalize it or multiply it with some scalar c to control the strength of the activation addition like ϕ(l)(steered)=ϕ(l)+c.v


# why activations and not features ?

<img width="724" height="724" alt="image" src="https://github.com/user-attachments/assets/e0f9acd7-9c6d-4107-a299-d09f7f64f613" />



One neuron may encode multiple features. Thus, a neural network can represent more features than it has neurons. This implies that the feature space is higher-dimensional than the activation space. Each feature in this higher-dimensional space corresponds to a direction in the activation space. Therefore, we can treat activations as vectors that represent feature directions. By modifying these activations (and hence the directions), we can change the features represented within the neural network.

# Experiments

1. Cross Activation steering
Here we take data A and data B which is trained on model A and model B respectively (model A and B have the same design). Then we compute mean of actiavtions at each layer l for both models. after that we compute the differece between the activations therefore we get steering vectors at each layer l is. Finally, we add the steered vectors to the initial activations to get our steered model.


   
3. Self activation steering
4. Multi steer activation steering
5. self activation Steering with capability retention
   
