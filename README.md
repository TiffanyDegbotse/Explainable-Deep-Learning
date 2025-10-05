# 🧠 Explainable Deep Learning – Grad-CAM Analysis on CIFAR-10

This repository contains the implementation and analysis for an explainability experiment using Grad-CAM and its variants (Grad-CAM++ and Score-CAM) applied to a pretrained ResNet-50 model. The goal of this project is to understand how deep learning models interpret visual cues related to transportation and mobility while testing their robustness on low-resolution images. This project explores how pretrained computer vision models, originally trained on high-quality ImageNet data, interpret and focus on relevant visual regions when exposed to low-resolution images from the CIFAR-10 dataset. Using Grad-CAM visualizations, we analyze how model attention shifts across different classes and how interpretability reveals model reasoning even when predictions are inaccurate.

The main objective is to examine how ResNet-50 focuses on image regions associated with airplanes, automobiles, ships, trucks, and horses, all representing different forms of transportation and movement. By comparing Grad-CAM variants, the experiment highlights how explainability techniques differ in sensitivity and localization, offering insights into model stability under domain shift.

The CIFAR-10 dataset contains 60,000 low-resolution (32×32) color images across 10 classes. The classes used in this experiment include airplane, automobile, ship, truck, and horse. CIFAR-10 simulates realistic low-quality conditions such as blurry or compressed traffic footage, making it a strong proxy for testing explainability under imperfect visual inputs.

**Dataset citation:**  
Krizhevsky, A. (2009). *Learning Multiple Layers of Features from Tiny Images (CIFAR-10).* University of Toronto. [https://www.cs.toronto.edu/~kriz/cifar.html](https://www.cs.toronto.edu/~kriz/cifar.html)

The model used is a pretrained ResNet-50 from Torchvision, trained on the ImageNet-1K dataset. This model is used without fine-tuning to evaluate how well it generalizes to lower-resolution images and different data distributions. Images were normalized with the ImageNet mean and standard deviation values:

`mean = [0.485, 0.456, 0.406]`  
`std  = [0.229, 0.224, 0.225]`

These values ensure that inputs match the scale and distribution expected by ResNet-50, which was trained on ImageNet.

**Model citation:**  
He, K., Zhang, X., Ren, S., & Sun, J. (2016). *Deep Residual Learning for Image Recognition.* In *Proceedings of the IEEE Conference on Computer Vision and Pattern Recognition (CVPR)*, 770–778. [https://pytorch.org/vision/stable/models/generated/torchvision.models.resnet50.html](https://pytorch.org/vision/stable/models/generated/torchvision.models.resnet50.html)

The experiment followed four main steps. First, the CIFAR-10 test set was loaded with ImageNet normalization, and images were resized from 32×32 to 224×224 to match ResNet-50’s input requirements. Second, pretrained ResNet-50 was used to predict each selected image class, logging both CIFAR-10 ground truth and predicted ImageNet labels. Third, Grad-CAM, Grad-CAM++, and Score-CAM were implemented using the model’s last convolutional layer to visualize model attention maps overlayed on the original images. Finally, results were compared across five representative samples: an airplane (predicted as “can opener”), an automobile (predicted as “moving van”), a ship (correctly classified), a truck (predicted as “moving van”), and a horse (predicted as “packet”). These comparisons revealed differences in how each CAM variant highlights visual features.

The airplane image was misclassified as “can opener,” but Grad-CAM still correctly highlighted the airplane’s body, showing reliable attention despite the incorrect label. The automobile was identified as a “moving van,” which is semantically reasonable within the same category, and its wheels were consistently emphasized across all three methods. The ship was correctly identified; Grad-CAM and Grad-CAM++ focused on the base and back of the ship, while Score-CAM emphasized the entire body. For the truck, Grad-CAM and Grad-CAM++ highlighted the headlights and door, whereas Score-CAM focused on the opposite side of the vehicle. Finally, the horse image showed that Grad-CAM and Grad-CAM++ concentrated on the legs and part of the body, while Score-CAM highlighted the entire horse but still resulted in a “packet” prediction.

Even when predictions were incorrect, Grad-CAM heatmaps aligned with meaningful regions of interest. Score-CAM produced broader, smoother attention maps, while Grad-CAM++ refined specific activation areas. The experiment demonstrates that explainability methods remain valuable in understanding model reasoning under imperfect conditions.

Even when ResNet-50 misclassified low-resolution CIFAR-10 images, Grad-CAM and its variants consistently provided interpretable attention maps. Explainability revealed the model’s focus on meaningful features such as object shapes and key parts (wings, wheels, or body outlines), demonstrating that visual reasoning can remain stable even when final classifications are off. This project highlights the importance of explainability in computer vision applications, especially in safety-critical domains such as autonomous driving and transportation monitoring.

**How to Run:**  
1. Open the notebook directly in Google Colab using the link included in this repository.  
2. Install dependencies:  
3. Run all notebook cells in order.  
4. Grad-CAM visualizations will appear for the five selected CIFAR-10 images.

**References:**  
- Krizhevsky, A. (2009). *Learning Multiple Layers of Features from Tiny Images (CIFAR-10).* University of Toronto.  
- He, K., Zhang, X., Ren, S., & Sun, J. (2016). *Deep Residual Learning for Image Recognition.* CVPR.  
- Selvaraju, R. R., Cogswell, M., Das, A., Vedantam, R., Parikh, D., & Batra, D. (2017). *Grad-CAM: Visual Explanations from Deep Networks via Gradient-Based Localization.* ICCV.

**Author:** Tiffany A. Degbotse  
**Course:** AIPI 590 – Explainable Deep Learning  
**Institution:** Duke University, Pratt School of Engineering  
**Created in:** Google Colab  
