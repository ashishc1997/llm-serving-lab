# Phase 1 Notes

## Tokenization 

The process of converting human readbale words into small components such that each token which can be a word or subowrd can be represented by a number. We can say it as an ID for that token.

There can be many ways this can be done - most known ways are Byte pair encoding (BPE) and Word Piece. 

## Embeddings

## Embeddings

The embedding matrix is a fixed lookup table that ships inside the model weights
(e.g. `model.embed_tokens.weight`). Shape: `vocab_size × hidden_size`. Each token ID
selects one row → that row is the token's vector.

The width (hidden size / d_model) is an architecture choice made by the model's designers. Config field names:
`hidden_size` (Llama, Mistral, Qwen), `n_embd` (GPT-2).

| Model        | vocab   | hidden | params in table | BF16 size |
|--------------|---------|--------|-----------------|-----------|
| GPT-2 small  | 50,257  | 768    | ~38.6M          | ~77 MB    |
| Llama 3 8B   | 128,256 | 4,096  | ~525M           | ~1.05 GB  |

Serving note: a large vocab costs real GPU memory. Some models reuse this
matrix as the output (logits) layer: "tied embeddings".

Note on "tied embedddings" - The embedding matrix we talk about that is used to convert a token into embedding at this stage is then used again while calculating the logits for the next token. This helps reducing the size of the model.

The embedding is context-free: "play" gets the same vector in every sentence.
Adding context is attention's job → next section.

## What are Q, K, V

Q - Query Vector 

We can imagine this as a token asking questions for what it wants. Anology wise a hiring manegere asking questions to find out what he wants.

K - Key Vector 

We can imagien this as a token telling what it has to offer. Anology wise a candidate letting know what he has to offer.

V - Value Vector

The actual menaing/content of the token.

The Q, K, and V for all the tokens is calculated by Multiplying their embeddings to the 'd_k', 'd_q', and 'd_v' there are trained metrices of shape ['d_model' X 'd_k']. The size of 'd_k' is decided by the model designers.

Now the attention formula calculates the attention using - (Q.KT/\root dk)V. What this does is it shifts the V or value of each token basis their neighbouring tokens.