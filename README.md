# 5_ACTIVITY
Laboratory Work 5 Activity-- Comparative Analysis of Pre-trained CNN Models for  Custom Image Classification

🔗 Links
# Google Colab Link: https://colab.research.google.com/drive/1HqRtA5J1wwOC0t_uCh39Yl4Y9UWGaBCX?usp=drive_link
# Google Drive Link: https://drive.google.com/drive/folders/1AaBGBGzdXNWRE60E-AH2BS51eoLV-1vP?usp=drive_link

## 📝 PART 13: Final Reflection & Guide Questions

### **A. Model Performance**
1. **Which pre-trained model achieved the highest accuracy? Why?**
   *MobileNetV2 achieved the highest accuracy.
Accuracy values from v8Iy38gSuWHc:
VGG16: 0.66
MobileNetV2: 0.95
EfficientNetB0: 0.04
Why: MobileNetV2's architecture, specifically designed for mobile and embedded vision applications, appears to be a better fit for feature extraction and learning patterns from your custom dataset, enabling more effective transfer learning compared to VGG16 and especially EfficientNetB0. Its balance of depth and efficiency likely contributed to its superior performance.



2. **Which model had the lowest performance? What could be the reason?**
   * EfficientNetB0 had the lowest performance, with an accuracy of 0.04.
* Reason: The very low accuracy and high validation loss (near 3.0) for EfficientNetB0 (as seen in feLfAhn5uQfD) indicate that it failed to learn effectively from the training data. This could be due to several reasons:
* Training Configuration: The fixed learning rate (0.0001) or other training parameters might not have been suitable for EfficientNetB0's specific characteristics, especially with frozen base layers.
*Architecture Mismatch/Sensitivity: While generally powerful, EfficientNetB0's specific feature extraction layers (when frozen) might not have been well-suited for transferring knowledge to your specific image classes with the current setup. It might be more sensitive to the fine-tuning process.
*Optimization Issues: The model might have gotten stuck in a local minimum during optimization, preventing it from converging to a better solution.


3. **How did loss values compare across models?**
   *MobileNetV2: Achieved the lowest final validation loss of 0.2131, indicating it learned the most effectively and generalized well to unseen data.
*VGG16: Had a moderate final validation loss of 1.8103, showing decent but not outstanding learning.
E*fficientNetB0: Exhibited a very high and stagnant final validation loss of 2.9971, which is close to the initial loss, suggesting almost no learning occurred during its training epochs. This aligns with its extremely low accuracy.


### **B. Evaluation Metrics**
4. **Why is accuracy not enough to evaluate a model?**
   * Accuracy alone can be misleading, particularly in datasets with class imbalance (where some classes have significantly more samples than others). A model can achieve high accuracy by simply predicting the majority class frequently, while performing very poorly on minority classes. Metrics like Precision, Recall, and F1-score provide a more granular view of how well the model performs for each individual class, giving a more complete picture of its strengths and weaknesses.


