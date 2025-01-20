# Connect4 Q Reinforcement Learning Agent with Domain Knowledge Boost


## Summary
This project showcases the development of a Connect4-playing reinforcement learning (RL) agent. 
### Methodology
- **Training Phases**: The agent was trained in three progressive phases:
  1. Against a random opponent.
  2. Against an untrained agent.
  3. Against itself.
- **Reward System**: Incentivized strategic moves (e.g., center control, aligning pieces, blocking threats).
- **Algorithm**: Utilized Q-learning, a model-free, value-based RL method.

### Findings
- Strategic reward design accelerated learning and improved performance.
- The agent developed offensive and defensive strategies.

### Results
- **Efficiency**: Training completed in ~200 seconds for 10,000 episodes.
- **Performance**:
  - Win rate >99% against random opponents.
  - Win rate ~55% against more intelligent opponents.

---

## Project Overview

This project focuses on developing a reinforcement learning (RL) agent capable of playing the Connect4 game against a human opponent or another agent. The agent should be effective when playing as both the first and second player. The core objectives include defining the environment, agent actions, reward system, and strategy using RL principles.

---

## Problem Definition

### Connect4 Game Overview

- **Game Board:** Vertical grid with 6 rows and 7 columns.
- **Goal:** Be the first to form a horizontal, vertical, or diagonal line of four tokens.
- **Players:** Two players, typically using red and yellow tokens.
- **Gameplay:**
  - Players take turns dropping a token into one of the seven columns.
  - Tokens occupy the lowest available position in the selected column.
  - The game ends when a player forms a line of four tokens or the board is full (resulting in a draw).

### Environment Definition

- **State Representation:** The current board configuration, where each cell can be:
  - **Empty:** Represented by `0`.
  - **Player 1's Token:** Represented by `1`.
  - **Player 2's Token:** Represented by `2`.

Example board state:

```
Col 1 | Col 2 | Col 3 | Col 4 | Col 5 | Col 6 | Col 7
  0   |   0   |   0   |   0   |   0   |   0   |   0  
  0   |   0   |   0   |   1   |   0   |   0   |   0  
  0   |   2   |   0   |   1   |   0   |   0   |   0  
  0   |   2   |   0   |   2   |   0   |   0   |   0  
  0   |   1   |   0   |   2   |   0   |   0   |   0  
  1   |   1   |   1   |   2   |   0   |   0   |   0  
```

- **Action Space:** The agent can drop a token into any column that is not full.
  - Valid actions: `A = {1, 2, 3, 4, 5, 6, 7}` (where the column is not full).

---

## Reward System

### Initial Reward System

| Situation                | Reward Value |
|--------------------------|--------------|
| Agent Wins              | +1           |
| Agent Loses             | -2           |
| Draw                    | -1           |
| Non-terminal Move       | -0.1         |

### Updated Reward System

| Situation                | Reward Value |
|--------------------------|--------------|
| Agent Wins              | +100         |
| Agent Loses             | -100         |
| Draw                    | 0            |
| Center Control          | +3 per token |
| Three-in-a-Row (with space) | +5         |
| Two-in-a-Row (with two spaces) | +2     |
| Opponent Threat (three-in-a-row with space) | -4 |

### Rationale for Updates

- **Domain Knowledge:** Heuristics such as center control and partial alignments are grounded in Connect4 strategies, guiding the agent towards advantageous states based on game theory and strategic intuition.
- **Winning Incentives:** Increased reward for winning (`+100`) prioritizes strategies that lead directly to victory.
- **Strategic Defense:** Penalizing opponent threats (-4) encourages active defensive play, aligning with the agent's learning goals.
- **Accelerated Learning:** Rewards for intermediate alignments (e.g., three-in-a-row) enable faster strategy development and better generalization to complex scenarios.

---

## Training Methodology

Training was divided into three phases to ensure progressive learning:

1. **Phase 1 (40%):** Training against a random opponent.
2. **Phase 2 (30%):** Training against an untrained agent.
3. **Phase 3 (30%):** Self-play.

### Metrics Monitored:

- **Win Rate:** Percentage of games won during training.
- **Average Episode Length:** Average number of moves per game.
- **Avg Rewards:** Average rewards across episodes.

### Training Results

| Phase       | Duration (s) | Avg. Reward | Avg. Length | Win Rate |
|-------------|--------------|-------------|-------------|----------|
| Phase 1     | 27.19        | 199.51      | 8.73        | 99.72%   |
| Phase 2     | 85.29        | 420.66      | 27.19       | 56.80%   |
| Phase 3     | 86.72        | 427.10      | 27.68       | 54.67%   |

---

## Key Insights

1. **Strategic Progression:** Training in phases allowed the agent to evolve from simple strategies (Phase 1) to complex strategies (Phase 3).
2. **Domain Knowledge Impact:** Heuristic rewards (e.g., center control) accelerated learning and improved agent performance.
3. **Efficiency:** The entire training (10,000 episodes) completed in under 200 seconds.
4. **Performance:** Achieved:
   - >99% win rate against random opponents.
   - ~55% win rate against more complex opponents.

---

## Live Test Cases

To evaluate the agent's performance, the following test cases were designed:

1. **Agent vs. Random Player:** Evaluate the agent's ability to win against random moves. 
2. **Agent vs. Human Player:** Test performance against human strategies. 
3. **Agent as First and Second Player:** Analyze performance in both roles.

---
## Hardware and Software

- **Hardware:** MacBook Pro, Apple M1 Pro Chip, 16GB RAM.
- **OS:** macOS Sequoia 15.1.
- **Software:**
  - VSCode 1.95
  - Python 3.11


---

## References
1. Sutton, R. S., & Barto, A. G. "Reinforcement Learning: An Introduction." Chapter 6 on Value Function Approximation was particularly influential.


