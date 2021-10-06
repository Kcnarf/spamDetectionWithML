# spamDetectionWithML
Exploring spam detection through Machine Learning

## [SpamDetection.ipynb](https://github.com/Kcnarf/spamDetectionWithML/blob/master/SpamDetection.ipynb)
 - experimentation based on [Using Natural Language Processing for Spam Detection in Emails](https://medium.datadriveninvestor.com/using-natural-language-processing-for-spam-detection-in-emails-281a7c22ddbc)
 - [new location](https://archive-beta.ics.uci.edu/ml/datasets/sms+spam+collection) of data
 - the main steps are :
   - sentence sanitization/uniformization
   - sentence tokenization :
     - creation of the vocabulary
     - creation of the dictionnary word -> token (a token is an integer, i.e. an index)
   - creation of the training data set and the validation data set
   - definition of the model:
     - uses a bidirectionnal LSTM (LSTM are appropriate to sequence, 'bidirectionnal' in order to grab information from the beginig of the sequence as well as the end of the sequence)
     - uses a dropout layout for regularization
   - training of the model:
     - train only with the training data set
     - use mini batches (forward prediction of several sequences at the same time), and thus stochastic gradient descent
   - evaluation of the trained model with the validation data set in order to compute Precision/Recall/F1 scores

## [spamDetection_withGloveEmbeddings.ipynb](https://github.com/Kcnarf/spamDetectionWithML/blob/master/spamDetection_withGloveEmbeddings.ipynb)
 - experimentation based on [Using pre-trained word embeddings](https://keras.io/examples/nlp/pretrained_word_embeddings/#load-pretrained-word-embeddings)
 - reuse GloVe embeddings (instead of the trainable keras.preprocessing.text.Tokenizer of the previous experimentation) :
 - compared to previous expérimentation :
   - the model has now 2 distincts parts :
     - the embedding part which reuses the GloVe language model, and doest not need to be trained (because spams are general purpose issue, no need to focus/specialize embeddings on a particular semantic field)
     - the classification part, which has the same deep learning architecture as the previous experimentation, and which is trainable
   - less weights to train (85k instead of 1.6M), even if the overall model has more weights (5M instead of 1.6M); no need to train the GloVe embedding part
