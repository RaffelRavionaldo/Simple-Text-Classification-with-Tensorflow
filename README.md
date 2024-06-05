Train the model on google colab that has Python version 3.10.2

Data Preparation and Training Process:

1.	The first step is to prepare dummy data, I asked chatgpt to prepare the dummy data, and then preprocess the data, because the target is a category column, we need to change it into a number using label encoding approval. for this case, I decide to make it into binary classification.

2.	After that I tokenize the name of the product and its description, but actually I just use the description column because It will be text classification and my description is longer than the name of the product. So to make it simple I just use the description column to create the model.

3.	For the train model, I just use one bidirectional LSTM because for now we just have a little data and the words from the description are not too many.

4.	The limitation of this model is that you only can use the English language and if you use a word that is not in the description column, it will make the prediction worse, so to improve this maybe we can use pre-trained word embedding from Stanford corpus/glove, you can download it via this link :  [GloVe: Global Vectors for Word Representation (stanford.edu)](https://nlp.stanford.edu/projects/glove/)  (I don’t use that because the size of that is really big)

If we use the pre-trained word embedding from Stanford, you must retrain the model, you can use this code before run step 3 on jupyter notebook : 

Prepare the Glove : 

![image](https://github.com/RaffelRavionaldo/Simple-Text-Classification-with-Tensorflow/assets/94748637/46682f24-46bd-4ac9-8fbf-acb9396641e1)

![image](https://github.com/RaffelRavionaldo/Simple-Text-Classification-with-Tensorflow/assets/94748637/ee9b005f-f184-43f3-ba6a-12fb0d8743b4)


Train the model : 

On step 3 in jupyter notebook, change this code : 

# Define embedding layer for description
desc_embedding = Embedding(input_dim=max_words_desc, output_dim=64, input_length=max_len_desc)(desc_input)

into : 

# Define embedding layer for description
desc_embedding = Embedding(input_dim=max_words_desc, output_dim=64, input_length=max_len_desc, weights=[embeddings_matrix], trainable=False)(desc_input)

and then we can re-train the model

If you want to run the code, just run all the code blocks on the Jupyter Notebook, if want to test it, you can go to step 4
