<h3 align="center"><a href="" style="color:#9C276A">
Cross-View Isolated Sign Language Recognition via<br>
View Synthesis and Feature Disentanglement</a></h3>
<h5 align="center"> 
If our project helps you, please give us a star🌟 on GitHub, that would motivate us a lot!
</h2>


## 💥 News
[2025/6/26] **Cross-View Isolated Sign Language Recognition via View Synthesis and Feature Disentanglement** is accepted by `ICCV 2025` 🎉🎉!

[2025/7/20] Release Multi-View Test (**MTV-Test**) set.

### The challenges of CV-ISLR task.
Demonstration of the viewpoint discrepancy in Cross-View Isolated Sign Language Recognition (CV-ISLR), where the top row shows a training ''alphabet'' sample and the bottom row illustrates a testing ''alphabet'' sample captured from a different perspective. 
The highlighted areas emphasize challenges such as self-occlusion and hand shape variations.

<p align="center">
  <img src="Imgs/cv_islr.png" alt="Illustration of the CV-ISLR challenges." title="Illustration of the CV-ISLR challenges." width="75%">
</p>
  
### Multi-View Test set (MTV-Test).
[MM-WLAuslan](https://proceedings.neurips.cc/paper_files/paper/2024/file/812c59ba55c03a68a10c25017bdb696e-Paper-Datasets_and_Benchmarks_Track.pdf) is currently the only dataset designed specifically for Cross-View Isolated Sign Language Recognition (CV-ISLR). Unlike traditional ISLR datasets with a single viewpoint, it includes multiple test subsets. However, these subsets primarily feature small yaw variations and rely on RGB-D sensors in controlled environments, limiting real-world applicability.

To address these gaps, we introduce MTV-Test, a diverse test set with broader view angles and varied conditions. It includes recordings from 30 participants—Auslan experts, Deaf signers, and volunteers—captured using everyday devices like smartphones and webcams. 

Download: MTV-Test [data](https://drive.google.com/drive/folders/1kkxoCDwlPzYVLiD6NIqL3tJe9LlZdvR-) & [label](https://drive.google.com/drive/folders/1lSTCrSGJF_2C03b54ENnOQud0avfAabT).



## Our proposed two-stage framework.
A promising strategy for CV-ISLR involves synthesizing multi-view data from frontal-view videos, allowing models to learn from a more diverse set of camera angles. 
Nevertheless, we observe that directly training on synthetic multi-view samples yields limited gains, as models tend to encode viewpoint-dependent cues rather than genuinely view-invariant representations. 
To overcome these challenges, we propose a two-stage framework composed of View Synthesis and Contrastive Multi-task View-Semantics Recognition.

### View Synthesis
In the View Synthesis stage, we extract 3D whole-body keypoints from frontal-view training data using methods such as SMPL-X-based models or image-based regression techniques. 
Then, instead of synthesizing multi-view RGB videos, we focus on 2D skeleton sequences that are more efficient to process and less sensitive to background and lighting variations.
Specifically, we rotate a virtual camera to diverse yaw and pitch angles and apply perspective transforms to project the 3D keypoints into their corresponding 2D skeletons. 
This strategy significantly enriches the training data with various viewing directions without the need for expensive multi-camera setups.

<p align="center">
<img src="Imgs/data_aug.png" alt="Multi-View Test set (MTV-Test)." title="Multi-View Test set (MTV-Test)." width="75%">
</p>

### Contrastive Multi-task View-Semantics Recognition

In the Multi-task View-Semantics Recognition stage, our goal is to train robust models on the synthesized multi-view sign data by disentangling viewpoint-specific and semantics-specific features.
First, we utilize a cross-attention mechanism to separate viewpoint and semantic information from entangled sign language embeddings. 
Concretely, we construct triplets of skeleton samples: two sequences that share the same sign semantics but differ in viewpoint, paired with a third sequence that shares the viewpoint but represents different semantics.
Then, we employ a multi-task learning framework that simultaneously predicts sign semantics and viewpoint angles. 
This design ensures that viewpoint features are treated as a distinct learning objective instead of being inadvertently entangled in the sign classification pathway. 
Finally, we apply contrastive learning objectives that align embeddings of similar viewpoints or semantics while separating mismatched ones. 
Our approach encourages the model to learn truly view-invariant sign representations, thereby improving generalization to unseen camera angles.


<p align="center">
<img src="Imgs/CMVSR.png" alt="Multi-View Test set (MTV-Test)." title="Multi-View Test set (MTV-Test)." width="75%">
</p>




