# Deep Learning for Astrostatistician

## Reinforcement Learning network

- Needs a:
    - Policy network: Self learning deep neural network
    - Value network: Ready to work

## Initialization
- For a NN with $n$ inputs and $r$ outputs, the initialization paradigm suggests the weights to be drawn from 

$$
W\sim U(-\sqrt{\frac{6}{n+r}},\sqrt{\frac{6}{n+r}})
$$

- The derivation assumes linearity in NN

## Training

- If the momentum algorithm repeatedly sees the same gradient $g$, it will accelerate in the direction $-g$ to a maximujm velocity of $\epsilon||g||/(1-\alpha)$

- Common choices of $alpha$ are 0.5, 0.9, 0.99. This isn't the learning rate. This alpha starts slow and increases over time. $\epsilon$ is the learning rate in this.
