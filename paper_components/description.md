Kolmogorov-Arnold Networks (KANs) were introduced as a class of networks based on the Kolmogorov-Arnold Representation Theorem (KART) and promised to be more efficient in smaller function learning tasks than Deep Neural Networks (DNNs). According to KART, a multivariate continuous function f on a bounded domain can be written as a finite composition of univariate functions.

$$
    f(x_1,x_2, \dots , x_n) = \sum_{q=1}^{2n+1} \Phi_q \left( \sum_{p=1}^{n} \phi_{q,p}(x_p) \right)
$$

Where $f: [0,1]^n \rightarrow \mathbb{R}$ defines the outer function and $ \phi_{q,p} : [0,1] \rightarrow \mathbb{R}$ and $\Phi_q : \mathbb{R} \rightarrow \mathbb{R}$ define the inner functions used for approximation. A major challenge when applying this theorem to machine learning (ML) is that the 1-D functions $\phi_{q,p}$ might be non-smooth or even fractal. However, \citeauthor{KAN_2024} argued that in the average case most functions in science are smooth and have sparse composite structure. This allows us to use smooth functions, in their case B-Splines, as the basis to create a network that can scale to arbitrary breadth and depths.

The choice of B-Splines as the basis for KANs has proven to be effective, but, they are not the only functions we may use in order to construct KAN models. In principle, we could use any univariate universal function approximator as the basis for a KAN model. However, for practical purposes we would like these univariate functions to be expressive, compact and easy to compute. Data Re-Uploading (DR) circuits are a class of QML algorithms that fit these characteristics and hence can form a promising new basis for KAN models.

Quantum Machine Learning (QML), is a field of machine learning which seeks to exploit the special properties of quantum circuits in order to create new more efficient ML models. Pérez-Salinas et al, introduced the Data Re-Uploading Classifier, which was proven to be a Universal Classifier based on the **Universal Approximation Theorem** of DNNs.

$$
    h(\vec{x}) = \sum_{i=1}^{N} \alpha_i \cdot \sigma(\vec{w_i} \cdot \vec{x} + b_i) \; \quad ; \alpha_i, b_i \in \mathbb{R}
$$

Specifically the authors used a corollary which stated that $\sigma$ could be a non-constant finite linear combination of periodic functions. This allowed DR models to create universal function approximators using rotational quantum gates. Critically, this proof also makes DR models eligible univariate functions to utilize as building blocks for KANs.

We utilize the universal approximation functionality of DR models in order to construct a new variant of the KAN model called QuIRK's. QuIRK incorporate DR models in place of B-Splines while maintaining the same scalability in depths and breadth structure as KANs. Due to the inherent higher dimensionality of qubits  compared to real-valued univariate functions, DR models are far more expressively compact. This increased dimensionality is due to two main factors - (1) The vectorized nature of qubits caused by superposition. (2) The complex-valued nature of qubit states. This allows our DR based QuIRK to use fewer trainable parameters and smaller model sizes when compared to KANs for a similar level of accuracy as shown experimentally in the results section.

Another important aspect of QuIRK's is that they can be easily accelerated on GPUs. We refer to our model as `*Quantum Inspired*' because, although we utilize a QML model, the structure of our network does not require any quantum computers for training or inference. Due to the lack of entanglement, all our circuits are factorizable into single qubit circuits and can be computed using $2\times 2$ matrix multiplications (matmuls) on simulators. These matmul operations are far more optimized for modern GPUs as compared to B-Splines used by KANs. This allows for better computational scaling as compared to KANs. Additionally, the use of these quantum inspired mathematical structures allows us to leverage the expanded feature space of  quantum systems. It is important to note that current backpropagation implementations and optimizers struggle with complex numbers and hence we leverage the capabilities of quantum simulators in this domain to train our models.

Therefore, the main features of the QuIRK model can be summarized as follows:
1. Data re-uploading based scalable network architecture,
2. Parameter efficient KAN model leveraging the higher dimensionality of quantum systems,
3. Computationally scalable due to simple $2 \times 2$ matrix multiplication based implementation.
