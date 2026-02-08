## Main Project

Official repository:
https://github.com/FBL10/humor-rlhf

Co-developed with FBL10.

# Humor RLHF — Applying Reinforcement Learning from Human Feedback to Humor Generation

This repository contains the code, data, and experiments for a course project exploring the application of **Reinforcement Learning from Human Feedback (RLHF)** to align a language model toward producing more humorous responses.

The project was conducted as part of the *Reinforcement Learning* course at Polytechnique Montréal.

---

## Overview

The objective of this project is to investigate whether RLHF techniques can be used to transform a standard instruction-following language model into a more **humorous and engaging conversational assistant**.

To achieve this, we combine:

- A **generation model** based on *Microsoft Phi-3-mini-128k-instruct*
- A **reward model** trained to evaluate the “funniness” of generated responses
- A **reinforcement learning algorithm**, Proximal Policy Optimization (PPO), implemented using the **TRL** library

The originality of the project lies in the construction of a reward model based on **BERT**, and its integration with PPO to guide the optimization of the generation model.

---

## Methodology

The project is structured around three main components:

### 1. Reward Model

- Built on **BERT Base**, augmented with a binary classification head
- Predicts the probability that a sentence is *funny* or *not funny*
- Trained on a humor detection dataset containing jokes and serious sentences
- Used as a proxy for human preferences (implicit RLHF)

⚠️ Note: The dataset contains a significant amount of toxic content, especially in the humorous class. Due to time constraints, extensive filtering was not performed.

---

### 2. Generation Model

- Based on **Phi-3-mini-128k-instruct**
- Chosen for its instruction-following abilities and relatively small size
- Fine-tuned using **LoRA** and **quantization** to reduce computational cost

---

### 3. Optimization with PPO (TRL)

Training is performed using the **Transformers Reinforcement Learning (TRL)** library, which provides:

- Trajectory generation from prompts
- Reward evaluation using the reward model
- Advantage estimation (e.g. GAE)
- PPO-based policy updates with clipping and stability controls

A total of **4,500 prompts** were used as initial states:
- 2,500 humor-oriented prompts generated with ChatGPT
- 1,000 serious prompts generated with ChatGPT
- 1,000 factual prompts from the **SciQ** dataset

---

## Evaluation

Evaluation was conducted by comparing rewards obtained by the initial and trained models on unseen prompts.

While the trained model obtained higher reward scores overall, **manual inspection revealed no clear qualitative improvement in humor generation**. This suggests limitations in the reward model or training procedure, highlighting the challenges of aligning language models on subjective criteria such as humor.

---

## Results & Limitations

- The reward model achieved high accuracy on the humor classification task, likely indicating overfitting
- PPO optimization increased reward scores without producing consistently funnier outputs
- Limited computational resources constrained training duration and experimentation

Despite these limitations, the project provides valuable insights into the practical challenges of RLHF for language generation.

---

## Resources

- **Official repository:**  
  https://github.com/FBL10/humor-rlhf

- **Trained model (Hugging Face):**  
  https://huggingface.co/fbl10/humor-rlhf

---

## Acknowledgments

We would like to thank **Sarath Chandar** and the teaching team of the *INF8450AE / Reinforcement Learning* course at Polytechnique Montréal for their guidance and support throughout the project, as well as the teaching assistants for their availability and helpful feedback.

