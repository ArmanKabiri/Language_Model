# A Word-level RNN-based Language Model enhanced with character-level knowledge implemented in PyTorch
---

This language model, following [[1]](#1), first tries to learn subword features (i.e. prefixes, suffixes, etc.) using a character-level CNN. Then the extracted feature vector of each word is concatenated with its word embedding, and is finally fed into a n-layer LSTM.

You are free to try other values for features_level variable which controls the word representation used in the RNN component. The default value is:
```
features_level = ['word','character']
```
You can set it to ['word'] or ['character'] to only rely on word embeddings or character-level trained trained features, respectively.

---
### This language model is trained on Tweets about Corona virus pandemic posted in March 2020.

After being trained on a downsampled dataset of size of 100 MB, the Train PPL decreased to 95, while PPL on Dev. set reached to 150.

Some of the funny and interesting tweets generated by the model are listed below (the initial sequence given to the model as the seed is bold):

* **it's impossible to** get it out . the coronavirus is a great equalizer . we need to do our part .
* **even god** has been in quarantine . i am in a very different place ! i think i can get tested coronavirus
* **even god** and his team and his wife are now suffering from coronavirus .
* **i think god** was the only one to see the country that is going to die . #coronavirus #coronaviruslockdown

* **i think sex** are the biggest rise during the coronavirus pandemic . and one thing is ? this lockdown is so good for our humanity so it can be a real idea
* **i think sex** in a hospital is . you are working with their loved ones to save lives . " #coronavirus #covid19
* **animals think** they can kill them to help us protect our health for their own political greed . #coronavirus #covid19

* **my girlfriends** are in this together . i feel so much good to see the virus that has been infected ! #coronavirus
* **my girlfriends** are being forced to stay indoors for days . i don't know what to do . #covid19 #coronavirus

* **nobody cares** if they die because it has been a big time when we were all on the earth in the world . this is not a joke .
* **bats should** be released . i guess the whole world is going to get back to the house . #covid19 #coronavirus
* **bats should** be ashamed of the economy . #coronavirus
* **coronavirus is** a good time to start and take a moment to stay home and keep others safe during this time . we need to keep our communities healthy amp safe . . stay informed . #covid19


---
## Quick Start Guide
* Install the necessary dependencies: Numpy, PyTorch (1.5.0), TensorFlow, Tqdm.
* Download Kaggle Covid19 tweets dataset from [here](https://www.kaggle.com/smid80/coronavirus-covid19-tweets).
* Parse and clean the downloaded dataset by running:
```
python ParseTweets.py --root_dir <path to dataset directory> --output_file <path to write the parsed cleaned file>
```
* Train the model by running
```
python Train.py
```
with the following arguments:

* '--corpus_train_file' : 'location of the data corpus for training'
* '--corpus_valid_file': 'location of the data corpus for validation'
* '--embeddings_file' : 'If pretrained embeddings exist, load them here.'
* '--output_model_path' : 'Path to save the trained model.'
* '--output_id2word_path' : 'Path to save dictionary file (id2word)'
* '--output_word2id_path' : 'Path to save dictionary file (word2id)'
* '--output_id2char_path' : 'Path to save dictionary file (id2char)'
* '--output_char2id_path' : 'Path to save dictionary file (char2id)'

* '--n_layers' : 'Number of LSTM layers stacked on top of each other.'
* '--hidden_size' : 'Number of hidden units in each LSTM layer'
* '--features_level' : 'Specify the level of features by which you want to represent your words. Default value is ['word', 'character']'
* '--cnn_kernels' : CNN Kernels : (n_kernel,width_kernel). Sample input: (10,2) (30,3) (40,4) (40,5). Notice the spaces and parentheses.
* '--character_embedding_dim' : The dimension of the character embeddings

* '--dropout_probablity' : 'Dropout probablity applied on embeddings layer and LSTM layer.'
* '--embeddings_dim' : 'The dimension of the embeddings'
* '--batch_size' : 'Number of samples per batch.'
* '--seq_len' : 'Length of the sequence for back propagation.'
* '--epochs' : 'Number of epochs.'
* '--lr' : 'Learning rate.'
* '--seed' : 'The seed for randomness'
* '--clip_grad' : 'Clip gradients during training to prevent exploding gradients.'
* '--print_steps' : 'Print training info every n steps.'
* '--bidirectional_model' : 'Use it if you want your LSTM to be bidirectional.'
* '--tie_weights' : 'Tie weights of the last decoder layer to the embeddings layer.'
* '--freez_embeddings' : 'Prevent the pretrained loaded embeddings from fine-tuning.'
* '--gpu' : 'Turn it on if you have a GPU device.'


#### To have the model generate new tweets, simply run
```
python Generate.py
```
with the following arguments:

* '--model_path' : 'Path to the pre-trained model.'
* '--id2word_path' : 'Path to the dictionary file (id2word)'
* '--word2id_path' : 'Path to the dictionary file (word2id)'
* '--id2char_path' : 'Path to the dictionary file (id2char)'
* '--char2id_path' : 'Path to the dictionary file (char2id)'
* '--seed_sequence' : 'The sequence given to the model as the seed for text generation.'
* '--gpu' : 'Turn it one if you have a GPU device'

### Feel free to contribute to this model.

---
### References
<a id="1">[1]</a> 
Kim, Yoon, et al. 
Character-aware neural language models.
Thirtieth AAAI Conference on Artificial Intelligence. 2016.
