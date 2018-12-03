After using basic models such as Logistic Regression and SVM(support vector machine) for text classification. Neural Network is used to see if we can get a better performance.  Word vectors are used here instead of word frequency. Word embeddings are vectorized representations of words. In order for the representations to be useful, some empirical conditions should be satisfied. For example, similar words should be closer to each other in the vector space. During the training process, the repersentations are constantly changing as well to optimize its performance.

 Highlighted steps in this Neural Network based approach: 

- Three columns in the dataframe are mainly used: ID, Article and Hyperpartisan. The whole dataset is splited into training and validation and testing using 0.75/0.125/0.125 ratio.

- The mean value for article length is calculated for the padding purpose.

- A function called **preproc** is used to tokenize articles, lemmatization is used, stop words and puctuations are removed before tokenizing articles using n grams. After this step, each article becomes a list of n-gram tokens and all the n-gram tokens in the training dataset are recorded to build the dictionary afterwards.

- Uni-gram is used in our model and the maximum vocabulary size is set to be 20000. According to the gram frequency, the first 20000 grams are selected. **id2token** is a list of tokens, where id2token[i] returns token that corresponds to token i. **token2id** is a dictionary where keys represent tokens and corresponding values represent indices. 0,1 are used as padding index and unknown index respectively. 

- Converting token to id in the dataset using the built dictionary. Since neural network prefers well defined fixed-length inputs and outputs, articles are padded and the whole training dataset is transformed into minibatches so that the input articles can be fed in parallel to the network to speed up the computing.

- In the neural network architecture, after the embedding layer, a linear layer is used to convert the output to dimension 2. After softmax, the two numbers corresponding to the probabilities of belonging to each class.

- CrossEntropyLoss is used, and Adam is used as the optimizer. Other hyper-parameters like learining rate, embedding size are tuned afterwards using the validation dataset. 

- ablation study: 

- 