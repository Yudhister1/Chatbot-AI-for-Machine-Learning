Overview
============
This is an attempt at implementing [Sequence to Sequence Learning with Neural Networks (seq2seq)] and reproducing the results in [A Neural Conversational Model](aka the Google chatbot). The model is based on two [LSTM](https://en.wikipedia.org/wiki/Long_short-term_memory) layers. One for encoding the input sentence into a "thought vector", and another for decoding that vector into a response. This model is called Sequence-to-sequence or seq2seq. 

Dependencies
============

1. [Install Torch](http://torch.ch/docs/getting-started.html).
2. Install the following additional Lua libs:

   ```sh
   luarocks install nn
   luarocks install rnn
   luarocks install penlight
   ```
   
   To train with CUDA install the latest CUDA drivers, toolkit and run:

   ```sh
   luarocks install cutorch
   luarocks install cunn
   ```
   
   To train with opencl install the lastest Opencl torch lib:

   ```sh
   luarocks install cltorch
   luarocks install clnn
   ```

3. Download the [Cornell Movie-Dialogs Corpus](http://www.mpi-sws.org/~cristian/Cornell_Movie-Dialogs_Corpus.html) and extract all the files into data/cornell_movie_dialogs.


Basic Usage
===========
Here's a sample conversation after training for 20 epoch with 50000 examples, using the following command:

```sh
th train.lua --cuda --dataset 50000 --hiddenSize 1000
```

(Took 3 days to train on my GeForce GTX 780M.)

For OpenCL, use `--opencl` instead of `--cuda`. To train on CPU, don't provide any of those two. Use the `--dataset NUMBER` option to control the size of the dataset. Training on the full dataset takes about 5h for a single epoch. The model will be saved to `data/model.t7` after each epoch if it has improved (error decreased).

> **me:** Hello?
> **bot:** Hi.
> 
> **me:** How are you?
> **bot:** I'm fine.
> 
> **me:** What's your name?
> **bot:** It's hard to describe.
> 
> **me:** How so?
> **bot:** I'm not sure.
> 
> **me:** What color is the sky?
> **bot:** It's blue.
> 
> **me:** What is your job?
> **bot:** It's not that i'm a fucking werewolf!
> 
> **me:** What is the purpose of life?
> **bot:** A gift.
> 
> **me:** Are you intelligent?
> **bot:** Yes, well...
> 
> **me:** Are you a machine?
> **bot:** That's a lie.


To load the model and have a conversation:

```sh
th -i eval.lua --cuda # Skip --cuda if you didn't train with it
# ...
th> say "Hello."
```

