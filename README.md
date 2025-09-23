# Activation-steering-on-MNIST-dataset

Activation steering is a technique used in interpretability and model editing where you directly manipulate a neural network’s internal activations (the hidden states or feature representations inside the model) to change its behavior in a controlled way.

<img width="669" height="445" alt="image" src="https://github.com/user-attachments/assets/d8fa88b4-723c-46ab-ba75-910f4f2968c5" />

The steps for actiavtion steering:

- Decide on a layer l of the model with actiations ϕ to apply the activation steering to.
- Define a steering vector v. In the simplest case we just take the difference of the activations. This can be self or cross model activations.
- Add the vector to the activation during the forward pass, i.e ϕ(l)(steered)=ϕ(l)+v
- you can also normalize it or multiply it with some scalar c to control the strength of the activation addition like ϕ(l)(steered)=ϕ(l)+c.v

In this repository I have trained a shallow neural network to classify numbers 0-7 of the MNIST dataset, and activation steered the model to classify numbers 8 and 9, while still retaining the model's learned capabilities. 

# why activations and not features ?

<img width="724" height="724" alt="image" src="https://github.com/user-attachments/assets/e0f9acd7-9c6d-4107-a299-d09f7f64f613" />



One neuron may encode multiple features. Thus, a neural network can represent more features than it has neurons. This implies that the feature space is higher-dimensional than the activation space. Each feature in this higher-dimensional space corresponds to a direction in the activation space. Therefore, we can treat activations as vectors that represent feature directions. By modifying these activations (and hence the directions), we can change the features represented within the neural network.

# Experiments

1. Cross Activation steering
Here we take data A and data B which is trained on model A and model B respectively (model A and B have the same design). Then we compute mean of actiavtions at each layer l for both models. after that we compute the differece between the activations therefore we get steering vectors at each layer l is. Finally, we add the steered vectors to the initial activations of model A to get our steered model. This steered model can predict for data B even though it was no trained on it .

orange is the steered model's activations / blue is model A activations 
<img width="609" height="583" alt="image" src="https://github.com/user-attachments/assets/6f58117b-f546-4949-9743-a284495ba6e8" />


problems with cross actiavtion steering - Though the model A and B have simillar design, they are trained on different data ( data A - numbers 0-8 and data B- number 9 ). Thus even though activation dimension is the same, they may lie in different activation subspaces of the same plane. Thus in steering the model A to predict 9, we end up removing the models previous capabilities. 
   
3. Self activation steering with capability retention
   Here we take data A and data B, where only data A is used to train model A and data B is the desired data we want the model to predict correctly. After training model A on data A we compute model A activations for data A and then we
   do the same for model A actiavtions for data B ( or no. 9 . Thus we get mmodel activations for data A and data and data B which we then compute mean at each layer l and then find their difference to get steering vectors or steering        activations. then we use this to steer model A to predict for data B while still keeping its capabilities of predicting for model A.

    orange is the steered model's activations / blue is model A activations 
<img width="680" height="648" alt="image" src="https://github.com/user-attachments/assets/d5654d3e-458f-4144-8f13-c0c0cbdb6bfd" />

   problems - the accuracy of the model reduces as the steered activations affect the inintial activations greatly due to the model A not being robust to high change in activation space.
              this is also bbecaause the model A requires a large control value to steer the model towards 9.

   accuracy- 65% on train and 63% cross validation 
    
5. Improving self activation steering with capability retention via noise injection in dataset
   
   We improve the model accuracy by training model A on data A with gaussian noise applied on each image. This makes model more robust and the model can retain learnned capabilities better.

   <img width="594" height="577" alt="image" src="https://github.com/user-attachments/assets/e7020f64-0eba-4d86-a13f-eae25ae4ea6f" />

   <img width="989" height="590" alt="image" src="https://github.com/user-attachments/assets/9894aa16-8468-480d-88d7-65aad7acd39e" />

   <img width="1341" height="779" alt="image" src="https://github.com/user-attachments/assets/678ea38a-f0fd-4c9c-b89a-07d012d59668" />



   accuracy - 90% on train and 89% on cross validation.

# Futhter experiments 

We are workinng on multi steer activation steering and anim to improve accuracy. Also we are investigating  if this has to do witth the robustness of a model or the models uncertaininty. 


   
