---
title: "Myth-busting the impossibility of functional programming hiring"
author: Phil Curzon
date: Oct 1, 2026
tags: [Functional programming, Hiring, Haskell, Scala]
description: A discussion of whether hiring for niche functional programming languages makes finding candidates a near impossibility or whether it might simplify the recruitment process.

---

> Functional programming? Haskell? Hiring must be virtually impossible?!

I've been an Engineering Manager for seven years and, for six of those, I've worked with what you might call _relatively niche_ technology, Haskell and Scala being prominent among those. Throughout my career, some variation of the question above is something that I've heard dozens or perhaps even hundreds of times - typically in response to talking about the technology we use.

If you're reading this as someone from a more mainstream technology background, you might even think the above statement is obviously true. After all:

- Engineering hiring is, broadly, hard
- Functional programming communities are significantly smaller than mainstream language communities
- Despite smaller communities, there are dozens of wildly different libraries and frameworks

All of those are true individually but, in this article, I'm going to try and convince you that, when engineering hiring is looked at holistically, it is actually _easier_ rather than _harder_ to hire within these niche communities. I'm only going to address the relative ease of hiring in this article - I'm not going to consider at all whether there are any technical merits to languages like Haskell and Scala.

## The Hiring Process

Before we can understand how technology impacts the hiring process, we need to understand that process in detail and the problems that it's designed to solve. Most of the organisations that I have worked in, regardless of technology, have structured their interview process something like this:

- Quick screening call
- Take-home coding exercise (time-boxed)
- Coding interview (typically continues the take-home task)
- Architecture interview
- Behavioural interview

Some organisations might roll multiple steps into one larger interview but, broadly, the outline is strikingly similar. However your organisation does it, the process is like a funnel: some candidates will be rejected at each step of the journey; some will reach the final stage and ultimately go to be hired.

It will probably surprise no-one reading this to hear that, as an EM, the part that I care about in this process the most is the behavioural interview. If you want to build an organisation that is successful in the medium to long term, you need to bring in people who engage with each other in a way that is fundamentally constructive: helping one another to learn from their mistakes, sharing knowledge proactively so individuals don't become single points of failure, taking things off each other's plates at the right moment to prevent burnout, and broadly making work a friendly and inclusive environment for everyone.

When I was at ITV, the hiring philosophy we used in engineering was based on the idea that we would look for engineers who are "smart and kind." I still love this as a summary of the hiring process because it encodes a lot of information into such a short and concise description.

Behavioural interviews, despite their importance, are typically done as the final stage of the hiring process: the point where the final decision is taken. The consequence of this is that the key question that influences the difficulty of hiring is: how many candidates reach the behavioural interview stage? If very few candidates reach this stage it's both very difficult to make hires and very difficult to be selective about behaviour.

To help visualise this, I'd like to encourage you to imagine two scenarios.

> Please note the scenarios I'm going to describe below are hypothetical for the sake of convenient illustration and simple mathemetics: real hiring processes are much more complicated with each stage taking different amounts of time, having different pass rates and different numbers of interviewers involved in each one.

### Model 1 - Wide Funnel

Suppose that at each stage of the process, each candidate has a 50% chance of being selected to proceed to the next step and that each step takes 30 minutes on average:

![Hiring Model 1](/images/Hiring_Model_1.svg)

In this process:

- 64 candidates submit CVs for the role that are reviewed
- 32 candidates undergo screening calls
- 16 candidates are selected to complete take-home exercises
- 8 candidates proceed to the coding interview
- 4 candidates proceed to the architecture interview
- 2 candidates reach the behavioural interview
- 1 candidate is hired

64 candidates must apply to make one hire. This means making one hire requires ~63 hours of total review/interview time.

### Model 2 - Narrow Funnel

Now imagine a new process in which only the behavioural interview has a 50% success rate and the other stages are passed by 80% of candidates and, again, that each stage takes 30 minutes on average:

![Hiring Model 2](/images/Hiring_Model_2.svg)

In this process:

- 6.1 candidates submit CVs for the role that are reviewed
- 4.88 candidates undergo screening calls
- 3.9 candidates are selected to complete take-home exercises
- 3.15 candidates proceed to the coding interview
- 2.5 candidates proceed to the architecture interview
- 2 candidates reach the behavioural interview
- 1 candidate is hired

~6 candidates must apply to make one hire. Making one hire now requires ~11 hours of total review/interview time.

I hope it's uncontroversial to say that Model 2 is strictly better than Model 1: the vastly reduced interview time means that every interviewer will be fresher and more engaged, the candidate can expect more meaningful engagement and feeeback, and your engineers will spend more time engineering rather than interviewing.

