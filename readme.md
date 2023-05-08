This repository is designed to replicate some of the results of the paper
"Comparing deep learning and concept extraction based methods for patient
phenotyping from clinical narratives"

The Jupyter Notebooks are intended to be run on Google Colab. Upload this to a
folder called "DLH project" on your Google Drive to run it. If the folder
was shared to you (and not directly uploaded by you), you need to create a
shortcut to the folder in order to run it.

We do not have a requirements.txt, because this code is to be run on Google Colab,
and I do not think you use that there. The libraries needed should be available there.
We used the Gensim (4.3.1), Matplotlib (3.7.1), NumPy (1.22.4), os, pandas (1.5.3),
PrettyTable (0.7.2), PyTorch (2.0.0+cu118), re (2.2.1), scikit-learn (1.2.2), sys,
and time libraries in our code. Our version of Python was 3.10.11.

We used Jupyter Notebooks for this, as they are much more convenient to work with
than regular .py files. You can run a code block and see what happens,
then write more code or modify the code block based on the results,
try running a code block multiple times and printing different things,
and so on. Also, Jeremy's computer only has 128 MB of GPU RAM, so it would be
impossibe for him to train our models in a reasonable timeframe locally
(although each of our models trains quickly, we had 60 models, so using
GPU acceleration was vital).

preprocessing_for_cnn.ipynb contains code needed to create and save the documents
to be used in the study as stacks of Word2Vec embedding vectors, as well as the labels
indicating if the patient described in each one has each condition (in a separate dataframe).
It requires NOTEEVENTS.csv (which can be obtained from the MIMIC-III dataset
on PhysioNet, after completing a training course and signing a usage agreement)
and annotations.csv (which can be found within the data folder of
https://github.com/sebastianGehrmann/phenotyping/, which is the GitHub repository
created by the original authors of this study).
More information is present in the notebook itself.
We included "word_vectors_from_all_discharge_summaries.wordvectors", so you will
not actually have to run Word2Vec, but you still need to perform various other
preprocessing tasks done in preprocessing_for_cnn.ipynb.
We ran preprocessing_for_cnn.ipynb on a Google Colab session with high RAM and no GPU
acceleration (because gensim does not use the GPU).

notebook_for_cnns.ipynb takes the outputs of preprocessing_for_cnn.ipynb and
uses them to train and test various CNNs designed to classify patients as having
or not having assorted conditions.
It creates 6 different CNNs which take into consideration different combinations of
n-grams for each of the 10 conditions under investigation.
It both prints its results and saves them to a JSON file.
It also contains code to perform our two ablations.
We ran preprocessing_for_cnn.ipynb on a Google Colab session with normal RAM and standard GPU
acceleration.

Bag_of_words.ipynb contains code needed to train and test logistic regression
models which operate on bag-of-words representations of the documents and serve
as a baseline for the CNN. It requires NOTEEVENT.csv and annotations.csv within
the same folder as it in order to run. N-grams_bag_of_words.ipynb does the same,
but for n-gram based logistics regression baselines.
We ran these on a Google Colab session with normal RAM and no GPU
acceleration.

Display Notebook.ipynb contains information needed about our replication study as a whole,
discussion about our results, and many visualizations. It requires the JSONs created by
notebook_for_cnns.ipynb to run (which we included in the repository). It can be considered
our submission for the Notebook Bonus.

Presentation.pptx contains the slides used for our presentation.

"sped-up presentation video.mp4" is our presentation video.

"CS 598 DLH Project Final Report.pdf" is our final report. 

We will not include any pre-trained weights, as we have 60 different CNNs just for our
base experiment. You would not be able to use those weights without downloading the data
we used and preprocessing it in preprocessing_for_cnn.ipynb, as we cannot include the data
used due to privacy concerns. You can train and test any model you are curious about using
train_test_model() in notebook_for_cnns.ipynb, anyways (which takes between 10 seconds
for the smallest models and about 2 minutes for the largest, on a Google Colab platform
with normal RAM and standard GPU acceleration).

If anything is missing or you have any questions, feel free to reach out to
jbao8@illinois.edu.
