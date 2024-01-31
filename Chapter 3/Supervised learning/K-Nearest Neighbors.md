The initialization for this classification technique consists in:
- Define K
- Define a [[Distance]] metric
- Consider a set of labeled training samples
Then, after initializing and given a test sample we proceed as follows:
1) compute the distance between the test sample and all the training samples
2) Retain the top K training samples sorted based on the distance from the test (we call these K elements the K nearest neighbors)
3) Each neighbor "votes" for its label: assign to the test sample the label with more votes
This method is not parametric meaning that fitting of sample population to any parametrized distributions is not required, but it's time consuming since the distances must be re-computed for each test sample.