Now suppose that we have to pay a price to live in the world of Model 2: the candidate pool is 10x smaller! 

With a 10x smaller candidate pool we should assume that candidates will arrive into a model 2 process at a rate that is 10x lower: this has approximately zero impact on the rate candidates are hired because model 2 makes a hire from approximately 10x fewer candidates. At the same time, the size of the candidate pool makes no impact at all on the interview and review time required to make a hire. This means model 2 does not affect the rate of hiring but does result in saving ~50 hours of review and interview time per hire.

## Functional Programming and Selection

Okay, I admit: so far, I've cherry-picked some numbers to make a completely hypothetical case about two hiring processes. In order to convince you that functional programming makes hiring easier, I need to demonstrate that functional programming results in dramatically fewer candidates being rejected during the technical parts of the interview, so why might that be the case?

Allow me to suggest one possibility: __what if niche functional language experience selects _for_ overall engineering experience?__

Okay, but why?

### The horrors of the Haskell tutorial

Haskell is quite a difficult language to learn: not because it is particularly hard but because it is extremely different to other programming languages. It is lazily-evaluated by default, it uses immutable data structures pervasively, it is referentially transparent and side effects are performed monadically, it talks about category theory and weird mathematical constructs like endofunctors, monoids and burritos (okay, maybe not the last one!).[^noteburritos]

I don't think it would be particularly difficult for someone completely new to programming to learn Haskell: assuming they had suitable tutorials to learn from. It is, however, quite difficult for existing engineers to learn Haskell because it's so different to everything they've likely ever encountered before.

