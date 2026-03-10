**Deep Learning Image Watermarking**
Overview

This project implements a deep learning–based encoder–decoder neural network to securely embed and extract digital watermarks from images. It is designed to preserve high visual quality while ensuring watermark robustness against common image manipulations, including compression, resizing, rotation, noise, and cropping.
By leveraging modern neural network architectures and perceptual loss metrics, this project aims to enhance digital copyright protection for images.

**Key Features**

Encoder–Decoder Architecture: Learns to hide watermarks in images while maintaining visual fidelity.
Robustness Against Attacks: Tested against Gaussian noise, blur, JPEG compression, resizing, rotations, flips, cropping, and pixelation.

**Evaluation Metrics:**

PSNR (Peak Signal-to-Noise Ratio) – measures similarity between cover and watermarked images.
SSIM (Structural Similarity Index) – evaluates perceptual image quality.
NC (Normalized Correlation) – measures accuracy of watermark extraction.
Visualization: Shows original images, watermarks, watermarked images, extracted watermarks, and robustness results against attacks.

**Dataset**

Cover images: Oxford Pets Dataset
Watermarks: MNIST digits used as sample watermark patterns.
Images are resized to 128x128 pixels for uniformity.

**Model Architecture**
**Embedder (Encoder)**

Concatenates cover image and watermark.
Convolutional layers generate a residual map that embeds the watermark.
Output: watermarked image.

**Extractor (Decoder)**

Recovers the watermark from the watermarked or attacked image.
Convolutional layers followed by adaptive pooling produce extracted watermark of original size (28x28).

**Perceptual Loss Network**

Uses VGG16 features to compute perceptual similarity between original and watermarked images.
Helps maintain high visual quality.

**Training**

Optimizer: Adam (lr=1e-4)
Loss Function: Weighted combination of
Image reconstruction loss (MSE)
Watermark extraction loss (MSE)
Perceptual loss (MSE over VGG features)
Epochs: 30
Batch Size: 8
Training achieves high PSNR, SSIM, and NC, indicating effective watermark embedding and extraction.

**Evaluation & Results**

Clean Images (No Attack)
PSNR: 42.97
SSIM: 0.9973
NC (Clean): 0.9836

**Robustness Against Attacks**

The model has been tested against common image manipulations to evaluate watermark robustness. These include:
Gaussian Noise (e.g., variance 0.01, 0.02)
Blurring (e.g., radius 1–2)
Cropping & Resizing (e.g., 80–90% of original size)
Rotation & Flipping
JPEG Compression (quality 80–90)
Pixelation

**Observations:**

Watermarks are reliably extracted under most mild to moderate distortions.
PSNR and SSIM values remain high for small attacks, ensuring visual fidelity.
Normalized Correlation (NC) values are consistently above ~0.8 on average, indicating robust watermark recovery.
Extreme distortions (like aggressive flips or heavy cropping) may reduce watermark extraction accuracy.

**Average NC across all attacks: 0.8241**

Watermarks remain robust under most attacks, with slightly reduced extraction quality for aggressive distortions like flips or severe cropping.

**Visualization**

Shows a grid of images: cover, watermark, watermarked, extracted, attacked, and extracted after attack.
Bar charts visualize NC for each attack to compare robustness.
Helps assess performance visually and quantitatively.

**Usage**
# Clone repository
git clone https://github.com/yourusername/watermarking-project.git
cd capston project.ipynb

# Install dependencies
pip install -r requirements.txt

# Train the model
python train.py --epochs 30 --batch_size 8 --lr 1e-4

# Embed watermarks
python embed.py --input_folder images/ --watermark mnist.png --output_folder watermarked/

# Extract watermarks
python extract.py --input_folder watermarked/ --output_folder extracted/

# Evaluate robustness
python evaluate.py

**Future Improvements**

Experiment with adversarial training for improved robustness.
Extend the network for video watermarking.
Integrate more complex watermark patterns.
Optimize for real-time applications.
