# Hangul Character Recognition (한글 문자 인식)
 
> **This is a long-term personal passion project.** As a Korean, I've always been fascinated by how Hangul is built, and this repo is where I explore that through deep learning. Hangul was created in 1443 by King Sejong the Great and promulgated in 1446 as *Hunminjeongeum* (훈민정음), "the correct sounds for instructing the people," so that ordinary people could read and write without mastering thousands of Chinese characters. In terms of language classification, Korean is generally considered a language isolate (or the main member of the small Koreanic family), and Hangul itself is often classified by linguists as a *featural alphabet*: the consonant shapes depict the mouth and tongue positions used to pronounce them, and the vowels are built from three symbols representing heaven (·), earth (ㅡ), and humanity (ㅣ). That deliberate, almost engineered design is exactly what makes Hangul such an interesting problem for machine learning. This project will grow and change over time as I learn, experiment, and add new ideas.
 
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
- **Printed data:** PHD08 [1], a large-scale printed Hangul database covering the 2,350 most common syllables, with 2,187 samples per class (5,139,450 images) varying in font, size, print quality, resolution, binarization, and rotation
- **Handwritten data:** PE92 [2], a handwritten Korean character image database, and Korean handwriting datasets from AI Hub [3]
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
 
## References
 
[1] D. S. Ham, D. R. Lee, I. S. Jung, and I. S. Oh, "Construction of Printed Hangul Character Database PHD08," *The Journal of the Korea Contents Association*, vol. 8, no. 11, pp. 33–40, 2008. Available: https://koreascience.kr/article/JAKO200801440596768.page
 
[2] D. H. Kim et al., "Handwritten Korean Character Image Database PE92," in *Proceedings of the 2nd International Conference on Document Analysis and Recognition (ICDAR '93)*, Tsukuba, Japan, 1993, pp. 470–473. DOI: 10.1109/ICDAR.1993.395693
 
[3] AI Hub, National Information Society Agency (NIA), Republic of Korea. Available: https://aihub.or.kr *(update with the specific dataset name and access date once selected)*
 
---
 
*만들고 배우는 과정을 기록하는 프로젝트입니다.*
