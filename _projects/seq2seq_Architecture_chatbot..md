---
title: "Seq2Seq Architecture based DL chatbot"
collection: projects
date: 2020-01-20
---

This is a Proof-of-Concept Project on Seq2Seq Neural Architecture.
- Trained on Movie-lens dataset having conversations between different people by building a Seq2Seq neural architecture.
- It is trained on 100 epochs with a batch size of 64, and number of layers =3. The encoding and decoding embedding size are of 512 each.
- Dropout regularization used to remove any kind of overfitting and the losses are optimized using Adam optimizer.
- All the sentences in a batch, whether they are questions/ answers must have the same length. Hence  'PAD' tokens used.

