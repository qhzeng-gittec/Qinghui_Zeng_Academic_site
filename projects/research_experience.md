# Navigating the Complexities of Research: Lessons from My Undergraduate Journey

My experience in research, particularly in applied mathematics, has given me many opportunities to explore complex problems, face challenges, and develop strategies to overcome them. Through these experiences, I've learned not only the technical skills needed for research but also the critical thinking and persistence required to push through difficulties. In this blog, I want to share some of the key challenges I've encountered in my research projects, along with the strategies and insights I've developed to address them.

While these experiences might be more suited for undergraduate projects, I plan to think more carefully about how to apply them in my graduate studies.

## Reading Papers

Reading a large number of papers is essential before starting a project. It helps build a comprehensive understanding of the field and introduces common methods that can be applied to my own research projects. Here are some efficient strategies I've developed for reading research papers.

### Understanding Backgrounds

Understanding the background of a paper includes knowing the problems it addresses, the established theoretical results, and the mathematical tools it uses. Often, a mentor would recommend papers with new methods, but these papers often assume the reader already has a strong background in the area, which can be confusing for beginners. For example, when I first read a paper on wave transfer problems, I was confused about the problem setting and the physical concepts like wave number, radiation condition, reflection, propagating modes, and incident waves.  

To tackle this, I divided the theoretical background into two parts: fundamental mathematical and physical knowledge, and advanced knowledge in acoustic studies. Just like lower and upper-division courses at university, the first part is usually more crucial for understanding because the second part often builds on it. I would search for textbooks and read specific chapters to grasp the theory without getting bogged down in detailed proofs. For more advanced topics that were harder to grasp, I realized it was better to accept some theories as they are for efficiency purposes rather than trying to derive everything from scratch. This approach helped me focus on the most relevant aspects for my project.

### Omitted Derivations

Many papers, especially in mathematics, omit some steps during proofs and derivations, assuming the reader will find them simple. However, these skipped steps can be challenging if you're not familiar with the key mathematical tools. Instead of getting stuck, I found it helpful to consult with my mentor to understand which specific mathematical theories were being applied. This approach saved time and helped me avoid getting bogged down in areas that were not essential for my project.

### Setting Priorities for Papers

A large number of papers are published every day, especially in fast-developing fields. However, not every paper needs to be read in detail; only those that seem inspiring or innovative deserve more attention. In the field of data-driven physics modeling, many papers have limited contributions. My strategy is to quickly scan papers to understand their model structures and results, then summarize their contributions in simple terms. If the contributions seem significant, I will dive deeper into their theoretical background and motivation. For example, I found the paper on the Koopman Neural Operator particularly innovative because it integrates Koopman operator theory into machine learning, showing how combining mathematical frameworks can enhance performance.

### The Limitations of Reading Papers

Reading papers alone is not enough for doing research. Papers often highlight the strengths of their methods but say little about their drawbacks, making it hard to identify areas for improvement. Moreover, papers tend to focus on theory and offer limited guidance on practical implementation. In numerical experiments, many unexpected problems can arise, and papers rarely provide detailed solutions for these issues. In such cases, seeking help from a mentor or collaborating with peers can be more effective than continuously diving into more papers.

## When Things Get Stuck

As an undergraduate, I found that my mentor wasn't always available to provide detailed guidance on my projects. Sometimes their advice wasn't enough to solve the problems I was facing. For example, in a project on wave propagation, I encountered several unexpected problems during implementation. My mentor initially thought it was a bug in my code, but the real issue was a small perturbation in the imaginary part during numerical computations, which caused a major change in the solution. I had to handle many of these unexpected problems on my own. Some of them could be explained through analysis of truncation errors and perturbation theory, but for problems that seemed beyond my understanding, I reached out to other professors via email for their insights.

## Spotting Bugs in Code

Finding bugs in code is a crucial skill in computational mathematics, even though it can be tedious. After spending a lot of time debugging, I've developed some strategies to help me spot issues more quickly.

**Test from the simplest case:**  
If the code is meant to solve a complex problem, start by testing it on the simplest case where the expected output is clear. Check each intermediate step to see if it matches expectations. If it works for the simple case, gradually add more complexity. If the code seems correct but the results are still off, consider analyzing errors introduced by the algorithm, such as perturbation theory and truncation errors.

From my experience, the "bad" problems, where the state changes dramatically, often cause failures. There was a time when I spent days checking my formulas and code for bugs, but everything was actually fine. The problem was with the inappropriate parameter settings, which caused the numerical solver to perform poorly. This taught me that numerical solvers aren't as powerful as I once thought; they are useful when exact solutions are hard to find, like in fluid dynamics problems. However, to fully understand the problem, it's important to approach it from a theoretical perspective as well.

---

I hope these insights and experiences can be helpful for anyone starting their journey in research. Research is not just about reading papers or running simulations; it's about understanding the underlying concepts, questioning assumptions, and finding innovative solutions to problems.
