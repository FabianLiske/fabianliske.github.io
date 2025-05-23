---
layout: default
title: Swarm Learning in Medical AI
---

## The Importance of Medical AI

The healthcare sector is under increasing pressure: populations are aging, chronic diseases are on the rise, and many regions face a shortage of medical specialists — particularly in fields like radiology, pathology, and oncology. Artificial intelligence (AI) offers a powerful way to help close this gap. AI systems can analyze medical images, genomic data, or electronic health records at scale, supporting physicians in diagnosing diseases earlier and more accurately, triaging patients, and even predicting treatment responses.

In areas with limited access to expert care, AI can act as a virtual second opinion or a diagnostic assistant, helping to reduce disparities in healthcare quality. Moreover, AI can handle time-consuming tasks, such as image annotation or documentation, freeing up valuable time for direct patient interaction.

But while the potential of AI in medicine is widely recognized, its implementation is often slowed. As healthcare is inherently decentralized, data is usually decentralized as well. Data privacy regulations and ethical concerns also hinder the creation of large, centralized datasets for training medical AI models. Swarm Learning offers a promising solution to these challenges - enabling collaborative AI development without the need to share raw patient data.

---

## What is Swarm Learning

In conventional machine learning, especially in healthcare, models are often trained on data that has been centralized — typically collected and stored in large data centers or cloud platforms. While this setup can be effective, it raises major concerns around data privacy, ownership, and compliance with regulations like GDPR or HIPAA.

### Local Learning

Every participant can create their own model using their own data (Fig 1a). However this will result in worse models if the amount of data ervery participant has is insufficient, but no data has to be shared.

### Centralized Learning

If all data can be centralized the training of a model can also be performed on a central copmute resource, for example in the cloud (Fig 1b). This typically results in better performance than locally trained models.

### Federated Learning

Federated Learnign (FL, Fig 1c) combines Local and Centralized Learning. The models are trained locally on locally stored data and the resulting model parameters are stored on a centralized server. While the users don't need to share their data centrally, there remains a central authority managing the model.

### Swarm Learning

Swarm Learning (SL) is a decentralized machine learning framework that combines edge computing with blockchain technology to enable secure, privacy-preserving, and collaborative model training. Unlike traditional federated learning, which relies on a central server for model coordination and aggregation, SL operates without any central authority. Instead, it employs a permissioned blockchain network to orchestrate peer-to-peer interactions, allowing participants (nodes) to dynamically join, contribute, and govern the model collaboratively.

Each participating node in the SL network trains a local instance of a machine learning model on its own private data. At predefined synchronization intervals, the model parameters—not the data—are exchanged among the peers. The parameters are merged into a shared global model using a consensus algorithm (typically a weighted average), and the updated parameters are then redistributed to all nodes for the next training iteration. This process is governed through smart contracts on a blockchain, which ensures transparency, auditability, and fairness in coordination.

The SL framework consists of two key layers:
1. Application layer - containing the machine learning model and task-specific logic.
2. Middleware layer - comprising the Swarm Learning Library (SLL), the Swarm API, and the blockchain-based orchestration mechanisms.

Warnat-Herresthal et al. used Docker Containers to simulate between 3 and 32 sperate nodes on a swarm network, each with its own dataset. Each node implented the SL framework and used a straightforward deep neural network using Keras to do the training. The models were trained for 100 epochs an vorying batch sizes.

Crucially, SL supports the use of heterogeneous hardware and variable network conditions. It is implemented in Docker containers and supports execution on dedicated machines or clusters. Identity management and node authorization are enforced using frameworks like SPIRE (based on SPIFFE). Synchronization intervals, merging strategies, and weighting schemes are configurable to balance performance and computational efficiency.

By design, Swarm Learning ensures:
- Confidentiality: No raw data leaves the institution.
- Resilience: No single point of failure due to decentralization.
- Democratization: Equal participation rights among collaborators.
- Security: Smart contracts regulate membership and consensus.

