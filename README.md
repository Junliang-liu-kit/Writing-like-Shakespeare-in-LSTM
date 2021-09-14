Writing like Shakespeare in LSTM
=====================
Using LSTM cells, you can learn longer term dependencies that span many characters in the text--e.g., where a character appearing somewhere a sequence can influence what should be a different character much much later in ths sequence. Implementation of a character-level language model using Long Short-Term Memory Recurrent Neural Networks to generate Shakespeare poems, use a collection of [Shakespearian poems](/data/shakespeare.txt), especialy focus on implementing the forward and backward passes of the LSTMs.

## Laguage Model
A language model is an algorithm of learning (to approximate) a function capturing the statistical characteristics of the distribution of sequences ofwords or characters in a natural language. It is dividied into.
* Character-based language model
* Word-based language model
<br>Probabilistic language models assign probabilities to any sequence, and are typically interpreted asguessing the next words/characters in a sequence. 

## RNN and LSTM

### RNN (Recurrent Neural Network)
![image](https://github.com/Junliang-liu-kit/Writing-like-Shakespeare-in-LSTM/raw/master/images/RNN1.jpg)
<br>The operation of a Recurrent Neural Network learning a character-based language model. Each network step receives an input of a character in the history. The output layer of each step is a multinomial distribution of all characters in the vocabulary conditioned by the history.

### The operation of each network step
![image](/images/RNN.jpg)
<br>Each character is represented by an one-hot representation (`a vector with the size of the vocabulary with all zeros, only the index of the character is 1`). It is then transformed (`linearly`) to a continuous-value vector (`embedding`) which is the input to the RNN network. The output of the network is fed into the `Softmax function` to get the distribution. Finally the loss of each step is Cross-Entropy between the output distribution and the label (a character represented with `one-hot vector`).

### LSTM
![image](/images/LSTM.jpg)
The LSTM is different than the simple RNN that it has two memory cells and three gate:
* forget gate
* update gate
* output gate
Compared to the RNN it was proposed as (one of) the solution(s) to make learning more efficient. ('GRU' is also a good solution)

## Gradient-Checking
Back-propagation implementation, in general, depends on the correctness of the gradient computation based on each step of the chain rule. It is therefore crucial
to verify the correctness of our returned gradients from the algorithm. The most efficient way to do this is to compare our analytical gradients (obtained by backpropagation) and the numerical gradients.

## Sampling
Since our network is a generative model we can check if it can learn properly based on trying to generate new samples. By generating new character sequences we will observe the learning progress of the network. Initially the network should generate almost random sequences, and then later on it manages to generate something that looks like the training data. The Vanilla RNN will be struggle to even generate correctly spelled words, while the LSTMs can generate more plausible
sequences.
