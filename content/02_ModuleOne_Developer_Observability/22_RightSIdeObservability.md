---
title: "Right-side Observability"
chapter: true
weight: 2
---

# Observability Belongs to the Operators
 
Observability is traditionally an operator's game - let's take a moment to investigate why.

## Developers VS. Operators

The divide between developers and system operators has been around forever: Developers design and write code for the application, which, in turn, is running on infrastructure that operators (DevOps engineers, cloud engineers, etc...) build, maintain and observe.

Observability — the practice of examining the internal state of a system simply by looking at its outputs — is, therefore, mostly reserved for operators. System output is an ops, not a dev, problem. Developers own the inputs, but not the outputs — they’re too far removed from the actual application that is built from the code they originally wrote.

In essence, observability is a [right-side (when speaking of the SDLC)](https://en.wikipedia.org/wiki/Systems_development_life_cycle),
post-deployment concern, meant for operators and operators alone. 

Once the system is up and running, it is expected to emit information geared towards allowing an operator to understand what’s going on inside of it. The operator is not expected to push new code or otherwise significantly alter the state of the system to get more information — it should already be there. That is a truly *observable system* - one that tells you what's going with it, instead of asking you to dig deep through its interiors to collect each sliver of information.

## Shifting Left Observability

A major trend sweeping our industry is to make common practices more “developer-friendly,” often referred to as “shifting left” — referring to the act of “pushing” steps from the right side of the software development life cycle (SDLC) to the left side:

   ![Shifting Left Observability](/images/02_Developer_Observability/right-side-observability-1.png)

One might ask where this trend is coming from - we believe it’s mostly about the fact that **giving developers more power** in various parts of the SDLC **yields tremendous benefits** for both developers and the companies they work for. We can roughly divide the reasons into three main themes:

1. **Developers Expected to Own Reliability** - The shift towards DevOps has placed the responsibility of reliability on developers. However, the current observability tools primarily focus on analyzing static data from logs and metrics, which often does not provide a comprehensive understanding of the running systems. This results in a gap in information availability and makes it difficult for developers to fully own reliability. The lack of ability to actively ask questions and get immediate answers from the applications raises concerns about the feasibility of expecting developers to maintain reliability.

2. **Applications Becoming Exponentially More Complex** - With the increasing complexity and distribution of production environments, there is a growing disconnect between live applications and the development process. This makes it challenging to predict and reproduce issues, leading to an increased adoption of testing in production. The widening gap between development and production further exacerbates the difficulty of addressing production incidents that involve developers' code.

3. **Existing [o11y](https://lightrun.com/observability/observability-vs-monitoring/) Tools Focus Mainly on Operators, not Developers** - Observability is not widely practiced among the [approximately 27 million developers worldwide](https://www.developernation.net/developer-reports/dn21), with existing observability tools primarily catering to operators. This creates a challenge as developers often lack familiarity with dashboards and configuration files, leaving them in the dark during production incidents that involve their code. The gap between what developers know and understand about their deployed code highlights the need for observability tools that cater to the development community.

Lighturn, the Developer Observability Platform, was built specifically to make sure developers get the observability they deserve - without sacrificing on ergonomics and in a safe, reliable fashion. 