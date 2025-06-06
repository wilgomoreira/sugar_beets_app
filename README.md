# Sugar Beets Semantic Segmentation with Uncertainty Estimation

This repository contains code and notebooks for semantic segmentation of sugar beet field images, with a focus on uncertainty estimation using imprecise probabilities and conformal prediction.

## Project Structure

```
.gitignore
best_model.pth
calibration_logits.pth
conformal prediction.ipynb
imprecise_probability.ipynb
test_logits.pth
train.ipynb
```

- **train.ipynb**: Prepares the dataset, trains a DeepLabV3 model, and saves the best model and logits for calibration and test sets.
- **imprecise_probability.ipynb**: Applies imprecise probability methods to the model outputs, computes lower bounds, sets class-wise thresholds using quartiles, and evaluates segmentation performance with uncertainty-aware metrics.
- **conformal prediction.ipynb**: Implements conformal prediction for pixel-wise uncertainty estimation, computes nonconformity scores, p-values, and evaluates selective risk and coverage.
- **best_model.pth**: The trained model weights.
- **calibration_logits.pth** / **test_logits.pth**: Saved logits, masks, and images for calibration and test splits.

## Workflow

1. **Data Preparation & Training**
   - Prepare RGB images and color masks, convert masks to class indices.
   - Split data into training, calibration (A & B), and test sets.
   - Train a DeepLabV3 segmentation model on the training set.
   - Save the best model and extract logits/masks/images for calibration and test sets.

2. **Imprecise Probability Analysis**
   - Compute softmax probabilities from logits.
   - Calculate lower bounds for probabilities using entropy-based adjustment.
   - Set class-wise thresholds based on quartiles of lower bounds.
   - Generate conservative predictions and fill uncertain pixels with baseline probabilities.
   - Evaluate using metrics: Average Precision, Brier Score, Expected Calibration Error.

3. **Conformal Prediction Analysis**
   - Compute nonconformity scores for the calibration set.
   - Use histogram-based approximation to compute p-values for test set pixels.
   - Define prediction sets and fallback to baseline predictions when uncertain.
   - Evaluate F1 scores, coverage, and selective risk.

## Requirements

- Python 3.8+
- PyTorch
- torchvision
- scikit-learn
- matplotlib
- seaborn
- tqdm
- OpenCV

Install dependencies with:

```sh
pip install torch torchvision scikit-learn matplotlib seaborn tqdm opencv-python
```

## Usage

1. **Train the Model and Save Logits**
   - Run `train.ipynb` to train the model and save logits for calibration and test sets.

2. **Imprecise Probability Evaluation**
   - Run `imprecise_probability.ipynb` to analyze uncertainty using imprecise probabilities.

3. **Conformal Prediction Evaluation**
   - Run `conformal prediction.ipynb` to analyze uncertainty using conformal prediction.

## Data

- Place your RGB images and label masks in the appropriate directories as referenced in `train.ipynb`.
- The code expects specific naming conventions for images and masks.

## Results

- The notebooks provide visualizations and metrics for both baseline and uncertainty-aware segmentation.
- You can compare the performance and coverage of different uncertainty estimation methods.

## License

This project is for research and educational purposes.

---

For questions or contributions, please open an issue or pull request.