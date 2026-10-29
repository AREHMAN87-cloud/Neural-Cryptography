# Neural Cryptography Using GANs and CNNs

A deep learning-based neural cryptography project that explores secure communication using Generative Adversarial Networks (GANs) and Convolutional Neural Networks (CNNs). The system trains neural networks to learn encryption and decryption strategies, enabling Alice and Bob to communicate securely while Eve attempts to intercept and decipher the transmitted information.

The project achieved approximately **99% encryption performance**, while limiting Eve's decryption capability to around **40%**, demonstrating how adversarial learning can be applied to neural network-based cryptographic systems.

Data Handling & Dataset Generation:

The model utilizes on-the-fly synthetic data generation during training rather than loading a large, fixed static dataset from disk. Random binary messages and keys are continuously regenerated in memory on every single iteration, exposing the networks to millions of unique combinations over time.

The 512-Row CSV File on GitHub

You may notice a CSV file in this repository containing exactly 512 rows. This file does not represent the full dataset used to train the neural networks. Instead:
• Batch Snapshot: The CSV is a standalone export of a single training batch (\(N = 512\)).
• Structure: Each row contains a randomly generated 16-bit message and its corresponding 16-bit symmetric key, filled with binary values (0 or 1) via np.random.randint.
• Purpose: It is provided strictly for reproducibility, code testing, and quick structural inspection without needing to run the full training loop.

Scaling up to 1M+ Training Examples

During actual training, the dataset scales dynamically in memory through the following pipeline:
• Step 1: Batch Creation (\(512\) examples) — The gen_data() function generates a fresh batch of 512 random 16-bit messages and keys.
• Step 2: Continuous Iteration (\(\times 2,000\) loop) — The training loop runs for 2,000 iterations per epoch. The code drops the previous batch and generates a brand-new one at each step.
• Step 3: Total Training Exposure (\(1.024\text{M}\) examples) — Alice and Bob train on a total of \(512 \times 2,000 = 1,024,000\) unique synthetic examples per epoch without overwhelming system memory.
(Note: To accelerate adversarial learning, Eve is given twice the batch size (\(1,024\) examples), exposing her to \(2,048,000\) generated examples per epoch).

### Key Features
- Neural network-based encryption and decryption.
- GAN-inspired adversarial training involving Alice, Bob, and Eve.
- CNN-based learning for secure message transformation.
- Evaluation of communication security against an adversarial model.
- Exploration of deep learning approaches to cryptography.

### Technologies
Python · Deep Learning · GANs · CNNs · Neural Networks

### Objective
To investigate how neural networks can learn encryption strategies through adversarial training and evaluate their ability to protect information against an eavesdropping model.
