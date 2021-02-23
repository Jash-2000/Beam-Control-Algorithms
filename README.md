# Balancing a pole on a dynamically moving cart.
<p align="center">
 <img src = "https://github.com/Jash-2000/Beam-Control-Algorithms/blob/main/Problem_fig.png" alt = "Control_System_Representation"/>
</p>

The task of balaning a beam on a cart is a **classic problem in Control Engineering**. The original model deals with a variety of constraints including physical parameters like friction and centre of mass, but for the purpose of simulation, we have to work with certain assumptions. We have **assumed a 1-D motion in which a pole is attached by an un-actuated joint** to a cart, which moves along a frictionless track. The system is controlled by applying a **force of +1 or -1 units to the cart i.e. either right or left**. The pendulum starts upright, and the goal is to prevent it from falling over. **The state space control block is represented by four values: cart position, cart velocity, pole angle, and the velocity of the tip of the pole.** The animation ends when the pole is more than 15 degrees from vertical, or the cart moves more than 2.4 units from the center. Further, a reward of +1 is provided for every timestep that the pole remains upright.

In this repository, I have implemented this problem using various **model based** and **model free** algorithms. The simulation environment used in OpenAI Gym which provides the data for **feedback loop**. It also aids in obaining a rendered animation output. 
Diifferent algorithms used can be summarized below.

  * **Gaussian sampling** - This mehtod initiates the action space with completely random values. It is clearly observant the the average episode length is no longer than 7. 
  * **Naive-Greedy Brute Force** - The Naive weight allocation method used a brute force algorithm to get the best weights. The average episode length was found to be around 200. This approach iterates through 100 random weigths which decide the update steps and saves the best obtained weights. It is basically a single layer Neural Network without backpropogation, hence **Naive**.
  * Further improvements were made by using **PID controlled On-Off controller** with fixed weights. The graph obtained is of oscillatory nature as the **control problem is of Regulatory nature**. The control block and the output obtained is shown below. The pole doesnt fall ever !!!!

![PID](PID.png)  ![Control Block](control_block.png) 

  * Developed a simple Deep Q-Learning Network(dqn) based system for balancing a beam imported from OpenAI gym, using a policy based (Boltzmann policy) rewqrding strategy

---

## To run the files
  * Clone the repo or download it and extract the files.
  * Import Open AI Gym using the following commmand
  ```cmd
    pip intall gym
  ```
  Gym contains a collection of pre-defined environments, where we can run our algorithms. 
  * It may take up some amount of time while training the network. So it is better to comment out **env.render()** before starting the training. 
  * Gym also allows you to save the final rendered output files using its wrapper functions. The final saved video files, weights and other logs would get saved in your working directory. To work with gym wrappers and save the output files in, 
   ```python
    from gym import wrappers
    env = wrappers.Monitor(env, '..\Desktop\RL\MovieFiles', force = True)
   ```
