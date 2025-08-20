# Actor-Critic on CartPole

This repository contains an implementation of the **Actor-Critic method** on the CartPole-v0 environment using Keras.  

The code is adapted from the official Keras example:  
- [Keras documentation: Actor-Critic CartPole](https://keras.io/examples/rl/actor_critic_cartpole/)  
- [Source code on GitHub](https://github.com/keras-team/keras-io/blob/master/examples/rl/actor_critic_cartpole.py)  

I studied the documentation and brought the source code into this repo for learning and experimentation purposes.

## How it works
- **Environment (CartPole)**: A pole is attached to a cart. The agent must keep the pole upright by applying left/right force.
- **State** = [cart_position, cart_velocity, pole_angle, pole_angular_velocity]
- **Actor**: Given the environment state (4 values), outputs a probability distribution over actions (left/right).
- **Critic**: Given the same state, predicts the expected future reward (value function).

## Training loop
1. Actor samples an action from its probability distribution.
2. Action is applied in the environment → new state, reward, done.
3. Critic estimates the value of the state (expected future reward).
4. Compute discounted returns with factor `gamma`.
5. Update:
   - **Actor**: increase probability of actions that led to higher-than-expected rewards (policy gradient).
   - **Critic**: minimize error between predicted value and actual returns.
6. Repeat until running reward > 195 (CartPole solved).

---

## Actor–Critic Flow Diagram

```bash
    State (s)
       │
       ▼
┌───────────────┐
│     Actor     │───> Action (a) ───> Environment
└───────────────┘                         │
       │                                  │
       ▼                                  ▼
┌───────────────┐                  Next State (s'), Reward (r)
│     Critic    │<───────────────────────────────┘
└───────────────┘
       │
       ▼
```
## Key idea
- **Actor** learns *what to do* (policy).  
- **Critic** learns *how good it is* (value).  
- They cooperate to stabilize and accelerate reinforcement learning.



