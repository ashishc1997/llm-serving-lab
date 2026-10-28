# Phase 1 Notes

## Tokenization 

The process of converting human readbale words into small components such that each token which can be a word or subowrd can be represented by a number. We can say it as an ID for that token.

There can be many ways this can be done - most known ways are Byte pair encoding (BPE) and Word Piece. 

## Embeddings

The embedding matrix will act as a lookup table for the embedding vectors for a given token. The size of the embedding is decided by the architect of the model. For GPT it is 762. 

We can imagine this as a single token is represented by a vector in 762 Dimenssional space. 

Side Note - The size of the embedding model is mentioned as 'd_model' in the model confg files.

## What are Q, K, V
