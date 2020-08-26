#Introduction
###Build a network that combines supervised and unsupervised architectures in one model to achieve a classification task.

#Data
###Use 50% of the following classes for training (bird, deer and truck) while you can use any percentage you think is appropriate for the other classes.

#Architecture:
###Learning in 2 steps. First, I learned auto encoder module. Next, the detector was added in place of the decoder, and the detector was learned At this time. set requires_grad = false so as not to affect the auto encoder module.

##Why choose 2step?
###Before trained 2 step model , I trained auto encoder and detection separately. it turns out that the two modules do not need the same feature quantity.
###The detector only needs to look at the feature amount of the subject, but the auto encoder needs to learn including the background.
###In other words, the detector only needs to look at the feature amount of the subject, but the auto encoder needs to learn including the background.
###Therefore, in order to make an end-to-end system with high performance, I thought that the size of the model would be quite large.
###If it is 2 steps model, the model size will be relatively small, and at least the auto encoder module will give the same score as individual auto encoder model

##About Dataset
###Use 50% of the all classes for trainin, accuracy dropped.
###Double the size by adding augmentation while keeping the bird image at 50%, the accuracy increased by about 1%.

##About Data Augmentation
###It's better not to add augmentation such as random clock in auto encoder. The cause is probably like this. Crops and rotations create black areas (no image).
###The black areas is generated regardless of the surrounding image and occupies a certain proportion. This prevents loss decrease.
###In this case, the image after the auto encoder is darker than the input.
###However, since the subject has been correctly decoded, there is a possibility that it can be used for classification even as it is.
###This time I chose the one with the better loss.
###On the contrary, it is better to add augmentation in classification.
###If you do not add it, overfitting will occur at an early stage

##Model
###I tried 3models, Dence, SimpleCNN and Darknet
###The score was Darknet> SimpleCNN> Dence
###The score of Dence and Simple CNN improved with the addition of the Drop layer, but it did not reach Darknet.
###I think that if use a larger model, the accuracy will increase, so I will do it in the future.
###But it may not reach individual learning score.
