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

<p align="center">
<img src="Imgs/mtv.png" alt="Multi-View Test set (MTV-Test)." title="Multi-View Test set (MTV-Test)." width="1500">
</p>




