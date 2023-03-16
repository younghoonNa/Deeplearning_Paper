![image](https://user-images.githubusercontent.com/38518648/225702505-e45b45b3-b3c3-4dc3-938e-d5b27056ffff.png)


## Problem
1. Our optimizer used SGD
    -  Gradient descent algorithm cost is very expensive, can easier fall into local minima
2. Each batch have different distribution. It can make Internal Covariant Shift
3. Internal Covariant Shift: change distribution of network activation due to the change in network parameters during training.
4. We used ReLU activate function , As a result, half of our activation is zero

## Main Idea
Main idea: Calculating mean(𝝁) and variance(𝝈^𝟐) of training data in mini batch 𝒙. <br>
   Also training (𝜸, 𝜷) of each layer. And activation normalized zero-mean, unit variance 𝒙 ̂.  <br>
   Activation output changed 𝒚=𝜸𝒙 ̂+𝜷,  (𝜸=𝝈,  𝜷=𝝁) 

## Related work
<b> Train deep ResNet to competitive accuracies without normalization </b>
1. Learnable scalar at the end of each residual branch(initialized to zero)
2. Normalizer-Free Resnet 
    - Residual branch at initialization and apply Scaled Weight Standardization 
    - Same acc of ResNet on ImaegNet but less then EfficientNet and not stable at large Batch size

## Process
1. Computation of Residual branch

$$ h_{(i+1)} = h_i + \alpha f_i (h_i/\beta_i) $$

𝒉_𝒊 : input i-th residual block <br>
𝒇_𝒊 : i-th function computed by i-th residual branch, preserve Var(𝒇_𝒊 (𝒛)) = Var(𝒛) <br> 
𝜶 : rate of the variance of the activation after each residual block <br>
𝜷_𝒊=√(𝑽𝒂𝒓(𝒉_𝒊 ) )  <br>

→ Var(𝒉_(𝒊+𝟏) )  = Var(𝒉_𝒊 )+𝜶^𝟐 

2. Scaled Weight Standardization

$$ \hat{W}_{ij} = (W_{ij} - \mu_i) / \sqrt{N}\sigma_i $$

𝝁_𝒊 : 𝟏/𝑵  𝚺_𝒋    →  mean  <br>
𝝈^𝟐 : 𝟏/𝑵 𝚺_𝐣  (𝐖_𝐢𝐣  −𝝁_𝒊 )^𝟐   →  standard deviation <br>

3. ReLU scaled by 𝜸 that is non-linearity specific scaler
  - The combination of the 𝛄-scaled activate function and Scaled Weight Standardized layer ensure variance preserving 

$$ ReLU = \gamma = \sqrt{2/(1-(1/n))} $$

- When initialize hidden layer of Residual branch, our variance close to 1
- Input 𝒙 got linearity sampled 𝒩(𝟎,𝟏)
- ReLU output 𝒈(𝒙)= max(0, 1) will sampled from Gaussian distribution with variance 𝝈_𝒈^𝟐=(𝟏/𝟐)(𝟏−(𝟏/𝝅))
- Similarity of Kaiming He Weight initialization
++ Gradient Clipping method



