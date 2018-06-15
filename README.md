# LancoPKU Summarization
This repository is the implementation of three novel NLP summarization models proposed by lancopku recently. These models achieves state-of-the-art performances and are applicable to different tasks of summarization. By modifying the '.yaml' configuration file, one can easily apply the codes to his own work. Names of these models and their corresponding papers are listed as follows:

1. Global Encoding for Abstractive Summarization, [[pdf]](https://arxiv.org/abs/1805.03989)
2. Word Embedding Attention Network (WEAN)  [[pdf]](https://arxiv.org/abs/1803.01465)
3. SuperAE [[pdf]](https://arxiv.org/abs/1805.04869)

***********************************************************


### [Content](#0)
####  [1. How to Use](#1)
##### [---1.1 Requirements](#1.1)
##### [---1.2 Configuration](#1.2)
##### [---1.3 Preprocessing](#1.3)
##### [---1.4 Training](#1.4)
##### [---1.5 Evaluation](#1.5)
#### [2. Citation](#2)
####  [3. Introduction to Models](#3)
##### [---3.1 Global Encoding](#3.1)
##### [---3.2 WEAN](#3.2)
##### [---3.3 SuperAE](#3.3)


***********************************************************


<h2 id="1"> 1 How to Use </h2>

<h4 id="1.1"> --- 1.1 Requirements </h4>

* Ubuntu 16.0.4
* Python 3.5
* Pytorch 0.3.1
* pyrouge
* matplotlib (for the visualization of attention heatmaps)
* Tensorflow (>=1.5.0) and TensorboardX (for data visualization on Tensorboard)


***********************************************************

<h4 id="1.2"> --- 1.2 Configuration </h4>

In order to use pyrouge, set rouge path with the line below:
```
pyrouge_set_rouge_path script/RELEASE-1.5.5
```

***********************************************************

<h4 id="1.3"> --- 1.3 Preprocessing </h4>

```
python3 preprocess.py -load_data path_to_data -save_data path_to_store_data
```
Remember to put the data into a folder and name them *train.src*, *train.tgt*, *valid.src*, *valid.tgt*, *test.src* and *test.tgt*, and make a new folder inside called *data*

***********************************************************
<h4 id="1.4"> --- 1.4 Training </h4>

```
python3 train.py -log log_name -config config_yaml -gpus id
```

***********************************************************
<h4 id="1.5"> --- 1.5 Evaluation </h4>

```
python3 train.py -log log_name -config config_yaml -gpus id -restore checkpoint -mode eval
```

***********************************************************
<h2 id="2"> 2 Citation </h2>

Plese cite these papers when using relevant models in your research.
#### Global Encoding:
```
@inproceedings{globalencoding,
  title     = {Global Encoding for Abstractive Summarization},
  author    = {Junyang Lin and Xu Sun and Shuming Ma and Qi Su},
  booktitle = {{ACL} 2018},
  year      = {2018}
}
```

#### WEAN:
```
@inproceedings{wean,
  author    = {Shuming Ma and Xu Sun and Wei Li and Sujian Li and Wenjie Li and Xuancheng Ren},
  title     = {Query and Output: Generating Words by Querying Distributed Word
	       Representations for Paraphrase Generation},
  booktitle = {{NAACL} {HLT} 2018, The 2018 Conference of the North American Chapter
	       of the Association for Computational Linguistics: Human Language Technologies},
  year      = {2018}
}
```

#### SuperAE:
```
@inproceedings{Ma2016superAE,
  title   = {Autoencoder as Assistant Supervisor: Improving Text Representation for Chinese Social Media Text Summarization},
  author  = {Shuming Ma and Xu Sun and Junyang Lin and Houfeng Wang},
  booktitle = {{ACL} 2018},
  year      = {2018}
}
```
***********************************************************
<h2 id="3"> 3 Introduction to Models </h2>

<h4 id="3.1"> --- 3.1 Global Encoding </h4>

##### Motivation & Idea
Conventional attention-based seq2seq model for abstractive summarization suffers from repetition and semantic irrelevance. Therefore, we propose a model containing a convolutional neural network (CNN) fitering the encoder outputs so that they can contain some information of the global context. Self-attention mechanism is implemented as well in order to dig out the correlations among these new representations of encoder outputs.

##### Performance on LCSTS(ROUGE)
![On LSCTS](https://github.com/limuyu0110/Global-Encoding/raw/master/tables/CGU-LCSTS.png)

***********************************************************
<h4 id="3.2"> --- 3.2 WEAN </h4>

##### Motivation & Idea
In the decoding process, conventional seq2seq models typically use a dense vector in each time step to generate a distribution over the vocabulary to choose the correct word output. However, such a method takes no account of the relationships between words in the vocabulary and also suffers from a large amount of parameters (hidden_size * vocab_size). Thus, in this model, we use a query system. The output of decoder is a query, the candidate words are the values, and the corresponding word representations are the keys. By refering to the word embeddings, our model is able to capture the semantic meaning of the words.

##### Performance on LCSTS(ROUGE)
![On LSCTS](https://github.com/limuyu0110/Global-Encoding/raw/master/tables/WEAN-LSCTS.png)

***********************************************************
<h4 id="3.3"> --- 3.3 SuperAE </h4>

##### Motivation & Idea
Corpus from social media is generally long, containing many errors. A conventional seq2seq model fails to compress a long sentence into an accurate representation. So we intend to use the representation of summary (which is shorter and easier to encode) to help supervise the encoder to generate better semantic representations of the source content during training. Moreover, ideas of adverserial network is used so as to dynamically dertermine the strength of such supervision.

##### Performance on LCSTS(ROUGE)
![On LCSTS](https://github.com/limuyu0110/Global-Encoding/raw/master/tables/SuperAE-LSCTS.png)
