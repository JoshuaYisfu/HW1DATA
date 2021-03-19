# Large Scale Data Processing: Project 1 Report
Sean Chiang and Joshua Yi

## 1. **(4 points)** Run the program on your local machine to solve cases `k = 2,3,4,5,6`. For each `k`, provide `xS`, its hash value, the total time elapsed, and the number of trials.  

```
// k = 1
spark-submit --class project_1.main --master local[*] target/scala-2.12/project_1_2.12-1.0.jar this_is_a_bitcoin_block_of_34974696_and_22615604 1 20
==================================
found. count:1
(459401870this_is_a_bitcoin_block_of_34974696_and_22615604,043517ad05e2fbd95e7580c30b531717f0976b2de69f6766b7812675d41b0919)
Time elapsed:1s
==================================

xS          = 459401870this_is_a_bitcoin_block_of_34974696_and_22615604
hashValue   = 043517ad05e2fbd95e7580c30b531717f0976b2de69f6766b7812675d41b0919
timeElapsed = 1s
numTrials   = 20
```
```
// k = 2
spark-submit --class project_1.main --master local[*] target/scala-2.12/project_1_2.12-1.0.jar this_is_a_bitcoin_block_of_34974696_and_22615604 2 100
==================================
found. count:2
(1441097364this_is_a_bitcoin_block_of_34974696_and_22615604,007c0b4801d1677a695f05db9f2ae0f22e91b5d0bef2f3ec299cfabb65202fe8)
Time elapsed:1s
==================================

xS          = 1441097364this_is_a_bitcoin_block_of_34974696_and_22615604
hashValue   = 007c0b4801d1677a695f05db9f2ae0f22e91b5d0bef2f3ec299cfabb65202fe8
timeElapsed = 1s
numTrials   = 100
```
```
// k = 3
spark-submit --class project_1.main --master local[*] target/scala-2.12/project_1_2.12-1.0.jar this_is_a_bitcoin_block_of_34974696_and_22615604 3 500
==================================
found. count:2
(1766558624this_is_a_bitcoin_block_of_34974696_and_22615604,000300da4ba6700bdf299db22c5f02fcb3821918d65e03cfce3d9d8bd18922fc)
Time elapsed:1s
==================================

xS          = 1766558624this_is_a_bitcoin_block_of_34974696_and_22615604
hashValue   = 000300da4ba6700bdf299db22c5f02fcb3821918d65e03cfce3d9d8bd18922fc
timeElapsed = 1s
numTrials   = 500
```
```
// k = 4
spark-submit --class project_1.main --master local[*] target/scala-2.12/project_1_2.12-1.0.jar this_is_a_bitcoin_block_of_34974696_and_22615604 4 20000
==================================
found. count:1
(1982335496this_is_a_bitcoin_block_of_34974696_and_22615604,000053cf86cd141cc423ea4ce49b4506044c812f89da06665b1466b5fcb14430)
Time elapsed:1s
==================================

xS          = 1982335496this_is_a_bitcoin_block_of_34974696_and_22615604
hashValue   = 000053cf86cd141cc423ea4ce49b4506044c812f89da06665b1466b5fcb14430
timeElapsed = 1s
numTrials   = 20000
```
```
// k = 5
spark-submit --class project_1.main --master local[*] target/scala-2.12/project_1_2.12-1.0.jar this_is_a_bitcoin_block_of_34974696_and_22615604 5 500000
==================================
found. count:1
(800279104this_is_a_bitcoin_block_of_34974696_and_22615604,00000c5432065c50ff4220099d1df38fe1693fd75655407d1e38be5da96333b7)
Time elapsed:2s
==================================

xS          = 800279104this_is_a_bitcoin_block_of_34974696_and_22615604
hashValue   = 00000c5432065c50ff4220099d1df38fe1693fd75655407d1e38be5da96333b7
timeElapsed = 2s
numTrials   = 500000
```
```
// k = 6
spark-submit --class project_1.main --master local[*] target/scala-2.12/project_1_2.12-1.0.jar this_is_a_bitcoin_block_of_34974696_and_22615604 6 5000000
==================================
found. count:1
(2117178249this_is_a_bitcoin_block_of_34974696_and_22615604,00000067af8562e7c9697f45484be6b9f8e18f9f05442727f0fceb84161b72c2)
Time elapsed:3s
==================================

xS          = 2117178249this_is_a_bitcoin_block_of_34974696_and_22615604
hashValue   = 00000067af8562e7c9697f45484be6b9f8e18f9f05442727f0fceb84161b72c2
timeElapsed = 3s
numTrials   = 5000000
```

## 2. **(3 points)** Run the program on GCP to solve the case `k = 7`. Provide `xS`, its hash value, the total time elapsed, and the number of trials. Describe your cluster's configuration (number of machines, number/type of cores, etc.) and your process for estimating the number of trials needed in order to find the nonce.  

k=7
xS= 
hash value=
time elapsed=
Number of trials= 
Cluster's configurations= 2 machines, 48 cores and 96 threads since we are using a N-1 machine GCP

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