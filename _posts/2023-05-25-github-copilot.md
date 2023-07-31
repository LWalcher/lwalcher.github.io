---
title: 'GitHub Copilot'
date: 2023-07-31
permalink: /posts/2023/05/github-copilot/
tags:
  - github copilot
  - research
---

A blog post about GitHub Copilot and its approach to improve productivity in software development using deep learning.

Github Copilot
======

Features paper: https://arxiv.org/abs/2302.06590

What is GitHub Copilot?
======
General introduction to the topic featuring terms, definitions and the current state of GitHub copilot

How does Deep Learning help with software development?
======
How can this problem be mapped to a DL problem? inputs?, outputs?, loss?, etc.
How does GitHub advertise their product? Why should you use it as a developer?

How does GitHub Copilot work?
======
Describing what DL method is used and how github copilot generates code

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
> 
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
GitHub Copilot demonstrates that deep learning can support software development. It shows the potential of AI in complementing programmers rather than replacing them entirely. The affordability of the tool is also noteworthy, with pricing set at $10 per month for individual users and $19 per month per user for businesses, making it accessible to a wide range of developers. However, it is essential to approach the study's reported 55.8% increase in productivity with caution due to the study's specific design and potential limitations. Even though Copilot appears to be a useful and promising tool, further research and real-world applications are necessary to fully investigate the true impact of GitHub Copilot on productivity in software development.

