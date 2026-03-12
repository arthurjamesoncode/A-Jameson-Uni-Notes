## What is Generative AI
Generative AI are programs which take, as an input, a prompt and then output some piece of data. This could be text, an image a video code etc.

Examples include:
- GitHub Co-pilot
- ChatGPT
- Gemini
- Midjourney

Gen AI that produce text are called Large Language Models, or LLMs.

They are becoming more and more intelligent/powerful. Below you can see a figure which indicates how various Gen AI models performed on various exams. As you can see, some models performed in the top 10% of would be human candidates.
![[gen_ai_performance.png]]

An exam created to measure the intelligence of LLMs is called Humanities last exam. It is an exam with 2500 PHD level questions from 100 different subjects, such as medicine, computer science, maths, etc.

Below you can see an image of a sample question from this exam, as well as a table showing how various LLMs have performed when taking it.
![[last_exam.png]]
## What is a Large Language Model
As stated above, a generative AI that can produce natural language is called a Large Language Model or LLM.

An LLM is a probabilistic model that generates text. Given a sequence of words, the LLM predicts a word that would make the most sense to come next.

So if given the sentence "I had bread and butter for __ ", an LLM would attempt to find the token (word) $X$ for which $P(X\;|\;\text{I had bread and butter for})$ is maximal.

Language models have been around for ages. Alan Turing was working on this in the 1940s. 

You can see a timeline of recent developments in language models below. If you want to read more about them you can look at that [here.](https://arxiv.org/abs/2402.06853)
![[lm_history.png]]

Unlike early "statistical" language models, LLMs use neural networks to "predict" the next word given the previous context.

Whenever you give one a "prompt" you are giving it this "pre-context" and the LLM will generate one word at a time util it has completed a response.

LLMs use massive neural networks, containing over 1 trillion parameters/neurones. This is why they are called **Large** language models.

LLMs are powered by the **Transformer** architecture. This is the **T** of GPT, which stands for "Generative Pre-Trained Transformer".
## Transformers
Below you can see a diagram of the transformer architecture proposed in the paper [Attention is all you need](https://web.stanford.edu/~jurafsky/slp3/slides/transformer24aug.pdf) which was published by authors from google.

![[transformer_architecture.png]]

Going from the bottom you can see that the transformer takes, as an input, various tokens (words) which are represented as a vector, and have their position in the statement appended on to the end.

The middle layer is "stacked transformer blocks", this is the multi layer neural network into which the input is fed. Based on the current, and previous, input tokens it chooses the word which is most likely to come next given the context. Once it has this word it adds it to the context and then takes it as input again.
## Attention
In Masked Language Modelling, we have a sentence and we hide a word from the agent. We can use this to train LLMS.
![[sentence.png]]

![[masked.png]]

We can use this to generate labelled training data (You can read more about supervised learning in [[Lecture 27 - Machine Learning]]).

Now given the other word in the sentence, can we predict the hidden word? If we have, then we have learnt a model that can predict words based on previous ones.

Attention is essentially how important each other word in the sentence is with regards to the current word. You can see a sample attention distribution below
![[Attention.png]]

The transformer model has three main components it needs for computing the "attention" we should pay to each word in the context when making a prediction:
- Query ($Q$) - Our target word
- Key ($K$) - Other words in context
- Value ($V$) - embeddings of words

Given these, it can compute attention using the following formula$$
Attention(Q,K,V)=softmax(\frac{QK^T}{\sqrt{d_k}})V
$$
You can think of this as a key value store. We match each value in this store (represented by the key) against the query, and take the (weighted) sum over the values of those keys.

If the key is relevant to the query (has high attention) then that relevance will be used to weight the value corresponding to the token for the key.

In the case of text, each word is considered to be represented by an "embedding" (vector) in some fixed dimensional space.

$softmax$ is a function that takes the max of a given set of values, but in a soft manner. 

What this means is that instead of returning the maximum of this set of values it returns a new set of values, that all add up to 1, representing a probability distribution.

The formula for $softmax$ is below $$
sofymax(\vec{c})_i=\frac{exp(z_i)}{\sum_{j=1}^Kexp(z_j)}
$$where $exp(z_i)=e^{z_i}$ 

Below you can see a full example of the computing of attention.
![[attention_computation.png]]

We then learn a query weight matrix $\textbf{W}_Q$, a key weight matrix $\textbf{W}_K$ and a value weight matrix $\textbf{W}_V$ which will transform the query, key and values corresponding to the inputs.

Modern transformer models contain multiple sets (known as heads) of such matrices, and have many layers (for example 12 or more).

GPT-3 has 175 billion parameters for example.
## I give up
I cannot be arsed to write down notes for this whole lecture. There are 60 slides on a topic that we don't need to know much about yet. There, at max, will be 1 question on this which I don't think he can make too hard, since this is so far out of scope for "Intro to AI"
