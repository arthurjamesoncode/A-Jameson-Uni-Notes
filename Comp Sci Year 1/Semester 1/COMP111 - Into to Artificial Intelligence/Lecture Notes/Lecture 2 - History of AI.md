## First Steps: 1943-1955
- **1943** - Based on the first insights into the functioning of neurons in the brain and Alan Turing's theory of computation, McCulloch & Pitts suggest a model of artificial neural networks.
- **1950** - Claude Shannon publishes a paper detailing a program that could potentially play chess against a human.
- **1951** - Alan Turing creates [Turochamp](https://en.wikipedia.org/wiki/Turochamp), the first computer chess playing algorithm
- **1951** - Minsky and Edmonds build the first neural network computer, [SNARC](https://en.wikipedia.org/wiki/Stochastic_Neural_Analog_Reinforcement_Calculator)
## Dartmouth Conference: 1956
[The Dartmouth Conference](https://en.wikipedia.org/wiki/Dartmouth_workshop) was a two moth conference with 10 attendees. The main figures included McCarthy, Minsky, Shannon, Samuel, Newell, Simon.

Newell & Simon presented the LOGIC THEORIST program. Simon: "We have invented a computer program capable of thinking non-numerically, and thereby solved the venerable mind-body problem."

It was here that John McCarthy coined the name "Artificial Intelligence", but there were no technical breakthroughs.
## Optimism Regarding AGI: 1956-70
Promising performance of early AI systems on simple examples (integration problems, algebra problems, moving blocks) led to great expectations.

**Simon, 1957:** "It is not my aim to surprise or shock you - but the simplest way I can summarize is to say that there are now in the world machines that can think, that can learn and that can create. Moreover, their ability to do these things is going to increase rapidly until - in a visible future - the range of problems they can handle will be coextensive with the range to which the human mind has been applied."
## It Doesn't Work...: 1970
The systems from the 1960s almost always failed completely when tried out on a wider selection of or more difficult problems.

Examples:
- Translation of Russian scientific papers into English (space race between USSR and US) by simple syntactic transformations failed completely because of lack of stored general knowledge to resolve ambiguities (and for other reasons).
- Game playing programs failed because of inherent intractability (combinatorial explosion). Techniques developed for toy examples did not scale.
### Combinatorial Explosion:
In principle, it is easy to write a program playing chess by computing all possible sequences of moves up to $x$ moves, and then select an optimal move. 

However in chess there are:
- 400 different positions after one move per player
- 72,084 different positions after two moves per player
- 9x10$^6$ different positions after 3 moves per player
- 288x10$^9$ different possible positions after 4 moves per player

In practice, It's just not possible to write a program to look through each of these positions even after 4 moves, let alone more. To play chess optimally you would need far more so this strategy will just never work.

For a Rubik's cube there are:
- 43,252,003,274,489,856,000, or $4.3252\times10^{19}$, combinations
- Up to 481,229,803,398,374,426,442,198,455,156,736 or $4.8122\times10^{32}$  brute-force solution attempts

For context of how huge that number is, the 2019 Summit machine at the Oak Ridge National Lab in Tennessee executes roughly $10^{18}$ instructions per second. So it would take this extremely powerful machine $10^{14}$ seconds or $1.67\times10^{12}$ hours to compute.

Essentially, even if a program can find a solution in principle, it does not mean that it can find a solution in practice.

The Lighthill Report (1973) on AI for the British Research Council came to the conclusion that AI researchers had failed to address the combinatorial explosion problem and was pessimistic regarding research in, for example, general robotics and natural language processing. It formed the basis for the decision of the UK government to essentially end support for AI research.
## Expert Systems (Narrow AI): 1980s & 1990s
Since general purpose brute force techniques don't work, the focus changed to knowledge rich solutions.

The early 1980s saw the emergence of **expert systems** as systems capable of exploiting knowledge about tightly focused domains to solve problems considered the domain of experts.

Expert systems (combining basic logic and probability based reasoning):
- MYCIN: diagnosis infections, recommend antibiotics, diagnosis of blood clotting diseases.
- PROSPECTOR: aid geologists in mineral exploration, finding sites for drilling.

1990s: Most companies set up to commercialise expert systems technology did not survive due to some big problems:
- The knowledge elicitation bottleneck.
- Lack of trust in recommendations given by expert systems.
## Recent Successes

### IBM Deep Blue defeated world chess champion Garry Kasparov - 1997
Reasons for success: 
- Much faster.
- Machines with more storage. 
- Heuristic search algorithms.
### IBM Watson wins Jeopardy - 2011
Jeopardy! is an American television quiz show: contestants are presented with general knowledge questions they must answer.

Watson is a question answering computer system capable of answering questions posed in natural language.

In 2011, Watson competed on Jeopardy! against former winners Brad Rutter and Ken Jennings. Watson received the first place prize.

Reasons for success: 
- Progress in natural language processing and extracting knowledge from structured and unstructured content (required four terabytes of disk storage). 
### AlphaGo wins against 9-dan professional - 2016)
Go is Strategy board game for two players. The players take turns placing playing pieces in vacant intersections of a board with a 19 × 19 grid of lines.

The objective of Go is to fully surround a larger total area of the board than the opponent.

The AlphaGo computer program is created by Google DeepMind in London. In 2016, AlphaGo beats Lee Sedol in a five-game match.

Reasons for success: 
- Heuristic search not enough but there had been progress in machine learning.
### AlphaFold: Predict 3D models of protein structures - 2020
Proteins underpin the biological processes of all living beings. They are the building blocks of life.

There are more than 200 million known proteins, with many more found every year. Each has a unique 3D shape that determines how it works and what it does.

Predicting the 3D shape of a protein from its sequence of amino acids has been an unsolved challenge for over 50 years but was solved by Google Deepmind in 2020. Earning a Nobel Prize for Chemistry in 2024 for Demis Hassabis and John Jumper.

Reason for Success: 
- Progress in machine learning, in particular deep neural networks.

### Self Driving Cars: 
A ground vehicle capable of sensing its environment and navigating without human input.

In 1995, CMU’s NavLab 5 completed the first long distance drive (2,849 miles, 98.2 percent autonomous).
Self Driving Cars

There has been great progress over the past 15 years. Many car producers claim to essentially have the technology. However, trust and legal issues are major challenges.
Self Driving Cars

Reasons for Progress: 
- Better sensors
- Progress in machine learning for mapping environment and self localisation.
### Generative AI - (roughly) 2022
Systems that generate text, images, etc, by responding to prompts.
- ChatGPT, released in 2022, an example of a chatbot based on large language model GPT3 (developed by openAI);
- Current models: Claude 4.1 (Anthropic) and Grok 5 (xAI), GPT-o4-mini (OpenAI), Qwen 3 (Alibaba), DeepSeek R1 (DeepSeek), and so on.

All generative AI are based on the transformer deep learning architecture. Underpinning research published in article ”Attention Is All You Need” in 2017.

They are trained using in the order of a trillion words using networks with in the order of 100 billion parameters (2023).

The 2024 Nobel Prize in Physics was awarded to Geoffrey Hinton and
John Hopfield for their foundational work on artificial neural
networks.

## Major Challenge: Explainable AI
In many domains it is important to understand the decisions and predictions of AI algorithms. 

Examples: 
- Clinical decision support systems
- Interview support systems
- Financial advice systems.

Many AI algorithms (in particular deep learning) are naturally opaque and typically even experts cannot explain their decisions/predictions.

Lots of research currently into trying to explain to humans the decisions/predictions of such AI algorithms.
