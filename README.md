📊 Learning an Unknown Probability Density Function using GANs
📌 Project Overview

This project demonstrates a data-driven approach to learning an unknown probability density function (PDF) using a Generative Adversarial Network (GAN).
Instead of assuming any analytical or parametric distribution (such as Gaussian or exponential), the PDF is learned purely from data samples.

The experiment is conducted on real-world NO₂ (Nitrogen Dioxide) concentration data from India’s air quality dataset. A nonlinear transformation is applied to the original feature, and a GAN is trained to model the resulting distribution implicitly.

This project highlights the use of GANs beyond image generation, specifically for probability density estimation from raw data alone.

🎯 Objectives

Transform a real-world feature using a nonlinear function

Assume no prior knowledge of the resulting distribution

Train a GAN to learn the distribution only from samples

Generate synthetic samples from the trained generator

Approximate the learned PDF using Kernel Density Estimation (KDE)

Compare the real and learned distributions visually

📂 Dataset Description

Dataset: India Air Quality Data

Source: Kaggle

Feature Used: NO₂ (Nitrogen Dioxide concentration)

Reason for Choosing NO₂:

Continuous-valued real-world data

Non-Gaussian behavior

Suitable for density learning tasks

The code automatically handles:

Unknown CSV file names

Non-UTF8 file encodings

Inconsistent column naming (e.g., "NO2", "NO2 (µg/m3)", etc.)

🔄 Data Transformation

Each NO₂ value 
𝑥
x is transformed into a new variable 
𝑧
z using:

𝑧
=
𝑥
+
𝑎
𝑟
sin
⁡
(
𝑏
𝑟
𝑥
)
z=x+a
r
	​

sin(b
r
	​

x)

Where:

𝑎
𝑟
=
0.5
×
(
𝑟
 
m
o
d
 
7
)
a
r
	​

=0.5×(rmod7)
𝑏
𝑟
=
0.3
×
(
(
𝑟
 
m
o
d
 
5
)
+
1
)
b
r
	​

=0.3×((rmod5)+1)

𝑟
r is the university roll number

This nonlinear transformation ensures the resulting distribution has no known analytical form

🧠 Why GANs?

Traditional density estimation methods often assume:

A known distribution family

A fixed parametric form

In this task:

The distribution of 
𝑧
z is unknown

No parametric PDF is allowed

GANs solve this by:

Learning distributions implicitly

Using adversarial training instead of likelihood estimation

Generating samples that resemble the true data distribution

🏗️ GAN Architecture
Generator

Input: Gaussian noise 
∼
𝑁
(
0
,
1
)
∼N(0,1)

Output: Synthetic samples 
𝑧
𝑓
z
f
	​


Architecture: Fully connected neural network with ReLU activations

Discriminator

Input: Real samples 
𝑧
z or generated samples 
𝑧
𝑓
z
f
	​


Output: Probability of being real

Architecture: Fully connected neural network with Sigmoid output

Training Objective

Discriminator learns to distinguish real vs fake samples

Generator learns to fool the discriminator

🧪 Training Details

Framework: PyTorch

Loss Function: Binary Cross-Entropy

Optimizer: Adam

Epochs: 3000

Batch Size: 128

Stabilization:

Data standardization

Simple MLP architecture

Controlled learning rate

📈 PDF Approximation

After training:

A large number of samples are generated from the generator

The probability density function is approximated using:

Kernel Density Estimation (KDE)

The estimated PDF is compared with the real transformed data PDF

This allows visual and qualitative evaluation of how well the GAN has learned the distribution.

🔍 Results & Observations
✅ Mode Coverage

The GAN successfully captures the major modes of the transformed distribution

Minor modes are slightly smoothed, which is expected in KDE-based estimation

✅ Training Stability

Training remains stable without mode collapse

Loss values converge smoothly over epochs

✅ Quality of Generated Distribution

Strong overlap between real and GAN-generated PDFs

Small deviations observed in low-density tail regions

Overall shape and spread are well preserved

⚠️ Key Challenges Handled

Inconsistent column naming across datasets

Non-UTF8 encoded CSV files

Unknown dataset file paths in Kaggle

Real-world missing values

All issues are handled programmatically to ensure robustness and reproducibility.

🚀 How to Run

Open the notebook in Kaggle

Attach the India Air Quality dataset

Run all cells

Observe:

GAN training logs

Final PDF comparison plot

No manual file path or column edits are required.

🧩 Key Takeaways

GANs can be effectively used for probability density estimation

No analytical PDF assumption is required

Real-world data introduces challenges that must be handled carefully

Density learning is a powerful application of generative models beyond vision tasks

📌 Future Extensions

Use Wasserstein GAN (WGAN) for improved stability

Compare KDE with histogram-based density estimation

Extend to multivariate density learning

Apply to other environmental or sensor datasets

👤 Author

Archit Arora
B.Tech Computer Engineering
Thapar Institute of Engineering and Technology
