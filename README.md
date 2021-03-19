# Large Scale Data Processing: Project 1 Report
Sean Chiang and Joshua Yi

## 1. **(4 points)** Run the program on your local machine to solve cases `k = 2,3,4,5,6`. For each `k`, provide `xS`, its hash value, the total time elapsed, and the number of trials.  

```
// k = 1

xS          = 793641660this_is_a_bitcoin_block_of_34974696_and_22615604
hashValue   = 0d3068f6c9d251efd27c65bb3f431462d5189199243554e7f827a4a752c51bd2
timeElapsed = 1s
numTrials   = 1
```
```
// k = 2

xS          = 921400433this_is_a_bitcoin_block_of_34974696_and_22615604
hashValue   = 00e5bf2be4512d69d04ccac0970e622e00dae60a292017f1f347c08dde43e80c
timeElapsed = 1s
numTrials   = 85
```
```
// k = 3

xS          = 1935801145this_is_a_bitcoin_block_of_34974696_and_22615604
hashValue   = 000ff59c44a1aeeecd7a83bc8bcf775da7c3b0f54d3126f13cebba9a775cea9c
timeElapsed = 1s
numTrials   = 340
```
```
// k = 4

xS          = 1292877562this_is_a_bitcoin_block_of_34974696_and_22615604
hashValue   = 00002346784365707d54d2ca2a41018fb97a8e4114e202e7b170ada947d152c2
timeElapsed = 1s
numTrials   = 2186
```
```
// k = 5

xS          = 2076686935this_is_a_bitcoin_block_of_34974696_and_22615604
hashValue   = 0000048ab821dff36fdf761ccad3c7ac58431abf11240ed8ffe40527b255b9a5
timeElapsed = 1s
numTrials   = 24384
```
```
// k = 6

xS          = 1971864184this_is_a_bitcoin_block_of_34974696_and_22615604
hashValue   = 0000004a8acc5c382e21f367b53d403679fbddd715edf05c0ae61bad3f220b37
timeElapsed = 3s
numTrials   = 228474
```

## 2. **(3 points)** Run the program on GCP to solve the case `k = 7`. Provide `xS`, its hash value, the total time elapsed, and the number of trials. Describe your cluster's configuration (number of machines, number/type of cores, etc.) and your process for estimating the number of trials needed in order to find the nonce.  

```
// k = 7
xS          = 
hashValue   =
timeElapsed =
numTrials   = 

Clusters' configuration
  - 2 machines
  - 48 cores and 96 threads since we are using a N-1 machine GCP
```

## 3. **(3 points)** Modify **one** line of code in **src/main/scala/project_1/main.scala** so that the program generates the potential nonce from 1 to `n` (the number of trials) instead of randomly. Discuss whether or not this is more efficient than the randomized approach.

```
change
iter.map(x => rand.nextInt(Int.MaxValue - 1) + 1)

into
iter.map(x => rand.nextInt(trials - 1) + 1)
```

This modification is likely not more efficient because of the limitation of the possible hashes. The only thing that generating possible nonces from 1 to 'n' does is limit our possible answer.
If there is no nonce that hashes to satisfy the difficulty set under our number of trials, then no matter how many times we run that trial we will never find a solution.
On the other hand, using a random nonce from 1 to 2^32 has a chance that it might find a nonce that fulfills our difficulty no matter the number of trials, yet it is still very low.

The distribution of hash values evens out as the number of trials grows larger in our modified code, but the distribution of hashes is already even if we choose a random nonce from 1 to 2^32
regardless of how many trials we run. As such, it is not more efficient to limit our potention nonces to the number of trials instead of selecting randomly.


## Submission via GitHub
Delete your project's current **README.md** file (the one you're reading right now) and include your report as a new **README.md** file in the project root directory. Have no fear—the README with the project description is always available for reading in the template repository you created your repository from. For more information on READMEs, feel free to visit [this page](https://docs.github.com/en/github/creating-cloning-and-archiving-repositories/about-readmes) in the GitHub Docs. You'll be writing in [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown). Be sure that your repository is up to date and you have pushed all changes you've made to the project's code. When you're ready to submit, simply provide the link to your repository in the Canvas assignment's submission.

## You must do the following to receive full credit
1. Create your report in the ``README.md`` and push it to your repo
2. In the report you must include your full name and your partner's full name, in addition to collaborators
3. Submit a link to your repo on the canvas assignment

## Late Submission Penalties
Beginning with the minute after the deadline, your submission will be docked a full letter grade (10%) for every 
day that it is late. For example, if the assignment is due at 11:59 PM EST on Friday and you submit at 3:00 AM EST on Sunday,
then you will be docked 20% and the max you could receive on that assignment is an 80%. 
Late penalties are calculated from the last commit in the git log.
**If you make a commit 48 hours after the deadline, you will receive a 0 -- Please do not do this, it messes up our grading.**