![Fig. 1 - ML Techniques](/docs/assets/images/ml-techniken.png)
*Fig 1: ML Techniques*

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

SL models exhibit greater consistency and plausibility in their predictions. Reader studies have shown that image regions highlighted by SL models for decision-making often contain histologically relevant features, indicating that these models learn meaningful and interpretable representations.

### Resilience to bias and heterogeneity

SL performs robustly across heterogeneous datasets from multiple institutions, showing resistance to batch effects and technical variations. This improves model generalizability across different clinical settings and populations.

---

## Usage in Medical AI

### SL in Cancer Histopathology

Cancer histopathology - analyzing stained tissue slides under the microscope - is a cornerstone of cancer diagnosis. With the advent of digital pathology and AI, researchers have begun to explore how deep learning models can extract subtle, clinically relevant patterns from these high-resolution images. However, developing robust AI systems requires training on large and diverse datasets, which is often impossible due to legal and logistical barriers to data sharing between institutions.

SL addresses these challenges by enabling multiple pathology centers to collaboratively train AI models without moving data outside institutional boundaries. In a landmark study, Saldanha et al. demonstrated the use of SL to predict clinically important molecular features in colorectal cancer - specifically BRAF mutational status and microsatellite instability (MSI) - directly from hematoxylin and eosin (H&E)-stained slides.

Three large datasets from institutions in Northern Ireland, Germany, and the United States were used, each stored on physically separate servers. Each node trained a local model and participated in periodic synchronization rounds via a blockchain-based SL network. The study compared locally trained models, a centralized (merged) model, and various SL models (both basic and weighted).

The findings were compelling:
- Performance: SL models consistently outperformed locally trained models and matched or exceeded the performance of the centrally trained model. For instance, the weighted SL model achieved an AUROC of 0.7736 in BRAF mutation prediction, outperforming both the best local model and the merged model.
- Data Efficiency: SL showed high resilience when training data was limited. Even with small datasets (e.g., 100 patients per node), SL achieved robust performance—something individual models failed to do.
- Explainability: SL models highlighted histologically relevant regions in slide-level heatmaps, and human experts rated these regions as more plausible compared to those of locally trained models.
- Generalizability: SL models were validated on independent UK-based cohorts and maintained high performance, showing their potential to generalize across populations and institutions.

### SL in Detection of Leukemia

Leukemia diagnosis increasingly benefits from molecular profiling, particularly transcriptome analysis of blood cells. However, creating reliable AI-based classifiers requires large and diverse training datasets—something difficult to achieve in a clinical setting due to data privacy regulations and institutional silos.

Warnat-Herresthal et al. demonstrated how SL can overcome these barriers by enabling decentralized training of deep learning models on blood transcriptomes without data exchange . Using peripheral blood mononuclear cell (PBMC) transcriptomes from over 12,000 individuals across more than 100 clinical studies, they trained classifiers to detect acute myeloid leukemia (AML) and acute lymphoblastic leukemia (ALL).

Each dataset was distributed across multiple SL nodes, mimicking real-world institutional separation. The SL framework allowed these nodes to collaboratively train a shared model, coordinating parameter updates via a permissioned blockchain.

Key results included:
- Superior accuracy: Across various scenarios - including imbalanced case-control distributions and different data modalities (microarrays, RNA-seq) - SL consistently outperformed locally trained models and often matched the performance of centrally trained models.
- Robustness to heterogeneity: SL performed well even when data was split by platform (e.g., different sequencing technologies) or geographic origin, demonstrating resilience to batch effects and technical variability.
- Scalability and flexibility: The system scaled effectively from 3 up to 32 nodes. It also supported delayed node participation, showing that institutions can join an ongoing SL network without disrupting training.
- Algorithm independence: Although deep neural networks were used in most experiments, the authors also implemented logistic regression via LASSO in SL—demonstrating that the framework is model-agnostic.

