The author proposes a new method called BNSR that aims to replace BatchNormalization 
by incorporating skewness information using Pearson's second skewness coefficient.
BNSR is applied after the input values have been standardized to zero-mean and unit variance. 
The method uses a parameter p = 1.01 and executes under a specific expression. 
The usefulness of BNSR and the reason for using p = 1.01 are unclear. but 
   
## Expression
$$ p = \frac{std}{3(mean-median)}$$ 

if x >= 0

$$ \varphi_p(x) = x^p $$ 

if x < 0

$$ \varphi_p(x) = -(-x)^p $$ 

$$ \hat{x} = \frac{x - mean}{var} , -> \varphi_p(\hat{x}) $$
