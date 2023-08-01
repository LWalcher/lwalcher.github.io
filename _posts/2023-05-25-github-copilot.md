---
title: 'Recent Applications of Machine Learning - GitHub Copilot'
date: 2023-07-31
permalink: /posts/2023/05/github-copilot/
tags:
  - github copilot
  - research
---

A blog post about GitHub Copilot and its approach to improve productivity in software development using deep learning.

Github Copilot
======

GitHub Copilot is an innovative "AI pair programmer" tool developed collaboratively by GitHub and OpenAI. It was officially released in October 2021 and offers a powerful code autocompletion and suggestion system. Copilot is compatible with various integrated development environments (IDEs) such as Visual Studio, Visual Studio Code, and IDEs from the JetBrains family. It is suited best for coding in Python, JavaScript, TypeScript, Ruby and Go. 

How does Deep Learning help with software development?
======
To understand how deep learning can be applied to software development, it is important to understand the basic concept of deep learning. Deep learning is part of the machine learning field. It utilizes a neural network, that tries to mimic the human brain using a combination of data inputs, weights, and bias. Deep neural networks are composed of multiple interconnected layers of nodes, with each layer refining and optimizing predictions or categorizations from the previous layer. This progression of computations is known as forward propagation. The visible layers in a deep neural network are the input and output layers. The input layer receives the data for processing, while the output layer generates the final prediction or classification.
To train the model, a process called backpropagation employs algorithms like gradient descent to compute prediction errors and adjust the weights and biases by moving backward through the layers. This iterative process allows the neural network to make predictions and correct errors progressively, leading to increased accuracy over time. 
An important metric for this process is the loss function. It measures the error between predicted values and the actual or expected values. The goal of training the model is to minimize the output of the loss function or in other words: Given any input the model will accurately provide a corresponding output.
How can this be applied to software development? A programmer typically does not “reinvent the wheel”. Although there will always be new and innovative algorithms, they can always be broken down to smaller problems. At that point there is a high chance, that this problem has already been solved by someone. Thanks to platforms like GitHub and Stack Overflow, software developers have unlimited access to code snippets and answers to common coding challenges. Combined with personal experience, these problems can then be solved. To depict this as a deep learning model, we need to define our inputs, outputs, and our loss function. The following illustration provides a simple example of such a model.


![Example Neural Network](/images/network.png "Example Neural Network")

In the input layer the model is provided with a code snippet representing the current problem. E.g. the Java code:

  `public void printHelloWorld(){`

Then the model will, if thoroughly trained, understand the context of these lines of code, while passing the input data through various hidden layers and generate the following output:

`public void printHelloWorld(){
  System.out.println("Hello World");
`

Achieving good results requires extensive training of the model. For this use case it a large amount of code snippets and their completed counterparts are necessary as prerequesites. Additionally, a loss function must be defined, so that its values are minimized, when the predicted code is semantically and syntactically equal to the expected code. How GitHub Copilot managed to achieve this, will be shown in the following section.



How does GitHub Copilot work?
======
GitHub Copilot is developed using OpenAI's Codex, which is a variant of the Generative Pre-trained Transformer (GPT) architecture. It is a deep learning model, specifically a transformer model. The underlying model is trained on a combination of natural language data and billions of lines of source code from GitHub. 
To fully grasp how GitHub Copilot works, it's essential to understand the GPT (GPT-3) architecture. Similar to our example neural network above, GPT's model has an input and an output layer. The input is handled as a set of tokens in a sequence. Given the text *We all live in a* produces the following table-like data.

| \<s\> | we | all | live | in | a | yellow |
|-----|----|-----|------|----|-----|----|
|  0   |  1  |  2  |  3  |  4  |  5   |  6  |

GPT then predicts the next token in this sequence. The output layer receives a set of guesses with their corresponding probabilities. In this example an output could look like this:

- submarine (90%)
- taxi (5%)
- banana (1%)
- ...

These layers are what the user typically interacts with. When looking at the following figure, it becomes clear how many steps are actually necessary in between.

![GPT Architecture](/images/gpt2.png "GPT Architecture")
  > Radford, A., Narasimhan, K., Salimans, T. and Sutskever, I., 2018. Improving language understanding by generative pre-training, Figure 1: The transformer - model architecture

