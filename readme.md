## Distractor Generation

Data preprocessing:

1. Reading the file Tran.csv, separating the sentences in words list using tokenize function and also cleaning the sentence i.e. removing the special symbols from the sentence. Meanwhile, collecting sentences in a common list to generate a dictionary.
2. following a similar approach for for all the columns questions, answer_text, distractors.
3. Seaparating the distractors using a regular expression. And then processing them individually.

For training, the sentences in the dataset are converted into vectors where every word is represented by its index in the dictionary. But the output of the model is a word at a time for which we represent distractors as an array of one-hot arrays representing the occurence of the word.

Model:

The model is a sequence to sequence (word level) model, which consists of an encoder part and a decoder.
The encoder: encodes the question and the answer_text, there is an embedding layer and then a dot product and concatenation is performed on the vectors obtained and then finally passed to an LSTM layer for final part of encoding whose states are preserved which then form the initial state of the decoder.
The decoder: it takes normal vector of words representation of the distractor sentences, embeds it and then passes them to an LSTM layer whose initial state has been set with the states obtained from encoding, then the output from the LSTM layer is passed to a dense layer which contains number of nodes = vocabulary size and the activation used is softmax. This process is repeated multiple times during inference to get the distractor word by word.


