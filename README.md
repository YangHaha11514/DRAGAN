# DRAGAN

https://arxiv.org/abs/1705.07215

A stable algorithm for GAN training

Note: We now have preliminary BogoNet results for improved WGAN. And we beat them in every single metric by a significant margin! Do keep an eye out for the next version of this paper

I am a big fan of open discussions/democratized research. Do post any questions you have at :-
https://www.reddit.com/r/MachineLearning/comments/6da7pu/170507215_how_to_train_your_dragan_training/

We had an interesting discussion about connections between LSGAN, improved WGAN and DRAGAN (Ian Goodfellow and Martin Arjovsky were kind enough to give their comments). Check it out at :-
https://www.facebook.com/kodali.naveen.90

To summarize, recently introduced regularized class of GANs which improve stability can be classified into two types.

1. Global Constraint: 
This involves linking random real + fake sample pairs and imposing gradient constraints between them. Loss-Sensitive GAN was the first paper to introduce this general idea. Improved WGAN came up with a different way of imposing this type of constraint. While the motivations were very different, both roughly fall under the same class of models.

2. Local Constraint:
DRAGAN came up with the novel idea of imposing local constraints, motivated from local Nash equilibria hypothesis. To clarify the difference between these ideas, lets take an example. If we are modeling CIFAR-10, our algorithm might impose constraints between a cat picture + blurry cat picture, but global constraint based algorithms might do it between a cat picture + blurry airplane picture. We never do such a thing and argue that its bad for generative modeling performance. So, our constraint is strictly weaker than the global one. We observed improved performance and stability in our experiments using the local one. 

Essentially, both of these constraints mitigate the issue of local NE. The idea of using smoothing to make games more tractable is very old. We cite works of Nash from 1950s. To convince yourself that both these ideas are more general, rather than being restricted to a specific divergence measure or a loss function, I suggest trying out different generator functions, f-divergences (or) imposing gradient constraints in a variety of other ways possible. They all will improve stability, albeit to different extents. We give motivation for our final choice in the section 4.2 of our paper. 

It is always possible to find architectures which are particularly suited for a specific algorithm. So, we highly recommend our BogoNet metric to test for stability of different training procedures. It is inspired from WGAN and improved WGAN papers where they use 4-5 architectures that are known to be hard for vanilla GAN. We scaled up and generalized this experiment, we show results in our paper using a set of 150 different architectures. We pick them randomly to remove any biases.

Some of the repositories that would be helpful and which helped us in our experiments/code (big thanks!) - 

https://github.com/igul222/improved_wgan_training
https://github.com/wiseodd/generative-models/tree/master/GAN
https://github.com/openai/improved-gan/tree/master/inception_score