5. **Which model had the best F1-score? What does it indicate?**
   * Indication: The F1-score is the harmonic mean of Precision and Recall. A high F1-score indicates that the model has a strong balance between Precision (minimizing false positives, i.e., when it predicts a class, it's usually correct) and Recall (minimizing false negatives, i.e., it identifies most of the actual instances of a class). This makes F1-score a robust measure of overall classification effectiveness, especially important in multi-class scenarios or when classes might be imbalanced.



6. **How did Precision and Recall differ across models?**
   * MobileNetV2: Demonstrated consistently high precision (weighted avg: 0.96) and recall (weighted avg: 0.95) across almost all classes, often reaching 0.98-1.00 for both. This indicates excellent performance in both correctly identifying positive instances and minimizing false alarms or missed instances.
   * VGG16: Showed moderate precision (weighted avg: 0.70) and recall (weighted avg: 0.66). There was considerable variability across classes; for example, 19_golden_shower had high recall (0.94) but lower precision (0.43), meaning it found most golden showers but also incorrectly identified other things as golden showers. Conversely, 3_wisteria had high precision (0.90) but very low recall (0.16), meaning when it predicted wisteria, it was usually right, but it missed most actual wisteria plants.
   * EfficientNetB0: Exhibited extremely poor precision (weighted avg: 0.00) and recall (weighted avg: 0.04) for almost all classes. This indicates that the model is either barely making correct predictions for any class or is heavily biased towards predicting a single class incorrectly, leading to a breakdown in meaningful classification.




### **C. Confusion Matrix Analysis**
7. **Which classes were frequently misclassified?**
   * MobileNetV2: Showed very few misclassifications, with most predictions falling on the diagonal. It generally distinguished classes well.
   * VGG16: Several classes were frequently misclassified:
*3_wisteria: Out of 58 actual wisteria images, only 16 were correctly classified, with many being predicted as 1_echeveria, 20_passion_flower, or 12_freesia.
*9_peony: Out of 57 actual peony images, only 14 were correctly classified, with significant confusion with classes like 19_golden_shower, 8_fox_glove, and others.
*19_golden_shower: While it had high recall, its precision was low due to 43 actual 19_golden_shower images being predicted as 10_anemone.
*10_anemone was also frequently confused with 19_golden_shower
*EfficientNetB0: Almost all classes were misclassified. Its confusion matrix showed very few correct predictions for most classes, often predicting samples from other classes as 14_ficus_benjamina, suggesting a strong bias or failure to differentiate.



8. **What patterns did you observe in the confusion matrix?**
   * MobileNetV2: The confusion matrix was dominated by a strong diagonal, with very few off-diagonal values. This pattern indicates that MobileNetV2 successfully classified most images into their correct categories and rarely confused one class for another.
   * VGG16: The confusion matrix showed more scattered off-diagonal values. This indicates that VGG16 struggled with distinguishing visually similar classes, or certain classes were harder to learn. Specifically, classes like 3_wisteria and 9_peony were frequently misclassified across multiple other categories, suggesting VGG16 failed to learn robust features for these classes. There was also a notable unidirectional confusion where 19_golden_shower was often misclassified as 10_anemone.
   * EfficientNetB0: The confusion matrix for EfficientNetB0 revealed a catastrophic failure in classification. The diagonal was almost empty, with a strong bias towards predicting only one class (14_ficus_benjamina) for nearly all inputs, regardless of their true label. This pattern signifies that the model did not learn to differentiate between any of the classes.


### **D. ROC and AUC**
9. **Which model had the highest AUC score?**
   * MobileNetV2 had the highest AUC scores across the board.
   * From the ROC Curve plots in cell mvkGs89atYsA, MobileNetV2 shows almost all classes with AUC values of 0.99 or 1.00, indicating near-perfect separability between classes.
   * VGG16's AUC scores ranged mostly from 0.80 to 0.99, with more variability.
   * Given EfficientNetB0's overall poor performance, its AUC scores would be expected to be very low, likely close to 0.5 (random guessing), although its specific plot was truncated.


10. **What does AUC tell us about model performance?**
    * AUC (Area Under the Receiver Operating Characteristic Curve) is a metric that measures the ability of a classifier to distinguish between classes. It quantifies how well the model can differentiate between positive and negative classes across all possible classification thresholds. An AUC value of 1.0 indicates a perfect classifier, while an AUC of 0.5 suggests a model performing no better than random guessing. A higher AUC signifies better overall discriminative power, meaning the model is more effective at ranking positive instances higher than negative instances.


### **E. Explainability (Grad-CAM)**
11. **What did Grad-CAM reveal about model decision-making?**
    * The Grad-CAM visualizations (from cell ZHqciwvgtkTF) for the sample 5_impatiens image revealed:
    * MobileNetV2: Showed a more focused and localized heatmap, concentrating on the central parts of the flowers. This suggests the model was primarily attending to the most discriminative visual features of the flower itself to make its classification decision.
    * VGG16: Produced a heatmap that was somewhat focused on the flowers but also extended to surrounding regions and edges, indicating a broader, less precise area of attention for its decision.
    * EfficientNetB0: Generated a very diffuse and widespread heatmap that covered much of the image without clear localization on the object. This is consistent with its failure to classify, as it doesn't appear to be focusing on relevant features at all.


12. **Did the model focus on relevant image regions?**
    *MobileNetV2: Yes, it clearly focused on the relevant parts of the 5_impatiens flowers, which are the key features for identification.
    * VGG16: Partially. It showed some attention to the flowers but also considered broader, less specific regions, suggesting a less precise focus on the object of interest.
    * EfficientNetB0: No, its heatmap was too broad and lacked specific focus on the actual 5_impatiens flowers, indicating it was not leveraging the correct visual cues for classification.


13. **Which model produced the most meaningful heatmaps?**
    * MobileNetV2 produced the most meaningful heatmaps. Its Grad-CAM visualizations were more precise, highlighting the most relevant and discriminative visual features of the objects being classified. This indicates that MobileNetV2 is learning more semantically relevant features and has a better understanding of what constitutes a particular class.


### **F. Model Comparison & Improvement**
14. **Which model would you recommend for deployment? Why?**
    * Based on a holistic evaluation of all metrics, MobileNetV2 is strongly recommended for deployment.
    * why:
    * Superior Performance: It achieved the highest accuracy (0.95), best F1-score (0.96 weighted avg), and highest AUC scores (mostly 0.99-1.00) across nearly all classes, demonstrating excellent overall classification capability.
    * Clear Classification: Its confusion matrix showed minimal misclassifications, indicating robust discrimination between classes.
    * Explainability: Grad-CAM results confirmed that MobileNetV2 focused on relevant image regions, suggesting it learned meaningful features.
    * Efficiency: MobileNetV2 models are generally more lightweight and computationally efficient than VGG16, making them more suitable for real-world deployment, especially in resource-constrained environments like mobile or edge devices.
      

15. **How can you further improve your best-performing model?**
    *  To further enhance the MobileNetV2 model, you can implement several strategies:
    *  Fine-tuning: Instead of just freezing the base model, unfreeze some of the upper layers of the MobileNetV2 base and train them with a very low learning rate. This allows the pre-trained features to be adapted more specifically to your custom dataset.
* Hyperparameter Optimization: Conduct a more thorough search for optimal hyperparameters, including different learning rates (perhaps with learning rate schedules), optimizers (e.g., AdamW, SGD with momentum), batch sizes, and dropout rates.
*Advanced Data Augmentation: Employ more aggressive data augmentation techniques (e.g., CutMix, Mixup, RandAugment) to increase the diversity and effective size of your training data, improving generalization.
*Regularization: If any signs of overfitting appear (e.g., validation loss increasing while training loss decreases), consider adding more dropout layers or L1/L2 regularization.
*Ensemble Methods: Train multiple instances of MobileNetV2 (with different random initializations or slight variations) or combine it with other strong models, then average their predictions for potentially higher robustness and accuracy.
*Larger/More Diverse Dataset: If feasible, expanding the dataset with more images per class or introducing more variety within each class can significantly improve performance.

.

### **G. Real-World Application**
16. **How can your model be applied in real-world scenarios?**
    *  Given the nature of the image dataset (presumably involving plants/flowers based on impatiens in Grad-CAM), this model can be applied in various real-world scenarios:
    *  Automated Plant/Flower Identification Apps: Users can take a picture of a plant or flower, and the app identifies the species, useful for gardening, botany enthusiasts, or educational purposes.
*Agricultural Monitoring: Detecting specific crop types or identifying plant diseases/pests from images captured by drones or field cameras, aiding farmers in precision agriculture.
*Botanical Inventory and Conservation: Assisting researchers or conservationists in cataloging and monitoring plant species in ecosystems.
*Retail/E-commerce: Identifying plants or flowers from images for online shopping, allowing customers to easily find and purchase specific species.


17. **What are the risks of deploying an inaccurate model?**
    * Deploying an inaccurate model can lead to significant negative consequences, depending on the application:
    * Financial Losses: In agriculture, misidentification of crops or diseases could lead to incorrect treatments, resulting in crop damage or reduced yields. In retail, wrong product identification could lead to incorrect inventory management or customer dissatisfaction.
*Reputational Damage: A public-facing application that frequently provides incorrect classifications will quickly lose user trust and adoption.
*Inefficiency: If the model's predictions constantly require human oversight and correction, it negates the benefits of automation and can even slow down existing workflows.
*Safety Hazards: In more critical applications (though less direct for plant classification), inaccurate models could lead to severe outcomes (e.g., misidentifying edible vs. poisonous plants, if the scope were to expand).
*Bias Reinforcement: If the training data was biased, an inaccurate model could perpetuate and amplify those biases in real-world applications.


18. **How can this system be integrated into a mobile/web app?**
    * Mobile Application Integration:
*On-Device Inference (TensorFlow Lite): The trained Keras model (.keras file) can be converted into a TensorFlow Lite (.tflite) format. This optimized format allows the model to run directly on mobile devices (iOS via Swift/Objective-C, Android via Java/Kotlin) with low latency and reduced resource consumption. The mobile app captures an image, processes it, and feeds it to the embedded .tflite model for immediate classification.
*Cloud API Inference: The mobile application can capture an image and then send it to a backend server (e.g., built using Python frameworks like Flask or FastAPI) where the full TensorFlow model is deployed as a REST API. The server performs the image classification and sends the prediction back to the mobile app.
*Web Application Integration:
Backend API Inference: Similar to the cloud API for mobile, a web application (frontend built with frameworks like React, Angular, Vue.js) sends captured or uploaded image data to a backend server (e.g., Python, Node.js) hosting the TensorFlow model. The server handles inference and returns the results to the web client.
*Client-Side Inference (TensorFlow.js): For web applications, the Keras model can be converted to TensorFlow.js format. This allows the model to run entirely within the user's web browser, leveraging their local computational resources. This approach reduces server load, improves responsiveness, and can work offline. The JavaScript code in the browser handles image input, runs the model, and displays predictions. This is particularly suitable for smaller, less computationally intensive models like MobileNetV2.

