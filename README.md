# Development and Evaluation of Regularized Convolutional Neural Fitted Q Iteration (RC-NFQ) Algorithm for Autonomous Navigation
## ENPM690 - Robot Learning

## Dependencies
- python 3.9 (any version above 3 should work)
- Command-line interface
- Tensorflow
- Python running IDE (I used VS Code)
- Pytorch

## Libraries
- TensorBoard

## Installation Instructions
1. Download and extract the required files from the file.
2. Navigate to the extracted directory and build the code using the commands:
    ```
    cd highway-env/
    sudo python3 setup.py install
    cd ../rl-agents/
    sudo python3 setup.py install
    ```

## Problem
This guide covers the processes of training and testing reinforcement learning models specifically designed for highway driving environments using the RCNFQ algorithm. Utilizing configurations for various agents and environments, the procedure includes command-line operations for training, testing, and visualizing performance metrics.

## Features
1. Model Training: Automate the training of RL models with custom episode counts.
2. Model Testing: Evaluate model performance using best-saved checkpoints.
3. Result Visualization: Visualize training and testing results using Python scripts and TensorBoard


## Usage
1. Training: Run the training command from the rl_agents/scripts directory:
    ```
    python experiments.py evaluate configs/HighwayEnv/env.json configs/HighwayEnv/agents/RCNFQAgent/rcnfq.json --train --episodes 2000
    ```
    Replace '2000' with your desired number of episodes. The videos, weight checkpoints, event file and metadata are stored in a directory with the appropriate date, time, and process ID:
    ```
    rl_agents/scripts/out/HighwayEnv\RCNFQAgent\rcnfq_YYYYMMDD-HHMMSS_PID
    ```
2. Testing: Specify the checkpoint to recover from in the testing command:
    ```
    python experiments.py evaluate configs/HighwayEnv/env.json configs/HighwayEnv/agents/RCNFQAgent/rcnfq.json --test --episodes 10 --recover-from "out/HighwayEnv/RCNFQAgent/rcnfq_YYYYMMDD-HHMMSS_PID/checkpoint-best.tar"
    ```
    In our case, I have already trained a model. The checkpoint can be accessed by:
    ```
    python experiments.py evaluate configs/HighwayEnv/env.json configs/HighwayEnv/agents/RCNFQAgent/rcnfq.json --test --episodes 10 --recover-from "out\HighwayEnv\RCNFQAgent\rcnfq_20240430-123253_27365\checkpoint-best.tar"
    ```

## Visualization
1. Visualizing Statistics: To visualize statistics from the training or     testing phase, use the following command:
    ```
    python graph.py "out/HighwayEnv/RCNFQAgent/rcnfq_YYYYMMDD-HHMMSS_PID/openaigym.episode_batch.0.PID.stats.json"
    ```
    Replace YYYYMMDD-HHMMSS and PID accordingly.

2. TensorBoard for Event Logs: For a more detailed view with TensorBoard, navigate to the directory of your event file and start TensorBoard:
    ```
    tensorboard --logdir <path to your event directory> 
    ```
    ie. rcnfq_YYYYMMDD-HHMMSS_PID
    
    Follow the link mentioned in the terminal (Usually it is http://localhost:6006/ or http://localhost:6007/)

## Contributions
- rc_nfq directory in rl_agents\rl_agents\agents
- config file in rl-agents\scripts\configs\HighwayEnv\agents\RCNFQAgent

## Environment
![](https://github.com/vishnumandala/Development-and-Evaluation-of-RC-NFQ-Algorithm-for-Autonomous-Navigation/blob/main/highway-env.gif)

## Demonstration
![](https://github.com/vishnumandala/Development-and-Evaluation-of-RC-NFQ-Algorithm-for-Autonomous-Navigation/blob/main/demo.gif)

## Note
1. We have taken the highway environment from: https://github.com/Farama-Foundation/HighwayEnv
2. We have used the DQN model from: https://github.com/eleurent/rl-agents
3. We have referenced the rcnfq code from: https://github.com/cosmoharrigan/rc-nfq
