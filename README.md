The project focused on automating the identification of springtails (Collembola) using deep learning. 🧠 These tiny organisms are especially challenging to recognize due to their minuscule size, very subtle morphological differences, and the need for high magnification under a microscope. 🔬

We worked with 1,117 images, each annotated with YOLO+ bounding boxes and labeled (0–8) by four experts—labels that often conflicted. 📊

Objectives 🎯

Predict the springtail classes on the unlabeled test set and evaluate performance via the macro F1 score on Kaggle.

Infer the true species labels in the training set from the available (and sometimes conflicting) annotations.

Key challenges ⚠️

High variability across images (resolution, quality, lighting).

Noisy training labels due to discrepancies between experts.

Dominance of the majority “other” class (0), which is visually hard to distinguish from target species.

YOLO+ annotation errors: some images contained specimens even though they were supposed to depict only the background.
