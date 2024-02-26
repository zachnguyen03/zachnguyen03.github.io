# Diffusion Models for Generative Models

Original paper link: [click here](https://arxiv.org/pdf/2112.10752.pdf)

### Definition

---

<aside>
💡 The essential idea is to systematically and slowly destroy structure in a data distribution through an iterative forward diffusion process. We then learn a reverse diffusion process that restores structure in data, yielding a highly flexible and tractable generative model of the data

</aside>

- Why step-by-step denoising? Since estimating small perturbations is more tractable than explicitly describing the full distribution with a single, non-analytically-normalizable, potential function
- **Formulation of neural network in DDPM**
    1. Output:
        - Mean of noise at each time step
        - Original image (not good)
        - **Noise of image (subtracted from noise image → little bit less noised image)**
    2. Noise schedule:
        - Linear schedule: not optimal
            - Too rapid destruction of original image
            - Too uninformative at the end of diffusion step
        - Cosine schedule ([this paper](https://arxiv.org/pdf/2102.09672.pdf)): solve both problems linear schedule posits.
    3. **Architecture**
        1. U-Net: bottleneck in the middle, combine residual blocks and downsampling/unsampling blocks
        
        ![Untitled](https://miro.medium.com/v2/resize:fit:1084/1*KgT9m7wgbxyCWqmPqETCyQ.png)
        
        - Sinusoidal embedding is embedded into each residual block → keep track of the time step
        - Different amount of noise is added in different time step
        
        b. In [this paper](https://arxiv.org/pdf/2105.05233.pdf), author proposed updates to the previous diffusion model
        
        - Increase depth, decrease width → more attention layers + increase # of attention heads
        - Employ BigGAN residual block
        - Employ Adaptive Group Normalization (AdaGN)
        - Classifier Guidance (too coarse a topic)