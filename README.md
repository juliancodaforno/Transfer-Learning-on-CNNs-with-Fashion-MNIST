# Transfer-Learning-on-CNNs

A core tenet in feature learning is that good learnt features shall be transferable between tasks.  This has become a reality in computer vision where it is commonplace to use existing weights trained by others on alarge-scale datasets such as ImageNet (Deng et al., 2009), remove the classification layers, and then train new classification layers using your own labelled data while preserving the same convolutional neural networkstructure.

## Data
For this task we will emulate a similar setting with a toy example on the Fashion-MNIST data set. We need to make some minor modifications to create two subsets that do not share labels. Thus we split Fashion-MNIST into Fashion-MNIST-1 and Fashion-MNIST-2, which are of equal size and both contains a disjoint half of the original labels each.

## CNN Implementation
The idea was to first train a convolutional neural network with cross-entropy loss for the Fashion-MNIST-2data  to  then  use  it  for  the  transfer  learning  task.   In  this  part,  the  CNN  structure  and  hyperparameterswere tuned using the validation set of Fashion-MNIST-2 until arriving at a model performance of 93.33% accuracy.  A batch size of 256, a learning rate of 0.0001, 100 epochs and the added dropout functionality (with default p = 0.5) were used to get this performance. 

## Transfer Learning vs Random Initialization 
Then, the idea was to compare transfer learning vs random initialization. Therefore, two implemention of a multi-class, convolutional neural network with cross-entropy loss for the Fashion-MNIST-1 data, which shares the same structure as the one used for the Fashion MNIST-2 data. The pre-trained model still re-initializes its classifier layer because it is the layer that will have to change anyway (except if it was the same data).  This has been done by initializing the new CNN with the stored weights for all the other layers of the Fashion-MNIST-2 trained CNN (therefore only the classifier layer randomly initializes itself).  Indeed, in the code it can be seen that ”preCNN.fc3” is the only layer not being assigned the ”CNN2” weight parameters. The comparison has been performed using 5%, 10%, .  .  .  , 100% of the available Fashion-MNIST-1 training data to to compare the two model initializations.  In the code, two graphs giving the validation and training loss for each models on all the different % of datasets is given.

#  Results based on the graph in the Jupyter notebook
We can see that for the training loss comparison, the pre-trained CNN performs better all the time.  On the other hand, for the validation loss comparison, the randomly initialized CNN performs better after around 25%.   So  there  is  no  option  always  superior  to  the  other.   It  is  worth  noting  that  these  results  could  be explained by the pre-training model over-fitting in the training set.  Overall the performances of the two models are very high and relatively similar and do not give us a real feel of the need of transfer learning. This was just a toy model to get the feel of how to use transfer learning but this data is so "easily" classifiable that you can reach convergence anyway. Transfer Learning is widely used in industrial purposes when the cost of data is really expensive and therefore take the pre-trained model weights of a similar problem to provide better performance without needing to find more data.
