# Neuro-Evolution Sandbox

A browser-based simulation where small neural networks learn to survive through evolution.

This project is an experimental sandbox exploring **neuro-evolution**: neural networks trained not with backpropagation or labeled data, but through **survival, reproduction, and mutation** inside a simple physical world.

Creatures begin completely clueless. Over generations, they evolve behaviors that look strategic, competitive, and occasionally surprising — all emerging from a few simple rules.

---

## Live Demo

👉 **[Live Demo Link]**  
(Open in your browser — no installation required)

---

## Overview

Each creature in the simulation is a triangle that lives in a 2D world. It must:

- Move through physical space
- Manage limited energy
- Find and compete for food
- Reproduce if it thrives
- Die if it fails

Every creature is controlled by a **small neural network**.  
There are no hard-coded strategies. No rules like “if food is closer, boost.”  
All behavior emerges through evolution.

Over time, creatures learn to:

- Steer efficiently toward food
- Conserve momentum and energy
- Compete tactically with others
- Use boost at precise, high-value moments
- Abandon contested resources
- Position themselves where food is *likely* to appear

None of this behavior is explicitly programmed.

---

## What Makes This Different

- No machine learning libraries
- No gradient descent
- No reward shaping
- No predefined strategies

Just:

- A physical world
- A simple neural network
- Mutation and selection
- Time

This project focuses on **open-ended learning** rather than solving a predefined task.

---

## The Creature Brain

Each creature has a fully connected feedforward neural network:

- **Inputs:** 12
- **Hidden neurons:** 16
- **Outputs:** 4
- **Total weights:** 276

The network structure is fixed. Only the weights evolve.

### Inputs (What the creature senses)

Every frame, the brain receives:

1. Food direction (left/right, forward/back in body space)
2. Distance to nearest food
3. Energy level
4. Speed
5. Turn rate
6. Orientation (sin and cos of angle)
7. Boost cooldown state
8. Brake cooldown state
9. Two constant bias inputs

These values summarize everything the creature can perceive.

---

### Outputs (What the creature decides)

The neural network produces four outputs:

1. **Thrust** (0 → 1)
2. **Turn** (-1 → 1)
3. **Boost probability** (0 → 1)
4. **Brake probability** (0 → 1)

Outputs are transformed using sigmoid and tanh functions and then applied directly to the physics system.

Boost and brake only trigger when probabilities cross a threshold, creating clear decision boundaries that evolution can exploit.

---

## Physics and World Rules

The simulation uses intentionally simple but physical motion:

- Velocity and momentum
- Acceleration limits
- Angular velocity
- Friction
- Energy costs for movement and turning

Energy is the central constraint:

- Existing drains energy
- Moving drains more
- Sharp turns drain extra
- Boosting is expensive
- Food replenishes energy
- Reproduction requires surplus energy

The world enforces tradeoffs. Survival is never free.

---

## Evolutionary System

### Selection

Reproduction uses **weighted random selection**:

- Every eligible creature gets a base chance
- Better performers get higher probability
- No single creature can dominate reproduction

This maintains genetic diversity and avoids premature convergence.

### Inheritance

When two creatures reproduce:

1. **Crossover:** Brain weights are split and recombined
2. **Mutation:** Random weight tweaks are applied
3. **Clamping:** Weights are kept within reasonable bounds

There is no “correct” brain. Evolution explores what works.

---

## Emergent Behavior

After enough generations, creatures exhibit behavior that was never explicitly coded:

- Tactical boosting to steal food from competitors
- Energy-aware decision making
- Abandoning high-competition targets
- Momentum-based coasting
- Predictive positioning near food spawn zones

The system occasionally appears to “outsmart” its own randomness.

---

## Project Structure

The entire simulation lives in a **single HTML file**:



Everything runs locally in the browser using:

- HTML
- `<canvas>`
- Vanilla JavaScript

No build step. No dependencies. No installation.

---

## Running Locally

1. Clone or download this repository
2. Open `index.html` in any modern browser
3. Watch evolution unfold

The simulation runs completely offline.

---

## Ideas to Explore

Some fun experiments to try:

- Add predators
- Change food clustering behavior
- Modify energy costs
- Increase or decrease mutation rate
- Change neural network size
- Add obstacles or terrain
- Experiment with different activation functions

Small changes can radically alter evolutionary outcomes.

---

## Philosophy

This project is not a product.  
It is not optimized.  
It is not meant to be efficient.

It exists to explore how **complex behavior can emerge from simple rules**, and how evolution discovers solutions differently than traditional machine learning.

Evolution does not learn *what* to do.  
It learns *what survives*.

---

## Related Writing

This repository accompanies a detailed article describing the design, behavior, and insights from the simulation:

👉 **[LinkedIn / Medium Article Link]**

---

## License

MIT License  
Do whatever you want with it. Break it. Remix it. Learn from it.

---

## Final Note

If you watch long enough, you will see behaviors I did not describe.

That is the point.

Have fun — and never stop experimenting.

