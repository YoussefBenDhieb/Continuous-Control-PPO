[//]: # (Image References)

[image1]: https://user-images.githubusercontent.com/10624937/43851024-320ba930-9aff-11e8-8493-ee547c6af349.gif "Trained Agent"
[image2]: ./images/plot_of_rewards.png "plot of rewards"

# Continuous Control Project Report

## 1. Introduction

For this project, we implemented a PPO agent to solve the [Reacher](https://github.com/Unity-Technologies/ml-agents/blob/master/docs/Learning-Environment-Examples.md#reacher) environment.

![Trained Agent][image1]

In this environment, a double-jointed arm can move to target locations. A reward of +0.1 is provided for each step that the agent's hand is in the goal location. Thus, the goal of your agent is to maintain its position at the target location for as many time steps as possible.

The observation space consists of 33 variables corresponding to position, rotation, velocity, and angular velocities of the arm. Each action is a vector with four numbers, corresponding to torque applicable to two joints. Every entry in the action vector should be a number between -1 and 1.

## 2. Learning Algorithm

In order to solve the environment we implemented a PPO agent according to the [Proximal Policy Optimization Algorithms](https://arxiv.org/pdf/1707.06347.pdf) paper.

PPO is an actor critic model. The idea behind it, is that we limit how far we can change our policy in each iteration through the KL-divergence, where the KL-divergence measures the difference between two data distributions p and q which are our old and new policies.

In order to train the network, for each episode, we first collect trajectories from the 20 agents (part 4.2 in [Continuous_Control.ipynb](Continuous_Control.ipynb), then, we update the model 30 times successively (clipped_surrogate function in part 4.2 in [Continuous_Control.ipynb](Continuous_Control.ipynb)).

## 3. Model Architecture

The PPO agent has an actor and a critic networks implemented in the Policy class in part 4.1 in [Continuous_Control.ipynb](Continuous_Control.ipynb).

Both of them are have two fully connected hidden layers of size 512 each, while the actor outputs 4 actions with tanh activation and the critic outputs one value without activation function.

## 4. Hyperparameters Tuning

The hyperparameters where chosen using trial and error.

We used a :

- Learning rate of 3 e-4

- Gradient_clip of 0.2 to limit the gradient

- Epsilon value of 0.1 for the surrogate function in order to limit how far we can change our policy

- Dicount factor Gamma of 0.99

- Update value of 30 (we update our model 30 times each episode)

- Regulation term beta of 0.01

## 5. Results

The agent was able to solve the environment after 136 episodes with an average score of 30.02 for the last 100 episodes.

![plot of rewards][image2]

## 6. Ideas for Future Work

Even though the results where satisfying, we still can improve them by tuning the hyperparameters or by implementing other types of agents like DDPG or A3C and benchmark the results.