These results show that SL enables the development of high-performance, privacy-preserving diagnostic tools for leukemia, and could lay the foundation for broader adoption of decentralized AI in molecular diagnostics.

### SL in Detection of Tuberculosis

Tuberculosis (TB) remains one of the world’s leading infectious diseases, particularly in low-resource settings where diagnostic capacity can be limited. Transcriptomic profiling of blood has emerged as a promising tool for distinguishing active from latent TB infections, but AI models trained on such data face the usual challenge: data privacy restrictions limit access to sufficiently large and diverse datasets.

Using SL, researchers demonstrated that robust TB classifiers can be trained collaboratively without centralizing data. In their study, blood transcriptome datasets from nearly 2,000 individuals were distributed across SL nodes simulating distinct institutions. Each node trained locally on its data while synchronizing model parameters over a blockchain network.

Several realistic scenarios were tested:
- Balanced and imbalanced case distributions: Even when the number of active TB cases varied widely between nodes, SL maintained high classification performance, outperforming local models and often matching centralized approaches.
- Low-prevalence test sets: In simulations mimicking outbreak detection (e.g., 1 active case per 20 controls), SL models remained robust and sensitive, while local models degraded significantly.
- Network scalability: When the training network was expanded from 3 to 6 nodes—each with smaller data partitions—individual model performance dropped, but the SL model’s performance remained stable.

These results show that SL not only protects patient privacy but also enhances model generalization and robustness, particularly in scenarios with data imbalance or low signal strength. This makes SL highly suitable for collaborative AI efforts in infectious disease diagnostics, especially where data decentralization is the norm.

---

## Challenges of Swarm Learning in Medical AI

While SL holds great promise for privacy-preserving, decentralized AI in healthcare, several technical and practical challenges remain before its widespread clinical deployment.

### Infrastructure and Implementation Complexity
Establishing a functional SL network requires substantial coordination across institutions. Nodes must maintain synchronized hardware capabilities and networking infrastructure to support training and communication, including integration of blockchain-based parameter exchange. Embedding SL nodes into existing clinical systems across international healthcare providers is a significant logistical undertaking that has not yet been widely tested outside of controlled research settings.

### Model Performance and Scaling
SL models often perform comparably to centrally trained models, but achieving optimal performance still depends on training data size and distribution. When cohorts are small, model performance may degrade unless strategies like weighted SL are applied. Moreover, performance parity with centralized models is harder to maintain in scenarios involving heterogeneous data sources or imaging modalities.

### Governance and Fair Collaboration
Although SL removes the need for a central coordinator, it introduces new governance questions: How are model contributions quantified and rewarded? How are model weights balanced among datasets of varying quality or size? Fairness mechanisms such as weighting by cohort size exist, but broader governance frameworks remain underdeveloped.

### Privacy and Security Risks
Despite keeping data local, SL may still be vulnerable to model inversion or membership inference attacks through shared parameters. While SL improves over federated learning by reducing single-point-of-failure risk, full protection against adversarial behavior may require integrating differential privacy and further cryptographic safeguards, which were not part of current implementations.

### Regulatory and Ethical Considerations
Cross-border collaboration on medical data - even without sharing raw data - must align with diverse legal frameworks such as GDPR, HIPAA, and institutional review policies. SL’s design is compatible with many regulations in theory, but legal interpretations may vary and affect adoption in practice.

### Lack of Standardization and Validation
SL has been successfully demonstrated in use cases such as colorectal cancer histopathology, leukemia classification, and COVID-19 transcriptomics, but broader validation across clinical settings and data types is still lacking. Especially in critical applications, robust external validation and clinical benchmarking are essential before deployment.

---

## Sources

[Swarm Learning: A Survey of Concepts, Applications and Trends](https://arxiv.org/abs/2405.00556)

[Swarm learning for decentralized artificial intelligence in cancer histopathology](https://doi.org/10.1038/s41591-022-01768-5)

[Swarm Learning for decentralized and confidential clinical machine learning](https://doi.org/10.1038/s41586-021-03583-3)