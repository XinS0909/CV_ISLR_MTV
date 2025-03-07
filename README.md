# Cross-View Isolated Sign Language Recognition via View Synthesis and Feature Disentanglement

Cross-view isolated sign language recognition (CV-ISLR) addresses the challenge of identifying isolated signs from viewpoints unseen during training, a problem aggravated by the scarcity of multi-view data in existing benchmarks. 
To bridge this gap, we introduce a novel two-stage framework comprising **View Synthesis** and **Contrastive Multi-task View-Semantics Recognition**.
In the View Synthesis stage, we simulate unseen viewpoints by extracting 3D keypoints from the frontal-view training dataset and synthesizing common-view 2D skeleton sequences with virtual camera rotation, which enriches view diversity without the cost of multi-camera setups.
However, direct training on these synthetic samples leads to limited improvement, as viewpoint-specific and semantics-specific features remain entangled.
To overcome this drawback, the Contrastive Multi-task View-Semantics Recognition stage employs the cross-attention mechanism and contrastive learning objective to explicitly disentangle viewpoint-related information from sign semantics, thus obtaining robust view-invariant representations.
We evaluate our approach on the MM-WLAuslan dataset, the first benchmark for CV-ISLR, and on our extended protocol (**MTV-Test**) that includes additional multi-view data captured in the wild. 
Experimental results demonstrate that our method not only improves the accuracy of frontal-view skeleton-based isolated sign language recognition, but also exhibits superior generalization to novel viewpoints.
 
 
## The challenges of CV-ISLR task.
Demonstration of the viewpoint discrepancy in Cross-View Isolated Sign Language Recognition (CV-ISLR), where the top row shows a training ''alphabet'' sample and the bottom row illustrates a testing ''alphabet'' sample captured from a different perspective. 
The highlighted areas emphasize challenges such as self-occlusion and hand shape variations.

<p align="center">
<img src="Imgs/cv_islr.png" alt="Illustration of the CV-ISLR challenges." title="Illustration of the CV-ISLR challenges." width="1500">
</p>
  
## Multi-View Test set (MTV-Test).
MM-WLAuslan is currently the only dataset designed explicitly for Cross-View Isolated Sign Language Recognition (CV-ISLR). 
In contrast to traditional ISLR datasets—often restricted to a single viewpoint—MM-WLAuslan provides multiple test subsets, which allow benchmarking under various constraints. 
However, these subsets mostly involve small yaw angles and predominantly rely on controlled sensor environments, limiting their ability to reflect broader real-world complexity. 
Additionally, the use of specialized RGB-D devices does not fully emulate the ubiquitous consumer-grade cameras found in daily life scenarios.
         
To address these gaps, we propose **MTV-Test**, a test set that substantially extends cross-view and environmental diversity beyond what is currently offered by MM-WLAuslan. 
We recruit 30 participants, including Auslan experts, Deaf signers, and volunteers, ensuring a wide range of signing styles. 
Each participant is instructed on recommended camera angles, gloss lists, and recording procedures. 
Unlike MM-WLAuslan's reliance on RGB-D sensors, our data is collected using consumer-grade devices such as smartphones (e.g., iPhone and Samsung) and webcams (e.g., Logitech C922 Pro), aligning with real-world usage scenarios.
We show some data [here](https://github.com/XinS0909/CV_ISLR_MTV/tree/main/MTV_Test).

<p align="center">
<img src="Imgs/mtv.png" alt="Multi-View Test set (MTV-Test)." title="Multi-View Test set (MTV-Test)." width="1500">
</p>



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
<img src="Imgs/data_aug.png" alt="Multi-View Test set (MTV-Test)." title="Multi-View Test set (MTV-Test)." width="1500">
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
<img src="Imgs/CMVSR.png" alt="Multi-View Test set (MTV-Test)." title="Multi-View Test set (MTV-Test)." width="1500">
</p>




