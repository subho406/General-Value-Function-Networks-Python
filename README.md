# General Value Function Networks Python

Implements General Value Function Networks proposed in https://arxiv.org/abs/1807.06763 using JAX. 

Implementation Report: https://subho406.github.io/General-Value-Function-Networks-Python/Reproducing_General_Value_Function_Networks_31_jan_2022.pdf

### Abstract:
State construction is important for learning in partially observable environments. A general purpose strategy for state construction is to learn the state update using a Recurrent Neural Network (RNN), which updates the internal state using the current internal state and the most recent observation. This internal state provides a summary of the observed sequence, to facilitate accurate predictions and decision-making. At the same time, specifying and training RNNs is notoriously tricky, particularly as the common strategy to approximate gradients back in time, called truncated Back-prop Through Time (BPTT), can be sensitive to the truncation window. Further, domain-expertise--which can usually help constrain the function class and so improve trainability--can be difficult to incorporate into complex recurrent units used within RNNs. In this work, we explore how to use multi-step predictions to constrain the RNN and incorporate prior knowledge. In particular, we revisit the idea of using predictions to construct state and ask: does constraining (parts of) the state to consist of predictions about the future improve RNN trainability? We formulate a novel RNN architecture, called a General Value Function Network (GVFN), where each internal state component corresponds to a prediction about the future represented as a value function. We first provide an objective for optimizing GVFNs, and derive several algorithms to optimize this objective. We then show that GVFNs are more robust to the truncation level, in many cases only requiring one-step gradient updates.

### Instructions
```
#install the required dependencies
pip install -r requirements.txt

#run an experiment with a desired set of parameters, example below: 
python experiments/compass_world.py --truncation 1 --seed 1 --lr 0.01 --optimizer sgd --agent prnn 
```

### Experiments:

1. `experiments/compass_world.py`

```
usage: compass_world.py [-h] [--truncation TRUNCATION] [--lr LR]
                        [--tdc_beta TDC_BETA]
                        [--rnn_hidden_size RNN_HIDDEN_SIZE]
                        [--env_size ENV_SIZE] [--hidden_size HIDDEN_SIZE]
                        [--steps STEPS] [--eval_steps EVAL_STEPS]
                        [--seed SEED] [--wandb] [--agent_type AGENT_TYPE]
                        [--output_dir OUTPUT_DIR] [--optimizer OPTIMIZER]

optional arguments:
  -h, --help            show this help message and exit
  --truncation TRUNCATION
  --lr LR
  --tdc_beta TDC_BETA 
                      TDC beta value, applicable only for TDC/TDRC agent.
  --rnn_hidden_size RNN_HIDDEN_SIZE
  --env_size ENV_SIZE
  --hidden_size HIDDEN_SIZE
  --steps STEPS
  --eval_steps EVAL_STEPS
  --seed SEED
  --wandb               Use wandb for logging.
  --agent_type AGENT_TYPE
                        Agent to use for training. Available options: [prnn,
                        gvfn_td,gvfn_tdc]
  --output_dir OUTPUT_DIR
                        Dump the output to numpy array
  --optimizer OPTIMIZER
                        Optimizer to use. One of [sgd, adam]
   ```
   
### Results:
1. Compass World:

![RMSVE: Compass World](results/rmsve_result_compass_world.png)
![Accuracy: Compass World](results/accuracy_result_compass_world.png)
   


### Anknowledgements
- Original Authors: Matthew Schlegel, Andrew Jacobsen, Zaheer Abbas, Andrew Patterson, Adam White, Martha White.
- Huge thanks to Prof. Adam White, and PhD students Matthew Schlegel and Andrew Patterson for their help throughout this project.
- Original Implementation (https://github.com/mkschleg/GVFN)
