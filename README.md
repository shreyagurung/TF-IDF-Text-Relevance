# TF-IDF: Text Relevance

A small natural language processing project I built during my B.Tech in Information Technology to understand how computers can determine which words are more relevant within a collection of text.

This project explores TF-IDF, or Term Frequency-Inverse Document Frequency, through a small corpus of text about coffee, chocolate and cheese.

Rather than using a ready-made NLP library to produce the final result, I implemented the main TF-IDF calculation myself. The project also includes text preprocessing, stop-word removal and lemmatization.

This is an early learning project, and I am keeping it here as a record of an important stage in my technical learning.

## The question behind the project

When we read a document, some words tell us much more about its subject than others.

Words such as "the", "is", and "and" can appear across many documents and do little to distinguish one document from another.

A word that appears frequently in one document but rarely across the wider collection can be more informative.

I wanted to understand how this idea could be represented mathematically.

That is where TF-IDF comes in.

### Term Frequency

Term Frequency measures how frequently a term appears within a document.

### Inverse Document Frequency

Inverse Document Frequency measures how uncommon a term is across the collection of documents.

Together:

    TF-IDF = TF × IDF

A higher score indicates that a word is relatively more distinctive within a document or collection.

## The experiment

I created a small corpus containing six text documents across three categories:

    documents/
    │
    ├── Coffee/
    │   ├── general.txt
    │   └── starbucks.txt
    │
    ├── Chocolate/
    │   ├── dairymilk.txt
    │   └── galaxy.txt
    │
    └── cheese/
        ├── cottagecheese.txt
        └── general.txt

The corpus gave me a simple way to experiment with how the importance of a word changes depending on the other documents it is being compared against.

The central question was:

> If a word appears frequently in one document but is less common across the wider collection, does TF-IDF give it a higher score?

## From raw text to TF-IDF

The project follows a simple text-processing pipeline:

    Raw text
       ↓
    Read documents
       ↓
    Tokenise text
       ↓
    Remove stop words
       ↓
    Lemmatise words
       ↓
    Calculate Term Frequency
       ↓
    Calculate Inverse Document Frequency
       ↓
    Calculate TF-IDF
       ↓
    Sort and write scores

### 1. Reading the documents

The category-specific Python files read the text files belonging to each category.

- `coffee.py`
- `chocolate.py`
- `cheese.py`

They collect the text that is later processed by the TF-IDF functions.

### 2. Removing common words

The project uses NLTK to remove common English stop words.

For example:

    the
    is
    of
    and
    in

These words occur frequently but are generally not useful for distinguishing between the documents in this experiment.

### 3. Lemmatization

The project also uses WordNet lemmatization to reduce words to their base form.

This helps treat related forms of a word more consistently when analysing the text.

The preprocessing is handled through:

- `stemmingAndRemovingStopWordsClass.py`
- `stemmingAndRemovingStopWordsFullDocument.py`

Despite the filenames referring to "stemming", the code uses lemmatization through WordNet.

## Calculating TF-IDF

The main calculation is contained in `function.py`.

The code calculates the two components separately.

### Term Frequency

The implementation calculates how often a word occurs relative to the total number of words in a document.

    TF =
    number of times a term appears
    /
    total number of terms

### Inverse Document Frequency

The project then considers how many documents contain that word.

The implementation uses:

    math.log(len(lists) / (1 + n_doc(word, lists)))

The `1` added to the denominator prevents the calculation from dividing by zero when a word does not occur in any document.

### Final score

The two values are multiplied:

    TF-IDF = TF × IDF

The words are then sorted according to their calculated scores.

## Two ways of looking at the text

One part of this project calculates TF-IDF across individual documents.

Another part works with broader category-level text.

This allowed me to compare how word relevance changes depending on the collection of documents being considered.

It also helped me understand that TF-IDF is not simply a property of a word. Its score depends on the collection of documents against which it is being compared.

## Project files

| File | Purpose |
|---|---|
| `function.py` | Main TF-IDF calculation |
| `coffee.py` | Reads and works with the coffee documents |
| `chocolate.py` | Reads and works with the chocolate documents |
| `cheese.py` | Reads and works with the cheese documents |
| `stemmingAndRemovingStopWordsClass.py` | Preprocesses category-level text |
| `stemmingAndRemovingStopWordsFullDocument.py` | Preprocesses individual documents |
| `TFID.txt` | TF-IDF output |
| `TFID1.txt` | TF-IDF output from the other level of the experiment |
| `documents/` | Text corpus used for the experiment |

## What I was learning

This project helped me move from knowing the term "TF-IDF" to understanding what actually happens behind it.

I was learning:

- How raw text can be converted into data that a computer can analyse
- Why text needs to be preprocessed before analysis
- The difference between frequency and relevance
- Why common words become less useful for distinguishing documents
- How the wider document collection affects the importance of a word
- How mathematical formulas can be translated into working Python code
- How different stages of a text-processing pipeline fit together

The project was also an early exercise in working with Python libraries for natural language processing, including NLTK and TextBlob.

## What the project is not

This is not a search engine, recommendation system or production NLP application.

It is a small experimental implementation designed to understand the underlying idea behind TF-IDF.

The corpus is deliberately small and consists of a handful of manually collected text files.

That makes the project useful for learning, but not for drawing conclusions about large-scale text collections.

## Looking back

I built this project during my B.Tech in Information Technology at Christ University.

At the time, I was exploring different areas of computing and trying to understand what was happening underneath the tools and concepts I was learning.

This project is particularly useful to me in retrospect because it shows an early attempt to take a concept from machine learning and natural language processing and actually implement the underlying logic myself.

My work since then has moved in a different direction, towards GIS, disaster management, environmental research and sustainability.

I still want to keep these earlier technical projects around.

They are not representative of the work I do today, but they are part of how I got here.

## Technical stack

- Python
- NLTK
- TextBlob
- Natural Language Processing
- TF-IDF
- Text preprocessing
- Lemmatization

## Repository status

This is an undergraduate learning project.

The original code has been preserved rather than rewritten into a modern NLP implementation.

Some file paths and dependencies reflect the environment in which the project was originally developed, so the code may require adjustments to run on a modern machine.

The purpose of this repository is to document the original experiment and preserve the learning behind it.
