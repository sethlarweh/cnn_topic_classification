# cnn_topic_classification
## Intro
I wrote this classifier to classify Quora questions based on topics (Techonlogy, Business, Design, Food, Books).
Its inspired by [this](http://www.wildml.com/2015/12/implementing-a-cnn-for-text-classification-in-tensorflow/). I tweaked his code a bit to use pretrained wordvec.
Also you can find the topicwise questions in data directory. Every run is assosiated with a graph that plots accuracies vs steps taken. To download Quora questions, I used [this](https://github.com/vishaljain3991/quora_crawl).

## Requirements

- Python 2
- Tensorflow > 0.8
- Numpy

## Loading embedding vectors
```
$ cd data
```

```
$ wget http://nlp.stanford.edu/data/glove.6B.zip
```
```
$ unzip glove.6B.zip
```

```bash
python embedding_loader.py --help
```

```
optional arguments:
  -h, --help           show this help message and exit
  --data_dir DATA_DIR  data directory containing glove vectors

```
## Training

Print parameters:

```bash
python train.py --help
```

```
optional arguments:
  -h, --help            show this help message and exit
  --embedding_dim EMBEDDING_DIM
                        Dimensionality of character embedding (default: 128)
  --filter_sizes FILTER_SIZES
                        Comma-separated filter sizes (default: '3,4,5')
  --num_filters NUM_FILTERS
                        Number of filters per filter size (default: 128)
  --dropout_keep_prob DROPOUT_KEEP_PROB
                        Dropout keep probability (default: 0.5)
  --l2_reg_lambda L2_REG_LAMBDA
                        L2 regularizaion lambda (default: 0.0)
  --batch_size BATCH_SIZE
                        Batch Size (default: 64)
  --num_epochs NUM_EPOCHS
                        Number of training epochs (default: 200)
  --evaluate_every EVALUATE_EVERY
                        Evaluate model on dev set after this many steps
                        (default: 100)
  --checkpoint_every CHECKPOINT_EVERY
                        Save model after this many steps (default: 100)
  --allow_soft_placement [ALLOW_SOFT_PLACEMENT]
                        Allow device soft device placement
  --noallow_soft_placement
  --log_device_placement [LOG_DEVICE_PLACEMENT]
                        Log placement of ops on devices
  --nolog_device_placement
  --data_dir DATA_DIR   Provide directory location where glove vectors are
                        unzipped


```

Train:

```bash
python train.py
```

## Evaluating

```bash
python eval.py --eval_train --checkpoint_dir="./runs/1459637919/checkpoints/"
```

Replace the checkpoint dir with the output from the training. To use your own data, change the `eval.py` script to load your data.


## References

- [Convolutional Neural Networks for Sentence Classification](http://arxiv.org/abs/1408.5882)
- [A Sensitivity Analysis of (and Practitioners' Guide to) Convolutional Neural Networks for Sentence Classification](http://arxiv.org/abs/1510.03820)
