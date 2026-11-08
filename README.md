# Hangul Character Recognition (한글 문자 인식)

> **This is a long-term personal passion project.** As a Korean, I've always been fascinated by how Hangul is built, and this repo is where I explore that through deep learning. It will grow and change over time as I learn, experiment, and add new ideas.

---

## About the Project

Hangul is one of the most systematically designed writing systems in the world. Every syllable block is composed of smaller letters called **jamo**:

| Component | Options | Example (한) |
|---|---|---|
| Initial consonant (초성) | 19 | ㅎ |
| Vowel (중성) | 21 | ㅏ |
| Final consonant (종성) | 27 + none | ㄴ |

Together these form **11,172 possible syllables**. Many are rare, and some never appear in typical datasets at all.

Instead of treating recognition as a giant 11,172-class problem, this project explores models that understand Hangul's compositional structure, recognizing each jamo separately and assembling them into syllables.

## Core Question

**Can a model read Hangul syllables it has never seen during training** by composing jamo it learned from other characters?

## Approach

- **Baseline:** a standard CNN classifier over all syllable classes
- **Jamo model:** a shared backbone with three output heads predicting the initial, vowel, and final jamo separately
- **Compositional test:** deliberately hold out a set of syllables during training and evaluate whether each model can recognize them
- **Interpretability:** visualize where the model attends when predicting each jamo, to see whether it learns the block layout on its own

## Data

- **Synthetic data:** characters rendered in a variety of Korean fonts with random distortions, giving full control over which syllables appear in training
- **Handwritten data:** public datasets such as PHD08 and AI Hub Korean handwriting data
- **Personal test set (planned):** real handwriting samples collected from family and friends

## Roadmap

- [ ] Synthetic dataset generator
- [ ] Baseline flat classifier
- [ ] Three-head jamo model
- [ ] Held-out syllable (compositional generalization) experiments
- [ ] Attention / saliency visualizations
- [ ] Evaluation on real handwriting
- [ ] Future ideas: few-shot Korean font generation, historical documents, scene text

## Project Structure (planned)

```
├── data/           # dataset generation and loading
├── models/         # model architectures
├── experiments/    # training configs and results
├── notebooks/      # exploration and visualizations
└── README.md
```

## Status

🚧 Early development. This is an ongoing personal project, so expect frequent changes as it evolves.

---

*만들고 배우는 과정을 기록하는 프로젝트입니다.*
