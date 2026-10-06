# Interpreting-Self-Debiasing-Methods-Research

These files include various python files from my research on the BBQ Bias benchmark and various self debiasing methods used to reduce the bias on that benchmark. I first took the bias benchmark-- BBQ from https://arxiv.org/pdf/2110.08193. BBQ has multiple choice questions of 3 including one stereotype-aligned, one against the stereotype, and an unknown answer for 9 stereotype categories (read more in the paper). I tested Gemma 2.0 on the benchmark in BBQExperimentReplication--BaselineBias.ipynb. I then replicated https://arxiv.org/pdf/2402.01981 with Gemma 2.0 and tested their two methods: explanation prompting (asking the model to explain its answer and then asking the question) and reprompting (asking the model if it is certain on its answer) on the BBQ benchmark in BBQ-SelfDebiasing-ExplanationPromptingBBQResults.ipynb and BBQ-SelfDebiasing-RepromptingBBQResults.ipynb. I then used a classifier probe to investigate whether a probe trained on baseline results could work for the 2 self-debiasing methods. I used the classifier probe for two distinctions- whether the model answered an unknown or known answer on the BBQ questions and further within the known answers whether the model answered a stereotype-aligned answer. The unknownVSknown probes are stored in BaselineActivationProbeUnknownVSKnown.ipynb, ActivationProbe-Explanation-UnknownVSKnown.ipynb, and ActivationProbe-Reprompting-UnknownVSKnown.ipynb. The stereotyped VS non-stereotyped probes are stored in BaselineActivationProbe-StereotypedVSNon.ipynb and ActivationProbe-Explanation-StereotypedVSNon.ipynb. Note that there is no reprompting notebook, as there is a sample size of 3 known answers to separate into stereotyped and non-stereotyped, which is useless.

# BBQ Results
<img width="1888" height="678" alt="image" src="https://github.com/user-attachments/assets/44c16df6-67cf-4caf-ba8b-dbce32cdb632" />

Here are the results for the BBQ experiment. Note that we including disambiguous questions, where the answer is included in the prompt. This resulted in a notable find that reprompted models tend to doubt their answers and answer unknown to many questions where the answer is stated in the prompt. Some more detailed results:

<img width="913" height="319" alt="image" src="https://github.com/user-attachments/assets/2d0d7570-c518-48f1-ab84-ceb19b8023d8" />

<img width="1790" height="590" alt="image" src="https://github.com/user-attachments/assets/9c0ad3a5-53df-4d23-b994-d4c7f1f04ee4" />

<img width="1702" height="584" alt="image" src="https://github.com/user-attachments/assets/0b61928b-935c-4c35-b535-7d870b008232" />

# Probe Results

Using the classifier probe trained on the baseline to test on the self-debiased models found these results (IMPORTANT: ONLY RAN ON AGE CATEGORY:

<img width="1702" height="584" alt="image" src="https://github.com/user-attachments/assets/ce6b56d2-d284-4d93-adf6-c669af013356" />

# Jacobian Lens

I also hand inputted over 50 prompts from the BBQ testing into neuronpedia to see how biased the Gemma model was in the Jacobian lens. The Jacobian lens attempts to look at the inner activations of the model and see what it is 'thinking. Hand grading the responses and what was activated in the lens (maybe not the most efficient way to do this) found these results:

<img width="1798" height="696" alt="image" src="https://github.com/user-attachments/assets/61ece678-985a-49e3-b82c-c67f6ba07920" />

What was especially interesting was the model tending to be very willing to discriminate with stereotypical names like here:

<img width="1798" height="696" alt="image" src="https://github.com/user-attachments/assets/eb0d9a22-3ef2-4b43-80cc-bec794fa23c6" />

The Gemma model answered Omar, and there are many other cases of this name based discrimination happening, which is quite interesting. The Jacobian lens also overall showed many more slight clues of the model at least being aware of the stereotype and thinking about it more, if not answering with the stereotyped response as well. Any bias by a widely used model has much wider dangers, as millions of people use chatbots everyday, and eventually pick up their habits and eventually stereotypes. Having one of the most widely used open-source models be racist needs to be fixed.

For more in depth results for any of this contact me at alecklen11@gmail.com, or run the code.
