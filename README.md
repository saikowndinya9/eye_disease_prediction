## 🗺️ Workflow

```mermaid
flowchart TD
    A[Data Acquisition] --> B[Preprocessing]
    B --> C[Dataset Splitting]
    C --> D[Model Definition<br/>(AlexNet)]
    D --> E[Compilation<br/>(Loss, Optimizer)]
    E --> F[Training & Validation]
    F --> G[Load Best Model]
    G --> H[Evaluation<br/>(Accuracy, F1, Confusion Matrix)]
    H --> I[Prediction & Visualization]
    I --> J[Save & Deploy Model]
```

---

### 🔍 Step-by-Step Breakdown

1. **Data Acquisition**  
   - Gather raw eye images from the dataset (glaucoma, diabetic retinopathy, cataract, and normal eye).  
   - Organize images into respective folders for each disease class:  
     - **Glaucoma**  
     - **Diabetic Retinopathy**  
     - **Cataract**  
     - **Normal**

2. **Preprocessing**  
   - **Resize** all images to `256×256` pixels.  
   - **Normalize** pixel values to [0,1].  
   - (Optional) Apply **augmentation** (rotation, flips) to boost variety.

3. **Dataset Splitting**  
   - Split the data into **Training** (e.g. 70%), **Validation** (15%), and **Test** (15%) sets.  
   - Use stratified sampling to maintain class balance across splits.

4. **Model Definition (AlexNet)**  
   - Instantiate a Keras `Sequential` model based on AlexNet:  
     - Multiple `Conv2D` + `ReLU` layers  
     - Local response normalization or `BatchNormalization`  
     - `MaxPooling2D` layers  
     - Fully-connected (`Dense`) layers  
   - Adapt the final `Dense` layer to classify the **4 eye disease categories** using softmax activation.

5. **Compilation**  
   - Loss: `categorical_crossentropy`  
   - Optimizer: `Adam` (or SGD with momentum)  
   - Metrics: `accuracy`, plus track **F1-score** via callbacks or `tf.keras.metrics`.

6. **Training & Validation**  
   - Train for **N** epochs (e.g. 30–50), monitoring validation loss.  
   - Use `ModelCheckpoint` to save the best weights and `EarlyStopping` to prevent overfitting.

7. **Load Best Model**  
   - Reload the checkpoint with the lowest **validation loss**.

8. **Evaluation**  
   - Compute **accuracy**, **precision**, **recall**, **F1-score** on the test set.  
   - Plot a **confusion matrix** to visualize performance across all 4 categories.

9. **Prediction & Visualization**  
   - Run inference on **new eye images** (e.g., frames from your demo video).  
   - Overlay predicted labels (glaucoma, diabetic retinopathy, cataract, normal) and confidence scores.

10. **Save & Deploy**  
    - Export final model as `.h5` or TensorFlow SavedModel.  
    - (Optional) Deploy via a Flask/FastAPI app or convert to TensorFlow Lite for mobile/edge deployment.
    
11. **Appendix**

    -Data Set Link : https://www.kaggle.com/datasets/gunavenkatdoddi/eye-diseases-classification
    -Project files link : https://drive.google.com/drive/folders/1H6Oz5bkV_sjR9PGECFKMO-PPNOKDiBvx?usp=sharing
    -Demo Video Link : https://drive.google.com/file/d/1LGFCxoieI-wxP-r6e-yPCia_GQzZ1QT7/view?usp=sharing
