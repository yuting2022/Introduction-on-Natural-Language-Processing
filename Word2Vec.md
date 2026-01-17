Word2Vec is a neural embedding framework designed to learn dense, low-dimensional vector representations of words from raw text. The central idea is that words appearing in similar linguistic environments should end up close to one another in the embedding space. In doing so, Word2Vec operationalizes a modern form of the distributional hypothesis—“you shall know a word by the company it keeps”—and it does so through a computationally efficient neural architecture.

There are two main variants within Word2Vec: CBOW (Continuous Bag of Words) and Skip-gram. 

The difference between them lies largely in what they are trying to predict. CBOW takes the surrounding context words in a fixed sliding window and tries to predict the missing center word. In implementation, the embeddings of those context words are typically summed or averaged and then used to infer the probability of the target word. 

Skip-gram, on the other hand, reverses the prediction direction. It starts from a center word and attempts to predict the words that appear around it. 

Conceptually, CBOW feels a bit like a fill-in-the-blank exercise, whereas Skip-gram resembles imagining possible contexts given a single word.

In practice. CBOW tends to be faster to train because each update predicts only one center word. Skip-gram requires multiple predictions per center word, which makes training more computationally expensive. However, this extra burden pays off for low-frequency vocabulary: Skip-gram distributes the learning signal across individual context predictions and therefore tends to maintain richer representations for rare words, while CBOW’s averaging process may obscure or dilute such information.

Both models also maintain two sets of embeddings—one for center words and one for context words. These are sometimes called center and context embeddings. In most practical settings, the center embeddings are used as the final word vectors for downstream applications because they tend to capture the semantic relationships people care about. At a high level, Word2Vec is not only capable of capturing topical similarity (e.g., “king” and “queen”) but also more structured analogies, which famously gave rise to examples such as “king – man + woman ≈ queen”.

Another important practical consideration in Word2Vec is the choice of window size. 

There is no theoretical rule that dictates the optimal window; instead, the choice depends on the corpus and the task. On corpora with relatively strict syntactic boundaries—such as news articles or encyclopedic text—CBOW often uses a smaller window, roughly in the range of three to five words, producing more localized semantic information. Skip-gram, by contrast, can benefit from larger windows—often five to ten or more—because a broader co-occurrence horizon enables it to learn topical and thematic regularities. In applied settings, window size becomes a way of choosing between focusing on syntactic versus semantic relations: smaller windows emphasize local grammatical roles, whereas larger windows highlight looser semantic associations.
