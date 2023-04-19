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
  - **Input** :- Here, no input is needed as the model will just generate random data.
  - **Output** :- The model would generate a json file containing the labels and their corresponding text.

The model architecture is shown below -
<img src="https://github.com/Shreyasi2002/Legal-Augmentation/blob/main/pictures/architecture.png"/>


<!-- EXPERIMENTS AND RESULTS -->
## Experiments and Results
There were several models tested, the details of which are as follows :-

### GPT-2 Unsupervised Text Generation
In this  case, GPT-2 124M pre-trained model was finetuned using the dataset to generate data in xml format which is then converted to the required JSON format. This model was trained for 2000 steps with a learning rate of 0.0001 with a cross entropy loss of 1.36 on the dev dataset. Then, it was trained for 2000 more steps with a learning rate of 0.00001 with a cross entropy loss of 0.64. While training this model, top-k sampling was used with k being 40.
For this, the pipeline used is as follows :-
<img src="https://github.com/Shreyasi2002/Legal-Augmentation/blob/main/pictures/pipeline.png"/>

### Sentence-by-Sentence generation using GPT2
In the context of GPT2, sentence-by-sentence generation is achieved by splitting the input text into individual sentences, and generating each sentence separately. This allows for greater control over the output, as the model can be fine-tuned to generate text that adheres to a specific style, tone, or topic. By preserving the labels for each fragment of text, the resulting document is more organized and easier to read.

```
Original Text: 
It is claimed that the accused had looked after Lakshmi well till the birth of their first child, which was a girl and he was not happy with the girl child and thereafter started ill-treating Lakshmi, apart from which, he was also demanding dowry and on that pretext, he used to assault her continuously.

Synthetic Text: 
It is claimed that the accused had looked after Lakshmi well till the birth of their first child, which was a girl and he was not happy with the girl child and thereafter started ill-treating Lakshmi, apart from which, he was also demanding dowry and on that pretext, he used to assault her continuously.
According to the police, Lakshmi was admitted to a private hospital for treatment of her injuries after which she succumbed to her injuries. Lakshmi's mother has filed a complaint against the accused.
```

### Random Insertion using BERT
Random insertion using BERT is a technique that involves randomly inserting [MASK] tokens into a sentence with a certain probability, and then using BERT to fill in the masked tokens to predict the word. This approach can be used to generate synthetic text that is similar to the original text, but with some variations or additions.
```
Original Text: 
In this regard, it is the complainant's case that Laxmi had repeatedly told her about the ill-treatment.

Masked Text: 
In this [MASK] regard, it is the [MASK] complainant's case [MASK] that [MASK] Laxmi [MASK] had repeatedly [MASK] told [MASK] her about the [MASK] ill-treatment.

Synthetic Text: 
in this this regard, it is the the complainant ' s case case that that laxmimi had repeatedly repeatedly told told her about the the ill - treatment.
```

### T5 model for augmentation and summarization
The T5 model is a powerful language model that can be used for various tasks, such as summarization and translation. To experiment with the T5-base model, different task prefixes were implemented to perform different tasks.
<img src="https://github.com/Shreyasi2002/Legal-Augmentation/blob/main/pictures/T5_arch.png"/>
```
Original Text: 
It is claimed that the accused had looked after Lakshmi well till the birth of their first child, which was a girl and he was not happy with the girl child and thereafter started ill-treating Lakshmi, apart from which, he was also demanding dowry and on that pretext, he used to assault her continuously.

Output Text: 
Lakshmi's father allegedly started ill-treating her and demanding dowry. on that pretext, he used to assault her continuously.
```

### Back Translation
Another task implemented using the T5-base model was back-translation, which involves translating the original English text to French using Google's T5 model and then translating the resulting French text back to English using the Helsinki NLP model. The output text shows that the T5 model can effectively translate the original text to French and back to English, while preserving the meaning of the text.
```
Original Text: 
It is claimed that the accused had looked after Lakshmi well till the birth of their first child, which was a girl and he was not happy with the girl child and thereafter started ill-treating Lakshmi, apart from which, he was also demanding dowry and on that pretext, he used to assault her continuously.

First Translation: 
Il est affirmé que l'accusé s'était bien occupé de Lakshmi jusqu'à la naissance de leur premier enfant, qui était une fille, et qu'il n'était pas satisfait de la fille en question, en commençant par la suite à la maltraiter, hormis cela, il exigeait également la dot; sous ce

Output Text: 
It is claimed that the accused had properly cared for Lakshmi until the birth of their first child, who was a daughter, and that he was not satisfied with the girl in question, beginning subsequently to mistreat her, except for that, he also demanded dowry; under this
```

### Controlled generation using Template
The process begins by creating a template that includes placeholders such as "[ADJECTIVE]", "[NOUN]", "[VERB]", and "[ADVERB]", along with associated lists of words to serve as substitutions for these placeholders. Next, text is generated by randomly selecting words from the provided lists to fill in the placeholders. This resulting text is then fed into the GPT-2 model, which generates additional text based on the input. The final outcome is a combination of the template and the randomly chosen words, merged together.
```
Template: The [ADJECTIVE] [NOUN] [VERB] [ADVERB] in the [ADJECTIVE] [NOUN].
 
Filled template: The lazy sun cried slowly in the lazy sun

Generated text: The lazy sun cried slowly in the lazy sun The sun was falling softly, and was no more restless nor restless for fear of the dark A man could have a dream of his youth as young As. A dream of great love is such a dream that it's the same as a dream of a man himself.
```


## Future Directions
 - In the GPT-2 unsupervised text generation, it is possible to give it some input like names of lawyers, court, or even type of case like civil, criminal, etc., so that the generated data is not completely random. The model can be modified further to limit hallucination.
 - The augmentation of legal text is frequently centred on documents written in the English language. However, there exists a necessity for the development of legal text augmentation methodologies that are capable of operating with documents composed in various other languages. The implementation of techniques for augmenting legal text in multiple languages has the potential to enhance comprehension of legal documents in countries where languages other than English are spoken, as well as to streamline legal analysis across international borders.
 - Legal documents encompass various domains, including but not limited to corporate law, intellectual property law, and environmental law, necessitating domain-specific legal text augmentation. The refinement of domain-specific legal text augmentation techniques that are customised to the unique language and structure of individual domains may enhance the precision and pertinence of the produced text.
 - The augmentation of legal text through human-in-the-loop methodology is imperative. Although machine learning models have the capability to produce synthetic text that bears resemblance to pre-existing legal documents, they may not consistently encompass the subtleties and contextual intricacies of legal language. The integration of human experts in the process of generating and validating synthetic text through human-in-the-loop legal text augmentation techniques may serve as a means of guaranteeing the accuracy, relevance, and reliability of the generated text.
 - The increasing sophistication of legal text augmentation techniques necessitates the establishment of standardised evaluation metrics to assess the quality and utility of the generated text. The proposition of devising assessment criteria that consider variables such as precision, comprehensibility, and pertinence may facilitate the comparison and assessment of distinct legal text augmentation methodologies by scholars and professionals.
