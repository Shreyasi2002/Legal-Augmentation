<div id="top"></div>

<br />
<div align="center">

<h2 align="center">Legal Text Augmentation</h2>
<!-- <h3 align="center">Milestone 1</h3> -->

  <p align="center">
    Using data augmentation techniques to create new annotated legal text data by adding variations to existing data. Using deep learning models, such as neural networks, to analyze and classify the augmented data. By combining these techniques, improving the accuracy of legal text classification models and increase the amount of annotated legal text data available for use.
    <br />
    <br />
    <a href="https://github.com/Shreyasi2002/Legal-Augmentation">View Demo</a>
    ·
    <a href="https://github.com/Shreyasi2002/Legal-Augmentation/issues">Report Bug</a>
    ·
    <a href="https://github.com/Shreyasi2002/Legal-Augmentation/issues">Request Feature</a>
  </p>
</div>

<!-- TABLE OF CONTENTS -->
<details>
  <summary>Table of Contents</summary>
  <ol>
    <li>
      <a href="#problem-definition">Problem Definition</a>
      <ul>
        <li><a href="#corpus-description">Corpus Description</a></li>
      </ul>
    </li>
    <li>
      <a href="#proposed approach">Proposed Approach</a>
      <ul>
        <li><a href="#experiments-and-results">Experiments and Results</a></li>
        <li><a href="#future-directions">Future Direction</a></li>
      </ul>
    </li>
      </ol>
</details>


<!-- PROBLEM DEFINITION -->
## Problem Definition
The problem is to improve the performance of deep learning models on Indian legal text classification by augmenting the existing dataset. Specifically, the goal is to use various data augmentation techniques to increase the size and diversity of the dataset and improve the model's ability to handle semantically annotated legal documents with multiple rhetorical roles.

To solve this problem, we need to apply various data augmentation techniques such as back-translation, synonym replacement, sentence deletion, etc. to increase the size and diversity of the existing dataset. We also need to train and evaluate various deep learning models, such as recurrent neural networks (RNNs), and transformer models, on the augmented dataset to improve the performance on the legal text classification task. Additionally, we may need to fine-tune pre-trained language models, such as BERT or GPT-2, on the augmented dataset to further improve the performance. Overall, the problem requires a combination of data augmentation techniques, deep learning models, and evaluation metrics to achieve the desired performance on legal text classification.


<!-- CORPUS DESCRIPTION -->
## Corpus Description
The corpus/dataset that will be used is a set of 300+ legal documents with semantic annotations from the OpenNyAI GitHub repository (https://github.com/OpenNyAI/Opennyai) 

Each JSON file contains a list of data points, where each data point is represented by a dictionary with the following keys:
 - id: a unique identifier for the data point, which can be useful for evaluation purposes.
 - annotations: a list of dictionaries containing sentence-level annotations for the data point. Each data point is a dict with the following keys:
 - id: a unique identifier for the sentence.
 - value: a dictionary containing the following keys:
 - start: the starting index of the sentence in the text.
 - end: the end index of the sentence in the text.
 - text: the actual text of the sentence.
 - labels: a list of labels that correspond to the text of the sentence.
 - data: the actual text of the judgement.
 - meta: a string that provides metadata about the judgement, such as its category (e.g., Criminal, Tax, etc.).
 
<!-- PROPOSED APPROACH -->
## Proposed Approach
We propose the usage of 124M model of GPT-2 (https://github.com/minimaxir/gpt-2-simple), which is a lighter version of GPT-2, fine-tuned on our data set for effective generation of Legal Data annotated with rhetorical roles.
For this, the pipeline used is as follows :-
