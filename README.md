# Hangul Character Recognition (한글 문자 인식)
 
As a Korean, I've always been interested in how Hangul works, particularly how its characters are constructed. I wanted to explore that interest through deep learning and see what I could build with it. This is a long-term personal project that I'll continue to expand and improve as I learn new deep learning techniques.

Hangul was created by King Sejong in 1443 and introduced in 1446 as Hunminjeongeum (훈민정음). It was designed to make reading and writing easier for ordinary people, without requiring them to learn thousands of Chinese characters. One thing I find interesting is how the writing system is structured. The consonants are shaped around the positions of the mouth and tongue when making each sound, while the vowels are built from three symbols representing heaven (·), earth (ㅡ), and humanity (ㅣ). Because of this, Hangul is often described as a featural alphabet. 

That underlying structure makes Hangul an interesting subject for machine learning. I want to experiment with different deep learning approaches, explore how the writing system can be represented computationally, and see where the project takes me. I'll continue building on it as I learn and come across new ideas.
 
---
 
## About the Project
 
Every Hangul syllable block is composed of smaller letters called **jamo**:
 
| Component | Options | Example (한) |
|---|---|---|
| Initial consonant (초성) | 19 | ㅎ |
| Vowel (중성) | 21 | ㅏ |
| Final consonant (종성) | 27 + none | ㄴ |
 
Together these form **11,172 possible syllables**. Many are rare, and some never appear in typical datasets at all.
 
Instead of treating recognition as one giant classification problem, this project explores a model that understands Hangul's compositional structure, recognizing each jamo separately and assembling them into syllables.
 
To keep the first version focused, the project starts with **printed characters** and the **2,350 most commonly used syllables**.
 
## Core Question
 
**Can a model read Hangul syllables it has never seen during training** by composing jamo it learned from other characters?
 
## Approach
 
- **Baseline:** a small CNN that classifies each image directly as one of the syllable classes
- **Jamo model:** the same CNN backbone with three output heads predicting the initial consonant, vowel, and final consonant separately
- **Compositional test:** deliberately hold out a set of syllables during training (while making sure each of their jamo still appears in other syllables), then compare how well each model recognizes them
## Data
 
- **Synthetic data (primary):** 64×64 grayscale images of characters rendered in a variety of Korean fonts with random distortions, giving full control over which syllables appear in training
- **Printed data (optional):** PHD08 [1], a large-scale printed Hangul database covering the 2,350 most common syllables, with 2,187 samples per class (5,139,450 images) varying in font, size, print quality, resolution, binarization, and rotation
## Tech Stack
 
- **PyTorch** for models and training
- **Pillow** for rendering fonts into images
- **NumPy / Matplotlib** for analysis and plots
## Roadmap
 
- [ ] Synthetic dataset generator
- [ ] Baseline flat classifier
- [ ] Three-head jamo model
- [ ] Held-out syllable (compositional generalization) experiments
- [ ] Write up results
## Future Ideas
 
Once the core experiment is complete, possible next steps include:
 
- Attention / saliency visualizations to see whether the model learns the block layout on its own
- Comparing the CNN with a Vision Transformer
- Extending to all 11,172 syllables
- Handwritten data, such as PE92 [2] and AI Hub datasets [3], plus a personal test set of handwriting from family and friends
- Reading old Korean texts and historical documents
## Project Structure (planned)
 
```
├── data/           # dataset generation and loading
├── models/         # model architectures
├── experiments/    # training configs and results
├── notebooks/      # exploration and visualizations
└── README.md
```
 
## References
 
[1] D. S. Ham, D. R. Lee, I. S. Jung, and I. S. Oh, "Construction of Printed Hangul Character Database PHD08," *The Journal of the Korea Contents Association*, vol. 8, no. 11, pp. 33–40, 2008. Available: https://koreascience.kr/article/JAKO200801440596768.page
 
[2] D. H. Kim et al., "Handwritten Korean Character Image Database PE92," in *Proceedings of the 2nd International Conference on Document Analysis and Recognition (ICDAR '93)*, 1993, pp. 470–473. DOI: 10.1109/ICDAR.1993.395693
 
[3] AI Hub, National Information Society Agency (NIA), Republic of Korea. Available: https://aihub.or.kr *(update with the specific dataset name and access date once selected)*
 
---
 
*만들고 배우는 과정을 기록하는 프로젝트입니다.*
 
