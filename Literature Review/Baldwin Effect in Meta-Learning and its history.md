## Original Model-Agnostic Meta-Learning (MAML) inspiration
- Uses gradient descent to learn initial parameter values of a neural network to make learning new parameter values easier and faster for different tasks
## Meta-Learning by the Baldwin Effect
- Shows that Baldwin effect is competitive with MAML without having to be differentiable or having direct access to gradients
- Initial weights and hyperparameters are inherited but learned weights are forgotten from one generation to the next
- Darwinian evolution means there's no learning within a lifetime
- Already shown before this paper that the Baldwin effect works to form initial parameters and hyperparameters of a learning algorithm
- This paper shows that BE also works for evolving agents on task distributions to be few-shot data-efficient
- Genome evolved is shaped by task distribution
- Learning algorithm learns specific tasks
- Compares Baldwin to standard Darwinian and Lamarckian evolution
- Next steps is to test evolutionary meta-learning approaches on more complex task distributions and for non-differentiable fitness functions like multi-modal data distributions
### Steps for Meta-Learning by BE
1. Generate population of individuals, where each individual has neural network weights and learning parameters for the entire network
2. Pick some individuals
3. Give those individuals some tasks from a distribution
4. First, copy those individual's starting weights and biases
5. Let it learn using gradient descent on all those tasks with each task (still involves loss and weight updates)
6. Evaluate the results after learning using a fitness function, which aggregates its performance across tasks
7. Create offspring by selecting the individuals with better fitness but only inherit the original weights and biases of those selected individuals and use an evolutionary algorithm to choose how to crossover genomes
8. Repeat for many generations
![[Pasted image 20260914221116.png]]
### MAML
- Randomly initialize parameters
- Loop through tasks in distribution
- Evaluate loss on that task for k examples
- Use loss to do gradient descent on the parameters for inner loop on each specific tasks
- After all tasks covered, another step of gradient descent is done based on the sum of all the losses on tasks? Shows a summation![[Pasted image 20260914220727.png]]
### Genetic algorithms (GA) used
- Steady State Genetic Algorithm - 
- Generational Genetic Algorithm
### Natural Evolution Strategies (NES)
- This paper uses separable NES

## Tasks
### Sinusoid-fitting task
- Agent fits a single sinusoid chosen from a distribution of phases and amplitudes, regression task
- 25 different sine waves are sampled per generation, 10 points used for training and 10 points used for testing
- Amplitude sampled uniformly from [0.1, 5.0] and phases from [0, pi]
- 5 gradient descent steps for each sine wave in one fitness evaluation
- Performance evaluated using MSE (mean-squared error)
- Fitness evaluated performance as averaged results for different sine waves
- Tested with MAML, NES, and GA
#### Model
- Neural network with two hidden layers with 40 neurons each
- Initialized with Gaussian noise of mean 0 and std 0.01
#### Result
- MAML ended up being better but results were comparable
- Initial weights and biases ended up making the prediction to be the general shape of a sine wave even before any learning
### Physics simulation reinforcement learning tasks
- Tested with Baldwinian, Darwinian and Lamarckian evolution
- Baldwinian has gradient descent but only initial weights and biases inherited
- Darwinian had no learning at all, no gradient descent
- Lamarckian has learning and inherits that learning
- 10 episodes were used for fitness evaluation with different task parameters
- MuJoCo tested two Planar Cheetah tasks, one for goal direction and the other for goal velocity
#### Model
- A2C controller?
- two hidden layers of size 100
- Softmax output across 12 discrete actions
#### Result
- Lamarckian better than Baldwin and Darwinian for goal velocity
- Baldwin better than the other two for goal direction
- This mean Baldwin is better for a task that requires more drastic changes while Lamarckian is better at fine-tuning but not for bigger changes in task requirements
- Baldwin better for quickly changing and broad scenarios
- Lamarckian better for narrow task distribution