# SARSA (State-Action-Reward-State-Action)

**Type**: Reinforcement Learning  
**Category**: Policy-based method

## Overview
SARSA is an on-policy reinforcement learning algorithm that updates the action value function based on the state-action pairs visited by the agent following a specific policy. It was introduced as a way to learn policies that depend on both the current state and the agent's actions.

## Key Concepts
- **Policy Learning**: SARSA learns a policy that specifies the best action to take in each state.
- **On-policy Method**: Learns the value of the policy being carried out by the agent.
- **Temporal Difference (TD) Learning**: Utilizes differences between estimated values at successive time steps for learning.

## How It Works
1. Initialize the Q-values arbitrarily for all state-action pairs.
2. For each episode:
   - Initialize the state.
   - Choose an action from this state using a policy derived from Q (e.g., ε-greedy).
   - Take action, observe the reward, and next state.
   - Choose the next action from the next state using the policy.
   - Update the Q-values using the observed reward and the estimated Q-values of the next state-action pair.
   - Repeat steps until the episode ends.

## Mathematical Model (Optional)
```
Q(S_t, A_t) ← Q(S_t, A_t) + α [R_t+1 + γ Q(S_t+1, A_t+1) - Q(S_t, A_t)]
```

## Pseudocode
```
Initialize Q arbitrarily
For each episode:
    Initialize S
    Choose A from S using policy derived from Q (e.g., ε-greedy)
    For each step of episode:
        Take action A, observe R, S'
        Choose A' from S' using policy derived from Q
        Q(S, A) ← Q(S, A) + α[R + γQ(S', A') - Q(S, A)]
        S ← S'; A ← A';
    until S is terminal
```

## Implementation (Python)
```python
def sarsa(Q, alpha, gamma, epsilon, num_episodes):
    for i in range(num_episodes):
        state = env.reset()
        action = epsilon_greedy(Q, state, epsilon)
        done = False
        while not done:
            next_state, reward, done, _ = env.step(action)
            next_action = epsilon_greedy(Q, next_state, epsilon)
            Q[state][action] += alpha * (reward + gamma * Q[next_state][next_action] - Q[state][action])
            state, action = next_state, next_action
    return Q
```

## Applications
- **Robotics**: Navigating complex environments.
- **Gaming**: Strategy and real-time decision making.
- **Control Systems**: Dynamic system control such as in HVAC systems.

## Strengths
- Can converge to an optimal policy while exploring actions.
- More stable compared to off-policy methods like Q-learning.

## Limitations
- Dependent on the policy used for learning.
- Less efficient on problems where off-policy learning is feasible.

## References and Further Reading
- Richard S. Sutton and Andrew G. Barto, "Reinforcement Learning: An Introduction."