The first step is the encoding of the input. The input sequence's size is fixed to 2048 tokens. In our example above all remaining positions would be filled with empty values. To process this sequence of tokens they will then be translated to a vector of numbers. In order to do that GPT has a vocabulary of 50257 tokens, represented as a vector. Each token is represented by a 50257 long vector with all values set to 0, except the position of the token in the vocabulary, which is set to 1. It is worth noting, that these tokens are not full words, but group of characters that appear often in texts. The result of the encoding is a 2048x50257 matrix of ones and zeroes.
As a next step input embedding is necessary to process this large data set. Embeddings are provided as a matrix in the model, representing weights learned during training. These embeddings capture semantic relationships and help the model make accurate predictions in various language tasks. This is achieved by multiplying those 2 matrices.
Next up positional encoding is performed through which the model can understand the sequential order of the tokens. This is followed by Multi-Head Attention. Attention in general predicts which input tokens to focus on and their importance for each output in the sequence. It involves learning three weight matrices (queries, keys, values) to transform sequence embeddings. By multiplying the queries and keys matrices, it calculates the importance of each token to others, resulting in a matrix that influences the weighted mix of token values. For Multi-Head attemption this process is repeated 96 times. This allows the model to understand contextual relationships between tokens in the sequence. The process continues with Feed Forward, which is a multi-layer-perceptron with one hidden layer. It multiplies the input with learned weights, adds the learned bias and multiplies it with weights a second time. After each of the last two steps, Add & Norm is performed which adds the input of the current step with its output and normalizes the result.
After passing through all these steps, the input is transformed into a 2048 x 12288 matrix, with each position containing information about which token should appear in the sequence. To extract this information, the model reverses the mapping used in the embedding section to transform the output matrix back into a word encoding. By using softmax, the values are treated as probabilities for each word.

Utilizing this powerful model architecture and the extensive training GitHub Copilot is able to provide relevant completions, functions, or even whole code blocks. The following picture shows an example of Copilot providing unit tests for a given method.


![Copilot Example](/images/copilot.png "Copilot Example")
> https://github.com/features/ GitHub Copilot Example

The user is also able to provide feedback to Copilot to further improve and personalize suggestions.

