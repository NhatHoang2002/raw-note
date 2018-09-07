---
layout: post
title: "Python 3"
categories: it
tags: [python, data]
maths: 1
toc: 1
comment: 1
---

This note continues the [first python note](/python-note-1). Check out the [full list of notes in python](/tags#python).

## Random walk

### Visualize the walk

The current walk depends on the previous one.

~~~ python
import numpy as np
np.random.seed(123)
random_walk = [0] # initial

for x in range(100): # 100 walks
	step = random_walk[-1] # take the last step
	dice = np.random.randint(1,7) # from 1 to 6

	if dice <= 2:
		step = max(0, step - 1) # prevent back to less than 0
	elif dice <= 5:
		step += 1
	else:
		step += np.random.randint(1,7)
	
	random_walk.append(step)

import matplotlib.pyplot as plt
plt.plot(random_walk)
plt.show()
~~~

### Distribution

- **Question**: random walk go up/down (of tails) but what is the chance to go up to 65, for example?
- **Idea**: run 100 times the algorithm of random walk to get the last "tails" and then see the distribution of this final tail and guest the chance. Using **histogram** to visualize the distribution.

