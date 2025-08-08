Study of Classic Navigation Stack vs Reinforcement Learning-based Navigation
Overview
In this report, I explore and compare two approaches to mobile robot navigation:
1. Classic Navigation Stack: A traditional pipeline-based method using mapping, localization, path planning, and control.
2. Reinforcement Learning (RL) Navigation: A data-driven approach where an agent learns navigation policies through interaction and reward feedback.
The goal is to highlight their core components, advantages, limitations, and typical use-cases, without implementing them in ROS.
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

1. Classic Navigation Stack
1.1 Architecture and Components
The classic navigation stack follows a modular pipeline:

1. Mapping: Build or load a map of the environment.
   * Commonly uses SLAM (e.g., GMapping, Cartographer).
     
2. Localization: Estimate the robot's pose within the map.
   * Techniques: AMCL (Adaptive Monte Carlo Localization).
     
3. Path Planning:
   * **Global Planner: Computes a collision-free path from start to goal (e.g., Dijkstra, A\*).
   * **Local Planner: Generates velocity commands to follow the global path while avoiding dynamic obstacles (e.g., DWA, TEB).
    
4. Control & Obstacle Avoidance**:
   * Uses costmaps (static and dynamic) to represent obstacles.
   * Adjusts velocity commands based on sensor data (e.g., laser scans).

1.2 Strengths
* Deterministic Behavior: Predictable and explainable actions.
* Modular & Flexible: Components can be swapped or tuned independently.
* Mature Ecosystem: Well-supported in ROS with extensive community and documentation.

1.3 Limitations
* Hand-crafted Heuristics: Requires careful parameter tuning (e.g., costmap inflation radius, velocity limits).
* Limited Adaptability: Struggles in highly dynamic or unstructured environments.
* Scaling Challenges: Integrating semantic understanding or long-horizon planning can be complex.

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

2. Reinforcement Learning-based Navigation
2.1 Core Principles
Reinforcement Learning (RL) treats navigation as a Markov Decision Process (MDP):

* State  (s): Sensor readings, current pose, local map.
* Action (a): Velocity commands or motion primitives.
* Reward (r): Feedback signal, e.g., positive for reaching goal, negative for collisions.
* Policy (π): Function mapping states to actions, learned through trial and error.

### 2.2 Algorithm Categories
1. Model-Free RL:
   * Value-Based: Q-Learning, DQN.
   * Policy Gradient: REINFORCE, PPO, A3C.
     
2. Model-Based RL:
   * Learns a dynamics model to plan ahead (e.g., Dyna, PILCO).

2.3 Training Workflow
1. Simulation: Train in simulated environments (Gazebo, PyBullet) to collect experiences.
2. Reward Shaping: Design a reward function that balances reaching goals, efficiency, and safety.
3. Policy Evaluation: Validate performance on unseen maps or real robots.

2.4 Strengths
* Adaptive: Learns to handle complex, dynamic scenarios without explicit rules.
* Unified Framework: Integrates perception, planning, and control in one policy.
* Emergent Behavior: Can discover novel strategies (e.g., wall following).

2.5 Limitations
* Sample Inefficiency: Requires large amounts of training data.
* Training Complexity: Sensitive to reward design and hyperparameters.
* Sim-to-Real Gap: Policies trained in simulation may not transfer perfectly.

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## 3. Comparative Analysis

| Aspect                    | Classic Stack                   | RL-based Navigation                |
| ------------------------- | ------------------------------- | ---------------------------------- |
| Behavior                  | Rule-based, deterministic       | Learned, stochastic                |
| Adaptability              | Limited, rule-bound             | High, data-driven                  |
| Development Effort        | Manual module tuning            | Extensive training and tuning      |
| Explainability            | High—transparent steps          | Low—black-box policies             |
| Real-time Performance     | Proven on low-spec hardware     | Varies; may need GPU               |
| Robustness                | Reliable in structured settings | Strong in dynamic or unknown areas |

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

4. Use Cases and Future Directions

* Classic Stack: Ideal for industrial AGVs, warehouse robots, and indoor services where environments are mapped and stable.
* RL Navigation: Promising for exploration, search-and-rescue, and highly dynamic outdoor settings.

Hybrid Approaches that combine classical planners with RL-based local policies could leverage the benefits of both techniques.

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Conclusion

Both the classic navigation stack and RL-based navigation offer valuable tools for robotic pathfinding. The classic stack excels in predictable, well-mapped environments with clear operational requirements and high explainability. Reinforcement learning shines when adaptability is critical and when robots face novel or dynamic scenarios. Understanding the strengths and limitations of each approach helps guide the choice or integration of navigation strategies for a given application.

**Prepared by Marjuk**
