This repository is designed to replicate some of the results of the paper
"Comparing deep learning and concept extraction based methods for patient
phenotyping from clinical narratives"

The Jupyter Notebooks are intended to be run on Google Colab. Upload this to a
folder called "DLH project" on your Google Drive to run it. If the folder
was shared to you, you need to create a shortcut to the folder in order to run it.

preprocessing_for_cnn.ipynb contains code needed to create and save the documents
to be used as stacks of Word2Vec embedding vectors, as well as the labels
indicating if the patient described in each one has each condition (in a separate dataframe).
It requires NOTEEVENTS.csv (which can be obtained from the MIMIC-III dataset
on PhysioNet, after completing a training course and signing a usage agreement)
and annotations.csv (which can be found within the data folder of
https://github.com/sebastianGehrmann/phenotyping/, which is the GitHub repository
created by the original authors of this study)).

notebook_for_cnns.ipynb takes the outputs of preprocessing_for_cnn.ipynb and
uses them to train and test various CNNs designed to classify patients as having
or not having assorted conditions. The code within it is not yet complete.

Bag_of_words.ipynb contains code needed to train and test logistic regression
models which operate on bag-of-words representations of the documents and serve
as a baseline for the CNN. It requires NOTEEVENT.csv and annotations.csv within
the same folder as it in order to run.