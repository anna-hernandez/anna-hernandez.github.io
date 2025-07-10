
# LLM foundations

#### Transformer-based architectures

#### Attention mechanism

#### Tokenisation and embeddings

Tokenisation is the process of breaking down text into segments or units. These units become the smallest unit of language that a language model understands and uses to build up on. In the same way that characters (letters, symbols, etc.) are for us humans.

There are different techniques for tokenising, that broadly classify into three categories.

1. **Character-based tokenisers**
Splits texts into individual charactes, which creates very reduced and hence memory efficient vocabularies, but then the embeddings can become very large matrices and characters alone don't contain much semantic information.

2. **Word-based tokenisers**
Split the text into full words based on delimiter rules (e.g. whitespace). The good side of this is that a word contains a lot of semantic information and hence each token does too. The problem is that this often creates very large vocabularies which require a lot of memory and it treats different versions of the same word (e.g. plural and singular of the same word) as different words and hence having different embeddings, when it's not optimal because semantically they should be the same. It doesn't bode well either when you have contractions for instance, where is not clear if it's best to split the word or not. For instace, "my friend's dog" could be split as "my", "friend's", "dog", or "my", "friend", "'s", "dog", but neither solution is great.

3. **Subword-based tokenisers**
That's the middle ground and that seems to work best. Splits rare words into subword tokens, indicating (e.g. with preceeding or ending ## symbols) whether the subword is at the beginning or end of the word. This gives versatility because tokens can be re-used across words, vocabularies are smaller, and tokens still keep semantic meaning.
Examples are:
    - Byte-Pair Encoding (BPE)
    - Byte-level BPE
    - WordPiece
    - SentencePiece
    - Unigram


Important bits to remember:
- a language model performs its best when the input for inference is split with the same tokeniser used to train the model


#### Embeddings
There are two types.

1. Frequency-based
Use word frequency to score words in a text. The most famous is TF-IDF.

2. Prediction-based: use token / context prediction to create embeddings. The advantage of this is that it creates dense embeddings that can represent the word meaning better. These embeddings are semantic embeddings but not contextualised, hence each word has a single embedding to represent all its meanings.

- Word2Vec: trained using two approaches
    - Skipgram: predict the context tokens based on a target token
    - CBOW: predict the target token based on context tokens
- Glove: uses co-occurrency frequencies to score words

3. Attention-based
Use the attention mechanism to re-score original (semantic but not contextualised) embeddings.
