# Module_01
## Writing about random numbers 

This module introduces the difficult process of writing about random
numbers. We will use some introductory Monte Carlo simulations to:

2. **Discuss Uncertainty in Design:**
    - Perform statistical analysis of simulation data to extract meaningful insights
    - Present clear and concise statistical findings 
    - Distinguish between qualitative (social) and quantitative
      (engineering) uncertainty in technical documents
    - Illustrate the importance of social uncertainty in engineering
      design
3. **Monte Carlo Simulation:**
    - Create Monte Carlo simulations using software tools (e.g., Python, R) to analyze complex systems and scenarios
    - Interpret and communicate the results of Monte Carlo simulations
    - Explain the principles and applications of Monte Carlo simulation in data-driven decision-making
    - Develop probabilistic models for real-world scenarios
4. **Create Visualizations of Data:**
    - Generate effective and informative visual representations of engineering data using appropriate tools (e.g., Excel, Python, or MATLAB)
    - Select suitable visualizations  for different data sets and e.g. plots, bar charts, scatter
     plots, histograms, contour plots,


The core of Monte
Carlo methods depends upon good [pseudo-random number
generators](https://en.wikipedia.org/wiki/Pseudorandom_number_generator).
There are two opposing philosophical theories that:

1. randomness is impossible
2. the universe is random


## "Randomness" in a Newtonian world

In Classical Newtonian physics, every action has an equal and opposite
reaction. Each effect is created by some cause. 

"We may regard the present state of the universe as the effect of its
past and the cause of its future. An intellect which at a certain moment
would know all forces that set nature in motion, and all positions of
all items of which nature is composed, if this intellect were also vast
enough to submit these data to analysis, it would embrace in a single
formula the movements of the greatest bodies of the universe and those
of the tiniest atom; for such an intellect nothing would be uncertain
and the future just like the past could be present before its eyes."

-Pierre Simon Laplace, _A Philosophical Essay on Probabilities_[1]

Laplace makes the point that in any system governed by known physics, we
can predict future outcomes based upon initial conditions. In Laplace's
world, it seems like everything is predictable and well-behaved. This is
true, until you consider chaotic systems and things like the Butterfly
effect. 

A Chaotic system is different from a random system, because a choatic
system follows predetermined rules, but small changes in initial
conditions lead to large changes in final outcomes. The results can look
random, but there is no randomness in the laws or predictions. For
example the double pendulum follows specific physical laws, but
seemingly small changes lead to large final outcomes. 

![Double pendulum simulation that demonstrating 100 double pendulums
that begin to swing in unison, but as time progresses they begin
diverging into chaotic
motion](https://cooperrc.github.io/_images/100-pendulums.gif)


Modern physics involves the wave-particle duality of subatomic
particles, but this is still a set of deterministic physical laws that
make predictions about how the world works. The uncertainty principle
limits how accruately you can "know" position and momentum, but this
uncertainty is much smaller than almost all phenomena you can experience
e.g. uncertainty in electron positions might stretch to $\approx100~nm$. 

"I, at any rate, am convinced that [God] does not throw dice" 
-Albert Einstein [Letter to Max Borne]

Einstein disagreed with the idea that even Quantum Mechanics can
consider these theories as "random". Quantum Mechanical interpretations
of wave functions depend upon many-world theories and superposition, but
they are inherently deterministic. Always connecting events through
known interactions even when cause-effect relationships seem to invert.

## Randomness in a random world

Most scientific theories are grounded in an underlying dogmatism that
each effect is the result of some cause. Testing and validating
scientific theories is done by isolating causes and measuring effects.
In spite of these continued advances, there seems to be unexplained and seemingly random
phenomenon. Nihilism, Existentialism, and Absurdism try to make sense of a
world that seems random, chaotic, and meaningless. These philosophical
theories point to chaos and chance encounters and try to make sense of
the world in its random state. 

## Random number generators

Whether you consider the world to be ruled by cause and effect and
chaotic or completely random. It is not easy to create _truly_ random
numbers. _Truly random_ numbers need to be uniformly distributed e.g.
the chance of 0 is the same as the chance of 0.789 _and_ unpredictable.
Cryptocurrency, cryptography, and NFTs rely almost entirely on the
creation of _truly_ random numbers. 
In this course we will use the [NumPy
`default_rng`](https://numpy.org/doc/stable/reference/random/generator.html)
to create numbers that are pseudo random. We can't use them to generate
cryptographic keys, but they are great for understanding uncertainty in
physical systems. 



## References 
**1.** Laplace, Pierre Simon, A Philosophical Essay on Probabilities,
translated into English from the original French 6th ed. by Truscott,
F.W. and Emory, F.L., Dover Publications (New York, 1951) p.4.
**2.**
[Barker, E. and Kelsey, J. Recommendation for Random Number Generation Using Deterministic Random
Bit Generators, NIST Spec. Pub. 800-90A
](https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-90Ar1.pdf)
