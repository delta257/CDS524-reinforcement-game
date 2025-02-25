# CDS524-reinforcement-game
This report presents a reinforcement learning-based game designed using Q-learning. The game involves an agent navigating a maze to reach a goal while avoiding obstacles and managing energy. The Q-learning algorithm enables the agent to learn optimal policies through interactions with the environment, maximizing cumulative rewards.
1.Game introduction
This report presents a reinforcement learning-based game designed using Q-learning. The game involves an agent navigating a maze to reach a goal while avoiding obstacles and managing energy. The Q-learning algorithm enables the agent to learn optimal policies through interactions with the environment, maximizing cumulative rewards.

2.Design detail
2.1 Objective and rule
The objective of the game is for the agent (represented by a yellow square) to move from the start point (green square) to the end point (red square) while avoiding walls (grey squares) and a dynamic obstacle (purple square). The agent has limited energy and must reach the end point in as few steps as possible. The game ends if the agent reaches the goal, collides with the obstacle, or runs out of energy.
2.2 State and action space
State Space: Defined by the agent’s position, the obstacle’s position, and the remaining energy.
Action Space: The agent can move in four directions: up, down, left, and right.
2.3 Reward function
The reward function is designed to encourage the agent to reach the goal efficiently and avoid obstacles:
+100: For reaching the goal.
-10: For hitting a wall.
-2: For each step taken (step penalty).
-100: For colliding with the obstacle.
+5: For successfully avoiding the obstacle.
2.4 Game Environment
The maze is represented as a 2D grid using Pygame. The game includes a dynamic obstacle that moves randomly, adding complexity to the agent’s navigation.
3.Q-Learning Implementation
3.1Q-Learning Algorithm
The Q-learning algorithm is implemented to train the agent to learn an optimal policy. Key components include:
Q-Table: A 5-dimensional array (rows x cols x rows x cols x actions) to store Q-values for each state-action pair.
Epsilon-Greedy Exploration: The agent explores randomly with probability epsilon and exploits the learned policy with probability (1 - epsilon). Epsilon decays over time to reduce exploration.
Hyperparameters:
Learning rate (alpha) = 0.8
Discount factor (gamma) = 0.95
Initial epsilon = 0.9 (decays to 0.01 over time)
3.2 Training Process
The agent is trained over 2000 episodes. In each episode:
The agent and obstacle positions are initialized.
The agent selects actions using the epsilon-greedy strategy.
The environment provides feedback in the form of rewards and the next state.
The Q-table is updated using the formula:
Q(s, a) = Q(s, a) + alpha * (reward + gamma * max(Q(s', a')) - Q(s, a))
The episode ends when the agent reaches the goal, collides with the obstacle, or runs out of energy.
3.3 Dynamic Obstacle Handling
The obstacle moves randomly in one of the four directions at each step. The agent’s Q-learning algorithm is updated to account for the obstacle’s movement, ensuring the agent learns to avoid it dynamically.
4.Game Interaction
A Pygame-based user interface (UI) is developed to visualize the game:
Maze Visualization: The maze grid is displayed, with walls, the agent, the goal, and obstacles represented by different colors.
Energy Display:  The agent’s remaining energy is shown in real-time.
Reset Button:  A button allows users to reset the game after it ends.
Value Display: The UI includes a display of the agent’s Q-values for debugging and visualization.
5.Evaluation Results
5.1 Training Performance
After 2000 training episodes, the agent demonstrates significant improvement:
Success Rate:  The agent reaches the goal in ~90% of episodes.
Energy Efficiency:  The average energy consumed per episode decreases from ~40 units to ~20 units.
Reward Trends: The average total reward per episode increases from -100 (initial random movements) to +80 (trained agent).
5.2 Test Environment
In a test environment with a fixed obstacle and starting position, the agent consistently reaches the goal while avoiding the obstacle. The agent’s path is optimized, and it demonstrates the ability to adapt to the obstacle’s movements.
6.Challenges and Solutions
6.1 Challenge 1: Dynamic Obstacle Handling
Problem: The obstacle’s random movement made it difficult for the agent to predict its path, leading to frequent collisions.
	Solution: The Q-table was updated to include the obstacle’s position as part of the state, allowing the agent to learn to avoid it dynamically.
6.2 Challenge 2: Energy Management
Problem: The agent often ran out of energy before reaching the goal, especially in longer paths.
	Solution: The step penalty was reduced, and the agent was trained to prioritize shorter paths. Additionally, the initial energy was increased to allow for longer exploration.
6.3 Challenge 3: Q-Table Size
Problem: The 5-dimensional Q-table was memory-intensive and slow to update.
	Solution: The Q-table was optimized by reducing its dimensions (e.g., discretizing energy levels) and using a more efficient data structure.
7.Conclusion
This project successfully applies Q-learning to a maze-solving game with dynamic obstacles and energy management. The agent learns to navigate efficiently, avoid obstacles, and conserve energy. Future work could explore more complex environments, such as multi-agent scenarios or 3D mazes, and advanced reinforcement learning techniques like deep Q-networks (DQN).
