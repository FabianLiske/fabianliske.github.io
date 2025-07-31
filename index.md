---
layout: default
title: Swarm Learning in Medical AI
---

## The Importance of Medical AI

The healthcare sector is under increasing pressure: populations are aging, chronic diseases are on the rise, and many regions face a shortage of medical specialists. Particularly in fields like radiology, pathology, and oncology. Artificial intelligence (AI) offers a powerful way to help close this gap. AI systems can analyze medical images, genomic data, or electronic health records at scale, supporting physicians in diagnosing diseases earlier and more accurately, triaging patients, and even predicting treatment responses [[3](#references)].

In areas with limited access to expert care, AI can act as a virtual second opinion or a diagnostic assistant, helping to reduce disparities in healthcare quality. AI can handle time consuming tasks, such as image annotation or documentation, freeing up valuable time for direct patient interaction [[3](#references)].

While the potential of AI in medicine is widely recognized, its implementation is often slowed. As healthcare is inherently decentralized, data is usually decentralized as well. Data privacy regulations and ethical concerns also hinder the creation of large, centralized datasets for training medical AI models [[3](#references)]. Swarm Learning offers a promising solution to these challenges. It enables collaborative AI development without the need to share raw patient data [[3](#references)].

---

## What is Swarm Learning

In conventional machine learning, especially in healthcare, models are often trained on data that has been centralized. Typically collected and stored in large data centers or cloud platforms. While this setup can be effective, it raises major concerns around data privacy, ownership, and compliance with regulations like GDPR or HIPAA [[3](#references)].

![Fig. 1 - ML Techniques](/docs/assets/images/3_ml-techniken.png)
*Fig 1: ML Techniques [[3]](#references)*

### Local Learning

Every participant can create their own model using their own data (Fig 1a). However this will result in worse models if the amount of data ervery participant has is insufficient, but no data has to be shared[ [1](#references)].

### Centralized Learning

If all data can be centralized the training of a model can also be performed on a central copmute resource, for example in the cloud (Fig 1b). This typically results in better performance than locally trained models [[3](#references)].

### Federated Learning

Federated Learning (FL, Fig 1c) combines Local and Centralized Learning. The models are trained locally on locally stored data and the resulting model parameters are stored on a centralized server. While the users don't need to share their data centrally, there remains a central authority managing the model [[3](#references)].

### Swarm Learning

Swarm Learning (SL) is a decentralized machine learning framework that combines edge computing with blockchain technology to enable secure, privacy-preserving, and collaborative model training [[3](#references)]. Unlike traditional federated learning, which relies on a central server for model coordination and aggregation, Swarm Learning operates without any central authority [[3](#references)]. Instead, it employs a permissioned blockchain network to orchestrate peer-to-peer interactions, allowing participants (nodes) to dynamically join, contribute, and govern the model collaboratively [[3](#references)].

Each participating node in the Swarm Learning network trains a local instance of a machine learning model on its own private data. At predefined synchronization intervals, the model parameters, not the data, are exchanged among the peers. The parameters are merged into a shared global model using a consensus algorithm (typically a weighted average), and the updated parameters are then redistributed to all nodes for the next training iteration [[3](#references)]. This process is governed through smart contracts on a blockchain, which ensures transparency, auditability, and fairness in coordination [[3](#references)].

![Fig. 2 - SL Architecture](/docs/assets/images/2_sll-network.png)
*Fig 2: SL Achritecture [[2]](#references)*

The Swarm Learning framework consists of two key layers:
1. Application layer - containing the machine learning model and task-specific logic.
2. Middleware layer - comprising the Swarm Learning Library (SLL), the Swarm API, and the blockchain-based orchestration mechanisms [[3](#references)].

Warnat-Herresthal et al. used Docker Containers to simulate between 3 and 32 sperate nodes on a swarm network, each with its own dataset. Each node implented the Swarm Learning framework and used a straightforward deep neural network using Keras to do the training [[3, 5](#references)]. The models were trained for 100 epochs an varying batch sizes.

Crucially, SL supports the use of heterogeneous hardware and variable network conditions. It is implemented in Docker containers and supports execution on dedicated machines or clusters. Identity management and node authorization are enforced using frameworks like SPIRE (based on SPIFFE) [[3](#references)]. Synchronization intervals, merging strategies, and weighting schemes are configurable to balance performance and computational efficiency [[3](#references)].

By design, Swarm Learning ensures:
- Confidentiality: No raw data leaves the institution.
- Resilience: No single point of failure due to decentralization.
- Democratization: Equal participation rights among collaborators.
- Security: Smart contracts regulate membership and consensus [[3](#references)].

---

## Benefits of Swarm Learning in Medical AI

SL offers a number of concrete benefits for the development and deployment of AI in healthcare settings, especially when data privacy, decentralization, and regulatory compliance are critical concerns.

### Privacy-preserving collaboration

SL allows multiple institutions to collaboratively train machine learning models without exchanging raw patient data. This is achieved by sharing model parameters via a blockchain-based peer-to-peer network rather than centralizing data, which helps address legal and ethical concerns around data sovereignty and patient confidentiality.

### Decentralized trust and fairness

Unlike Federated Learning, which relies on a central coordinator to merge model updates, SL uses blockchain-based consensus mechanisms to enable fully decentralized and equal participation. This avoids monopolistic control over the model and encourages broader collaboration across institutions and countries. Fairness can be further improved by adjusting the weighting of model parameters in the merging process based on local dataset size.

### Data efficiency and scalability

SL improves the data efficiency of AI training. Even when each participating node contributes only a small dataset, SL is able to produce models with high predictive performance. This makes it particularly suitable for medical applications, where individual datasets may be limited in size due to privacy constraints, geographic separation or rarity of conditions.

### Explainability and robustness

SL models exhibit greater consistency and plausibility in their predictions. Reader studies have shown that image regions highlighted by SL models for decision-making often contain histologically relevant features. Indicating that these models learn meaningful and interpretable representations.

### Resilience to bias and heterogeneity

SL performs robustly across heterogeneous datasets from multiple institutions, showing resistance to batch effects and technical variations. This improves model generalizability across different clinical settings and populations.

---

## Usage in Medical AI

### SL in Cancer Histopathology

Cancer histopathology, analyzing stained tissue slides under the microscope, is a cornerstone of cancer diagnosis. With the advent of digital pathology and AI, researchers have begun to explore how deep learning models can extract subtle, clinically relevant patterns from these high-resolution images. Developing and training these models requires large and diverse datasets, which are often impossible to gather due to legal and logisitcal barriers.

![Fig. 3 - SL in Cancer Histopathology](/docs/assets/images/2_cancer-histopathology.png)
*Fig 3: SL in Cancer Histopathology [[2]](#references)*

Swarm Learning addresses these challenges by enabling multiple pathology centers to collaboratively train AI models without moving data outside institutional boundaries. In a landmark study, Saldanha et al. demonstrated the use of Swarm Learning to predict clinically important molecular features in colorectal cancer, specifically BRAF mutational status and microsatellite instability (MSI) directly from hematoxylin and eosin stained slides [[2](#references)].

Three large datasets from institutions in Northern Ireland, Germany, and the United States were used, each stored on physically separate servers. Each node trained a local model and participated in periodic synchronization rounds via a blockchain-based Swarm Learning network [[2](#references)]. The study compared locally trained models, a centralized (merged) model, and various Swarm Learning models, both basic and weighted [[2](#references)].

![Fig. 4 - Comparison](/docs/assets/images/2_cancer-results.png)
*Fig 4: Comparison between local and swarm [[2]](#references)*

The findings were compelling:
- Performance: Swarm Learning models consistently outperformed locally trained models and matched or exceeded the performance of the centrally trained model. For instance, the weighted Swarm Learning model achieved an AUROC of 0.7736 in BRAF mutation prediction, outperforming both the best local model and the merged model.
- Data Efficiency: Swarm Learning showed high resilience when training data was limited. Even with small datasets going down to 100 patients per node, Swarm Learning achieved robust performance, something the locally trained models failed to achieve.
- Explainability: Swarm Learning models highlighted histologically relevant regions in slide-level heatmaps, and human experts rated these regions as more plausible compared to those highlighted by locally trained models.
- Generalizability: Swarm Learning models were validated on independent UK-based cohorts and maintained high performance, showing their potential to generalize across populations and institutions.

### SL in Detection of Leukemia

Leukemia diagnosis increasingly benefits from molecular profiling, particularly transcriptome analysis of blood cells which involves analyzing gene activity in blood cells. However, creating reliable AI-based classifiers requires large and diverse training datasets which are again difficult if not impossible to gather due to privacy regulations.

![Fig. 5 - Blood Transcriptome](/docs/assets/images/4_blood-transcriptome.png)
*Fig 5: Blood Transcriptome [[4]](#references)*

Warnat-Herresthal et al. demonstrated how Swarm Learning can overcome these barriers by enabling decentralized training of deep learning models on blood transcriptomes without data exchange [[3](#references)]. Using peripheral blood mononuclear cell (PBMC) transcriptomes from over 12,000 individuals across more than 100 clinical studies, they trained classifiers to detect acute myeloid leukemia (AML) and acute lymphoblastic leukemia (ALL) [[3](#references)].

Each dataset was distributed across multiple SWarm Learning nodes, mimicking real-world institutional separation. The Swarm Learning framework allowed these nodes to collaboratively train a shared model.

![Fig. 6 - Comparison](/docs/assets/images/3_leukemia-results.png)
*Fig 6: Comparison between individual nodes and the shared model [[3]](#references)*

Key results included:
- Superior accuracy: Across various scenarios including imbalanced case-control distributions and different data modalities (microarrays, RNA-seq) Swarm Learning consistently outperformed locally trained models and often matched the performance of centrally trained models.
- Robustness to heterogeneity: Swarm Learning performed well even when data was split by platform/technology or geographic origin, demonstrating resilience to batch effects and technical variability.
- Scalability and flexibility: The system scaled effectively from 3 up to 32 nodes. It also supported delayed node participation, showing that institutions can join an ongoing Swarm Learning network without disrupting training.
- Algorithm independence: Although deep neural networks were used in most experiments, the authors also implemented logistic regression via LASSO in Swarm Learning, demonstrating that the framework is model-agnostic [[3](#references)].

These results show that Swarm Learning enables the development of high-performance, privacy-preserving diagnostic tools for leukemia and could lay the foundation for broader adoption of decentralized AI in molecular diagnostics.

### SL in Detection of Tuberculosis

Tuberculosis remains one of the world’s leading infectious diseases, particularly in low-resource settings where diagnostic capacity can be limited. Transcriptomic profiling of blood has emerged as a promising tool for distinguishing active from latent TB infections, but AI models trained on such data face the usual challenge of data privacy restrictions limiting access to sufficiently large and diverse datasets.

Using Swarm Learning, researchers demonstrated that robust Tuberculosis classifiers can be trained collaboratively without centralizing data [[3](#references)]. In their study, blood transcriptome datasets from nearly 2,000 individuals were distributed across Swarm Learning nodes simulating distinct institutions. Each node trained locally on its data while synchronizing model parameters over a blockchain network.

![Fig. 7 - Comparison](/docs/assets/images/3_tb-results.png)
*Fig 7: Comparison between individual nodes and the shared model [[3]](#references)*

Several realistic scenarios were tested:
- Balanced and imbalanced case distributions: Even when the number of active Tuberculosis cases varied widely between nodes, Swarm Learning maintained high classification performance, outperforming local models and often matching centralized models.
- Low-prevalence test sets: In simulations mimicking outbreak detection with just 1 ective case per 20 patients, Swarm Learning models remained robust and sensitive, while local models degraded significantly.
- Network scalability: When the training network was expanded from 3 to 6 nodes with smaller individual datasets, individual model performance dropped but the Swarm Learning performance remained stable.

These results show that Swarm Learning not only protects patient privacy but also enhances model generalization and robustness, particularly in scenarios with data imbalance or low signal strength [[3](#references)]. This makes Swarm Learning highly suitable for collaborative AI efforts in infectious disease diagnostics where data decentralization is the norm.

### SL vs Local vs Central

Comparing model performance differences not only between models trained locally, centrally, and in a swarm but also across studies also shows promising results for the concept of Swarm Learning as a whole. It should be noted that the results are not directly comparable as the researches used different models and hyperparamters across the studies, but we took the freedom to compare them for similar node-counts and conditions anyways.

---

## Challenges of Swarm Learning in Medical AI

While SL holds great promise for privacy-preserving, decentralized AI in healthcare, several technical and practical challenges remain before its widespread clinical deployment.

### Infrastructure and Implementation Complexity

Establishing a functional Swarm Learning network requires substantial coordination across institutions. Nodes must maintain similar hardware capabilities and networking infrastructure to support training and communication, including integration of blockchain-based parameter exchange. Embedding Swarm Learning nodes into existing clinical systems across international healthcare providers is a significant logistical undertaking that has not yet been widely tested outside of controlled research settings. Continuously sinking costs of compute, especially for AI with neural accelerators becoming more widespread, allows for the development of pre-configured nodes at a procepoint that could be attractive for medical institutions. Unfortunately we were unable to find any examples for "Swarm Learning nodes as an appliance", presumably due to the lack of standardization.

### Lack of Standardization and Validation

Swarm Learning has been successfully demonstrated in use cases such as colorectal cancer histopathology, leukemia classification, and COVID-19 transcriptomics, but broader validation across clinical settings and data types is still lacking [[3](#references)]. Especially in critical applications, robust external validation and clinical benchmarking are essential before deployment. [Hewlett Packard's Swarm Learning Library](https://github.com/HewlettPackard/swarm-learning) was a promising start but was turned into a community maintained project [[6](#references)].

### Model Performance and Scaling

Swarm Learning models often perform comparably to centrally trained models, but achieving optimal performance still depends on training data size and distribution. When cohorts are small, model performance may degrade unless strategies like weighted Swarm Learning are applied. Performance parity with centralized models is also harder to maintain in scenarios involving heterogeneous data sources or imaging modalities.

### Governance and Fair Collaboration

Although Swarm Learning removes the need for a central coordinator, it introduces new governance questions: How are model contributions quantified and rewarded? How are model weights balanced among datasets of varying quality or size? Fairness mechanisms such as weighting by dataset size exist, but broader governance frameworks remain underexplored and underdeveloped.

### Privacy and Security Risks

Despite keeping data local, Swar Learning may still be vulnerable to model inversion or membership inference attacks through shared parameters [[3](#references)]. While Swarm Learning improves over federated learning by reducing single-point-of-failure risk, full protection against adversarial behavior may require integrating differential privacy and further cryptographic safeguards, which are not part of current implementations. The blockchain hosting the smart contract is another theoretical vector for an attack, but with increasing size of the blockchain network these attacks become increasingly more expensive and less likely.

### Regulatory and Ethical Considerations

Cross-border collaboration on medical data, even without sharing raw data, must align with diverse legal frameworks such as GDPR, HIPAA, and institutional review policies. Swarm Learnings's design is compatible with many regulations in theory, but legal interpretations may vary and affect adoption in practice.

---

## References

[1] [Shammar, Elham, Xiaohui Cui, and Mohammed AA Al-qaness. "Swarm learning: A survey of concepts, applications, and trends." arXiv preprint arXiv:2405.00556 (2024).](https://arxiv.org/abs/2405.00556)

[2] [Saldanha, O.L., Quirke, P., West, N.P. et al. Swarm learning for decentralized artificial intelligence in cancer histopathology. Nat Med 28, 1232–1239 (2022).](https://doi.org/10.1038/s41591-022-01768-5)

[3] [Warnat-Herresthal, S., Schultze, H., Shastry, K.L. et al. Swarm Learning for decentralized and confidential clinical machine learning. Nature 594, 265–270 (2021).](https://doi.org/10.1038/s41586-021-03583-3)

[4] [Liu, C.-L.; Dai, Y.-H. Bioinformatic Analyses of Peripheral Blood Transcriptome Identify Altered Neutrophil-Related Pathway and Different Transcriptomic Profiles for Acute Pancreatitis in Patients with and without Chylomicronemia Syndrome. Biomolecules 2023, 13, 284.](https://doi.org/10.3390/biom13020284)

[5] [schultzelab/swarm_learning on Github](https://github.com/schultzelab/swarm_learning)

[6] [HPE Developer Portal on HPE Swarm Learning Library](https://developer.hpe.com/platform/swarm-learning/home/)