# NLP_FINAL_CNNtextsum
## Our steps

### Preprocessing

#### Tokenize and Prepocessing
(A)
將標點符號跟字分開
example:
"I Have a apple, pineapple, and pen"
to
"I Have a apple , pineapple , and pen"

(B)
th preprocess.lua \
-save_data /home/bossi/Textsum/data/train/CNNtextsum \
-train_src /home/bossi/Textsum/data/train/Train_article.txt \
-train_tgt /home/bossi/Textsum/data/train/Train_title.txt \
-src_vocab_size 30000 \
-tgt_vocab_size 30000 \
-valid_src /home/bossi/Textsum/data/train/Valid_article.txt \
-valid_tgt /home/bossi/Textsum/data/train/Valid_title.txt \
-src_seq_length 250 \
-tgt_seq_length 75

#### First Training:

th train.lua \
-data ../data/train/CNNtextsum-train.t7  \
-src_word_vec_size 300 \
-tgt_word_vec_size 300 \
-end_epoch 100 \
-save_model CNNtextsum -gpuid 1

#### Retraining:
th train.lua \
-gpuid 1 \
-data ../data/train/CNNtextsum-train.t7  \
-save_model CNNtextsum \
-end_epoch 100 \
-train_from /home/bossi/Textsum/opennmt/CNNtextsum_checkpoint3.t7 


#### Use your model
th translate.lua \
-gpuid 1 \
-model /home/bossi/Textsum/opennmt/CNNtextsum_checkpoint3.t7 \
-src ../data/train/Test_article.txt \
-output ~/CNNTS3.txt

### Citation

A [technical report](https://arxiv.org/abs/1701.02810) on OpenNMT is available. If you use the system for academic work, please cite:

```
@ARTICLE{2017opennmt,
  author = {{Klein}, G. and {Kim}, Y. and {Deng}, Y. and {Senellart}, J. and {Rush}, A.~M.},
  title = "{OpenNMT: Open-Source Toolkit for Neural Machine Translation}",
  journal = {ArXiv e-prints},
  eprint = {1701.02810}
}
```

### Additional resources

* [Documentation](http://opennmt.net/OpenNMT)
* [Example models](http://opennmt.net/Models)
* [Forum](http://forum.opennmt.net)
* [Gitter channel](https://gitter.im/OpenNMT/openmt)
* [Live demo](https://demo-pnmt.systran.net)
* [Bibliography](http://opennmt.net/about)