Influence of GitHub Copilot on productivity
======
To investigate GitHub Copilots influence on the productivity of software developers a research team consisting of Sida Peng (Microsoft Research), Eirini Kalliamvakou (GitHub Inc.), Peter Cihon (GitHub Inc.) and Mert Demirer (MIT Sloan School of Management) conducted a [study](https://arxiv.org/abs/2302.06590) with 95 participants. The study took place between May 15 and June 20 of 2022 and claimed to be one of the first studies regarding the effects of GitHub Copilot, which was released in October 2021. 

**Study Design.** The participants were randomly divided into two groups: the treated group, which had access to GitHub Copilot, and the control group, which was not allowed to use the tool. Before the experiment, demographic information on the groups was gathered via an entry survey. 
The treated group was given a 1-minute demo video and a setup guide for GitHub Copilot. Both groups were instructed to complete a task of writing a simple HTTP server in JavaScript.  The researchers measured task success and completion time as performance metrics for each group with the experiment starting at the time the repository was created. GitHub Classroom, a platform for coding assignments, was provided to complete the task and give access to a test suite to validate the participants submissions. To complete the task, the application had to pass 12 tests. A fast completion time would reward the participants with a higher monetary compensation. After the experiment, participants were asked to supply feedback on the usefulness of GitHub Copilot. For this exit survey both, the treated and control group, should give an estimation of the productivity gain through Copilot.

**Results.** Of the 45 developers in the treated group and the 50 in the control group, 35 each completed the task and the surveys. The demographic information gathered from these surveys is important for classifying further results and is shown below.

![Experience of the participants](/images/demogr1.png "Experience of the participants")

![Origins of the participants](/images/demogr2.png "Origins of the participants")
> The Impact of AI on Developer Productivity: Evidence from GitHub Copilot, Figure 5: Summary statistics of the experiment

Most participants were between the age of 25 to 34 age group and came from India and Pakistan, with relatively lower income compared to the US. The participants had high education levels with the largest group having a 4 year degree and the second largest with a professional degree. The majority was either employed or self-employed. On average, they had six years of coding experience and spent about nine hours daily on coding.



The treated group, using GitHub Copilot, completed the task in an average of 71.17 minutes, while the control group took 160.89 minutes. Therefore, the treated group completed the task 55,8% faster. The results are shown in the following image.

![Time to complete the task](/images/timecompleted.png "Time to complete the task")
  > The Impact of AI on Developer Productivity: Evidence from GitHub Copilot, Figure 6: Time to complete the task
  > 
  > Note: There is no information about the brown elements of the bar chart in the paper featuring the study, but it can be assumed that they depict participants, who have not completed the task successfully.

It can also be mentioned that the treated group's success rate was 7 percentage points higher than the control group, although this difference was not statistically significant. 
Taking the demographic information into account, an analysis was done to see if there is a specific group that benefits more than others from Copilot. The results are shown in the table below.

![Heterogeneous Treatment Effects](/images/table.png "Heterogeneous Treatment Effects")
  > The Impact of AI on Developer Productivity: Evidence from GitHub Copilot, Table 1: Heterogeneous Treatment Effects

According to these findings less-experienced developers, developers with many hours of coding per day and developers in the age group 25-44 benefit the most from Copilot.
Finally, the participants had to give a self-estimation on the benefits of Copilot. The following figure shows, how much productivity gain each participant anticipated when using this tool.

![Anticipated Productivity](/images/productivity.png "Anticipated Productivity")
  > The Impact of AI on Developer Productivity: Evidence from GitHub Copilot, Figure 7: Self-estimated productivity gain

Surprisingly even a large part of the control group expected a 50% increase in productivity. But in both groups there were also participants, who claimed that Copilot has a negative impact on productivity.
Overall the exit survey revealed that both groups underestimated the productivity gain from using Copilot, with an average estimated increase of 35% compared to the actual 55.8% increase that resulted from the experiment. 

Discussion
======

**Pros.** GitHub Copilot offers a user-friendly experience, making it easy to integrate into existing development workflows. Its intuitive interface and AI-powered code completion capabilities contribute to increased productivity, benefitting both experienced and novice developers. Senior Developers can utilize it for simple and repetitive tasks, e.g. writing tests, and reduce the risk of making errors. For those new to programming, Copilot serves as a valuable resource by assisting in the initiation of their projects, providing helpful suggestions and information.

**Cons.** Despite its promising features, GitHub Copilot comes with certain limitations and potential drawbacks. There is no guarantee of code quality when using the tool, as it may generate code that is not optimal or may introduce bugs. Its performance in large-scale projects has not been fully tested and validated, raising concerns about its suitability for more complex software development tasks. Additionally, there are legitimate worries about privacy and security, as the AI-powered code completion tool may access sensitive code or inadvertently leak proprietary information. Finally, while GitHub Copilot aims to enhance productivity, there is a possibility that it could negatively impact the learning experience for programmers by reducing the need for hands-on coding and problem-solving.

How meaningful was this study?
=========
The experiment involved a very basic programming task, which may not fully represent the complexity of real-world projects. The project was developed from scratch, rather than integrating Copilot's code completion into an existing larger-scale project. Furthermore, the evaluation of performance relied solely on 12 tests, lacking any assessment of code quality. 


Conclusion
======
GitHub Copilot demonstrates that deep learning can support software development. It shows the potential of AI in complementing programmers rather than replacing them entirely. The affordability of the tool is also noteworthy, with pricing set at 10 dollars per month for individual users and 19 dollars per month per user for businesses, making it accessible to a wide range of developers. However, it is essential to approach the study's reported 55.8% increase in productivity with caution due to the study's specific design and potential limitations. Even though Copilot appears to be a useful and promising tool, further research and real-world applications are necessary to fully investigate the true impact of GitHub Copilot on productivity in software development.

Sources
=======
1. Peng, S., Kalliamvakou, E., Cihon, P. and Demirer, M., 2013 [The Impact of AI on Developer Productivity: Evidence from GitHub Copilot](https://arxiv.org/abs/2302.06590)
2. [GitHub Website](https://github.com/features/)
3. Radford, A., Narasimhan, K., Salimans, T. and Sutskever, I., 2018. [Improving language understanding by generative pre-training](https://www.cs.ubc.ca/~amuham01/LING530/papers/radford2018improving.pdf)
4. Radford, A., Wu, J., Child, R., Luan, D., Amodei, D. and Sutskever, I., 2019. [Language models are unsupervised multitask learners](https://cdn.openai.com/better-language-models/language_models_are_unsupervised_multitask_learners.pdf)
5. Brown, T., Mann, B., Ryder, N., Subbiah, M., Kaplan, J.D., Dhariwal, P., Neelakantan, A., Shyam, P., Sastry, G., Askell, A. and Agarwal, S., 2020. [Language models are few-shot learners. Advances in neural information processing systems](https://arxiv.org/pdf/2005.14165.pdf)

