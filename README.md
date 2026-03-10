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
| Attack          | PSNR    | SSIM   | NC     |
| --------------- | ------- | ------ | ------ |
| Gaussian 0.01   | 38.2972 | 0.9662 | 0.9816 |
| Gaussian 0.02   | 33.6340 | 0.8957 | 0.9632 |
| Blur 1          | 28.7396 | 0.9139 | 0.9810 |
| Blur 2          | 23.8256 | 0.7413 | 0.9631 |
| Crop 0.9        | 15.7280 | 0.3827 | 0.7422 |
| Crop 0.8        | 14.2275 | 0.2730 | 0.7260 |
| Rotate 5°       | 15.4045 | 0.4792 | 0.8894 |
| Rotate -5°      | 15.9748 | 0.4755 | 0.8766 |
| Rotate 10°      | 12.9657 | 0.3163 | 0.6969 |
| JPEG 90         | 33.8860 | 0.9584 | 0.9673 |
| JPEG 80         | 32.1468 | 0.9402 | 0.9310 |
| Resize 0.8      | 31.9128 | 0.9601 | 0.9825 |
| Resize 0.6      | 29.8982 | 0.9361 | 0.9814 |
| Flip Horizontal | 8.9445  | 0.1854 | 0.2450 |
| Flip Vertical   | 11.3137 | 0.1677 | 0.2850 |
| Pixelate 2x2    | 24.2807 | 0.8402 | 0.9733 |


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
