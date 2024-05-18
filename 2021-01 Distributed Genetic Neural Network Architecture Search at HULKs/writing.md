---
title: General Paper Writing Advice
author: Lasse Peters
---

# Writing Strategy:

Writing Order: Try to write as much as possible in chronological order, but write the abstract late.

- In particular, write the introduction and related work *early*.
- Once you arrive at the conclusion, much of the paper will already have
  converged. If you reach this point, revisit the introduction and make
  sure that the story is consistent. (Motivation and key
  results/contributions still aligned what you wrote in the introduction.)
- You can write a draft of the abstract early but write a refined version
  of it late. It is good to be concise and it makes sense to spend some
  time on polishing this bit as much as possible.

- Go through the phases below.
    - Phase 0 and 1 *must* come first and happens only once.
    - All other phases can be done per section or in sync for all sections
        - This part allows parallelization of the writing process.

## Phase 0: Literature Review

- Only start after a good literature review to get *good overview over related work*

## Phase 1: Sketching the Section Layout

- Sketch the overall layout of the paper. Mostly this will be pretty standard
    - Abstract
        - Summarize in the shortest possible way:
            - 1-2 sentences: What is the problem and why is it relevant
            - What does this work do to address this problem.
            - What are the main results.
    - Introduction
        - Provide a good motivation for why this is a relevant research problem.
    - Related Work
        - Review relevant previous work and relate it to the approach / work in this paper.
            - Which work does this paper take inspiration from?
            - What are important differences of this work to the existing previous work.
    - Optional: Contribution
        - Sometimes it is good to have a specific section on what are the
          contributions of this paper. But often this can be stated as
          a paragraph at the end of the "Related Work" section or even the
          "Introduction"
    - Problem Formulation
    - Method
    - Experiments / Results
    - Conclusion
        - Recap what has been done in the paper. At most one or two sentences for each section.
        - State the main results; again only one or two sentences for this.
        - State limitations and derive possible future directions of work.


# Phase 2: Story Design.

- Roughly outline sections in bullet points first. At least their structure
    - This can also be just questions that need to be answered in a specific order.

# Phase 3: Flesh-Out.

- In a first "flesh-out" pass for each section try to "make meters"
    - Don't spend too much time on being concise. Just try describe
    - Write with a `Pomodoro` strategy to ensure focus and progress so that you
      don't get caught in oscillation between paragraphs or small details of
      formulation (you will have time to streamline later.)
        - Define *what* to work on in a short time slot.
        - Then make as much progress on that part as possible in each `Pomodoro`.
        - Take the breaks seriously to ensure good progress over a longer period of time.

# Phase 4 Polishing and Compression

- Go over the section(s) again and polish them. Try to make them more concise
  and avoid duplications in the body.
    - Note: It is okay to repeat statements from the body of the paper in the
      Introduction, Abstract, or Conclusion. But don't repeat thing *withing*
      these sections or within the body (unless it's a really important
      statement that needs to be emphasized. This is very rare.)

# Tooling

- [Academic Writing Check](https://github.com/devd/Academic-Writing-Check)
- [Purdue Online Writing Lab](https://owl.purdue.edu/owl/general_writing/punctuation/commas/extended_rules_for_commas.html#:~:text=2.,%2C%20since%2C%20when%2C%20while.)
- [github.com/lassepe/](https://github.com/lassepe/latex-setup-clean)

# Examples of Good Writing

- Good related work
    - [Fisac2018General](https://arxiv.org/pdf/1705.01292.pdf)
    - [Fisac2018Proabilistically](https://arxiv.org/pdf/1806.00109.pdf%3E)

- Good introduction
    - [Fisac2018Hierarchical](https://arxiv.org/pdf/1810.05766.pdf)
    - [Dorsa2016Planning](https://pdfs.semanticscholar.org/baef/0a1859fc0216c89289c69da88d6dc8399fc7.pdf)

- Good Framework Paper
    - [Egorov2017POMDPs](https://www.jmlr.org/papers/volume18/16-300/16-300.pdf)

# Common Grammar Mistakes to Check for in the End

- "require to reason" is wrong. Rather, just "require reasoning"