The [Haskell MOOC course](https://haskell.mooc.fi) is generally regarded as one of the best and most accessible courses for learning Haskell. On the very first page, we are confronted with comments like this:

> __Strongly typed__ - every Haskell value and expression has a type. The compiler checks the types at compile-time and guarantees that no type errors can happen at runtime. This means no AttributeErrors (a la Python), ClassCastExceptions (a la Java) or segmentation faults (a la C). The Haskell type system is very powerful and can help you design better programs.

Comparisons to three other programming languages. And those comparisons continue pervasively throughout the course with numerous examples of how Haskell programs different in both structure and expectation from Python, Java and C.

My point here is not to criticise the course - I actually think it's very well put together but the level of assumed experience for a beginner course is tremendous. The course is also constructed with its audience in mind: most people who take it have experience with at least one of those languages already, often several. It's also better than most other options for learning Haskell. One of the most recommended beginner-friendly Haskell books begins with an introduction to lambda-calculus. Again, an excellent book but hardly accessible to a wide audience.

In the Scala world, "The Red Book" (Functional Programming in Scala) is one of the best and most influential programming books I've ever read but it's an excellent resource for established engineers wanting to learn something new, not learning material for a complete beginner. Broadly speaking, functional programming in Scala uses many of the same concepts as Haskell while offering a probably more familiar runtime environment (the JVM).

### Argh! That can't possibly be good!

No, it isn't and I'm not going to sugar-coat that. I wish there were a genuinely beginner friendly Haskell book that assumed no prior programming experience at all. I've often thought about writing that book but I'm not sure an audience for it exists.

For a hiring manager though, the barrier to entry is somewhat useful: it's a filter that your interview process doesn't have to replicate.

How many times have you sat in an interview and watched someone do something incredibly naive like using `String`s as signalling values, getting tied in knots by reference vs value equality, silently swallowing exceptions or creating giant and ill-founded chains of inheritance hierarchies? The number of Haskell engineers you will find making such mistakes is, for all intents and purposes zero.

More broadly, the language is doing the heavy lifting for your technical interview process. Candidates who are unlikely to progress through your technical interview stages simply do not know esoteric functional programming languages. **No one likely to fail a technical interview would realistically have made it to the other side of learning one.**[^note1]

### Recruiter relationships

In a world of mainstream technology, relationships with recruiters can be incredibly transactional. They have many candidates with very similar experience and CVs on paper and they want to get them in front of as many companies as possible: it's very difficult for you to stand out as an organisation or for them to supply consistently outstanding candidates you're likely to hire.

In a world of niche functional programming your organisation suddenly becomes _interesting_ to recruiters. All of the candidates that have that experience on their CV are coming straight to you and the small group of organisations doing something similar. This allows both parties to become much more predictable to one another: the recruiter knowing that if they find a candidate with the relevant experience, you are very likely to hire them and your organisation knowing that they are likely to bring you candidates of interest that will get to the end of your hiring process.

## Framework and Library Experience

At the very start of this article, I spoke briefly about the plethora of different frameworks and libraries available within the world of functional programming. Surely this is still fatal and finding matching experience for your chosen technology is going to be impossible despite every other argument I've made?

The answer is: Yes - it is almost impossible but it isn't fatal and is actually another advantage.

Suppose that you hire an engineer who has ten years of experience with Spring Boot: it's entirely possible that that engineer does not understand, in detail, the layers underneath. I've interviewed, on paper, very experienced engineers who couldn't explain the details of what an HTTP request actually looks like because they had spent their careers in the world of a single framework.

Contrast that with someone who has seen Spring Boot (Java), axum (Rust), http4s (Scala) and servant (Haskell). They've seen, learnt and debugged four fundamentally different variations of the same thing. What's the big deal about learning another one?

More broadly, engineers who are particularly adept at using frameworks understand the _intent_ of the framework's abstraction and _why_ it exists as well as the content of it and that is actually better served by having seen it represented in half a dozen different ways.

## What about Juniors?

Maybe I've convinced you that functional programming experience selects for experienced engineers but how on earth do you hire juniors? Surely all the factors that I've argued are helpful now work in the opposite direction?

This is true but it matters less than you might think. Indeed, you are probably not going to find a pool of junior engineers to draw from with functional programming experience. There is a relatively small group of, usually fairly elite, universities that teach some form of functional programming as part of their curriculums. It is somewhat more common amongst those with a post-graduate academic background but there is no doubting that this is a really small pool. If you aren't recruiting in close physical proximity to one of those institutions, you aren't going to come across many of them.

Fortunately, specific language experience doesn't matter much when hiring juniors. Yes, you're back in the world of traditional technical screening, drawing from the same pool as every other language. But the juniors you hire will be surrounded by experienced engineers, most of whom made the same transition from imperative languages themselves. That goes a long way to making up for the weakness of functional programming learning materials.

Juniors also have an advantage: they haven't yet internalised the habits that make functional programming so hard for experienced engineers to learn.

If you need a lot of juniors all at once, it's possible to run a dedicated bootcamp in your language/chosen technologies to accelerate the learning timeline even more. Earlier in my career, I was involved in hiring over 20 juniors over the course of two months to fill a Scala programming bootcamp which lasted ~4 weeks. I was an engineer at the time so I don't have exact statistics to share on success rates but I remember being extremely impressed by the quality of Pull Requests coming from the bootcamp graduates immediately after they were distributed into their respective teams. I have managed several of those bootcamp graduates in the intervening years and many are now, themselves, extremely experienced senior and lead engineers.

Unsurprisingly, Juniors are able to progress and thrive astonishingly quickly in an environment where they are surrounded by high quality engineers who are committed to helping them succeed and grow. The first follows from the technical skills of the community, the second follows from a focus on behavioural hiring.

## Conclusion

So, to finally answer the question posed at the start:

No. Niche functional programming languages do not make hiring any more difficult and they often make it easier. The technical experience of candidates in this domain lead to a much narrower hiring funnel that is nicer to be involved in as a candidate, interviewer and hiring manager. It allows your entire interview process to focus more on behaviours rather than assessing technical competence: finding out more about the individual you are interviewing and whether they would be a positive addition to your team.

Every candidate who arrives in the world of a niche functional programming language has an interesting story to tell about the journey that led them there and that material is perfect for an interview setting: to understand the applicant and how they go about making proactive choices about the future of their career.

I've seen no evidence that engineers from functional programming communities are more capable or highly skilled than the leading engineers from mainstream language communities: only that the proportion of leading engineers within functional programming communities is significantly higher.

As a hiring manager, it's lovely to operate in a world in which a relatively small number of candidates are processed. That way the interview process can be more personal and even if a candidate isn't ultimately successful, they can be given detailed and meaningful feedback that isn't just superficial, is genuinely constructive and might even help them in future applications.

Having a smaller overall candidate pool absolutely is a side-effect of choosing a functional language but the size of the candidate pool only affects the difficulty of recruitment if everything else about the recruitment pipeline stays the same. What genuinely affects the difficulty of hiring is how many people make it to the final interview stage.

I'm certain that hiring in niche language communities isn't the only way to narrow the recruitment funnel to leading engineers and create a hiring pipeline that looks more like model 2 than model 1. What tricks do you use in your organisation to do this?

[^noteburritos]: [Burritos for the Hungry Mathematician](https://edwardmorehouse.github.io/silliness/burrito_monads.pdf)

[^note1]: Be careful not to draw the reverse conclusion! There are a _lot_ of brilliant engineers who know absolutely nothing about functional programming: my argument is entirely about the relative difficulty of finding them in each community.