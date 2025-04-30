Parse Tree Model for Emotion Detection and Emoji Mapping
Introduction
In this project, we tackle the challenge of mapping text sentences to emojis based on emotional content. The goal is to predict one of the five distinct emotions represented by the emojis: 😊 (happy), 😔 (sad), 🤢 (disgust), 😨 (fear), and 😠 (anger), based on the input sentence. The emotional meaning of text is highly subjective, which adds complexity to emotion detection.

The solution leverages Natural Language Processing (NLP) techniques such as tokenization, Part-of-Speech (POS) tagging, syntactic parsing, and weighted lexicon matching. Specifically, we employ a parse tree to improve accuracy by analyzing the structure of the sentence, identifying important emotional phrases, handling negation more effectively, and scoring emotions based on the emotional weight of words.

Improved Method: Parse Tree and Weighted Lexicon Matching
The model is designed to understand the emotional intent of the sentence by considering the syntactic structure of the input text. It does so using Part-of-Speech (POS) tagging and Parse Trees, which break down the sentence into meaningful chunks based on grammatical roles.

Steps of the Improved Model
Tokenization and POS Tagging:

The input sentence is first tokenized (split into individual words).

Each token is tagged with its Part-of-Speech using NLP tools, identifying grammatical roles such as noun, verb, adjective, etc.

Parse Tree Construction:

A set of grammar rules is applied to chunk meaningful phrases (e.g., noun phrases, adjective phrases) using NLTK's RegexpParser.

These phrases include those that are likely to carry emotional weight, such as adjective phrases (AP) and verb phrases (VP).

Phrase-Based Emotion Scoring:

The model doesn't treat all words equally. Instead, it extracts only the emotionally meaningful phrases (e.g., “not happy”, “feel scared”) from the parse tree.

These emotionally significant phrases are checked against a manually defined emotion lexicon, which includes words associated with different emotions (e.g., "love" for 😊, "hate" for 🤢 or 😠).

POS Weighting for Word Importance:

Words that are more likely to convey emotions, such as adjectives and strong emotion verbs (e.g., "scared", "love", "hate"), are given higher weights.

Neutral words, such as articles or filler words (e.g., “the”, “is”), are assigned lower weights.

Scoped Negation Handling:

Negation is not applied to the entire sentence. Instead, it is handled within specific phrases (e.g., verb phrases or adjective phrases). If negation (e.g., “not”, “never”) appears within these emotional chunks, it inverts the emotional polarity.

Example: “I’m not happy” would be classified as 😔 (sad), while “I’m happy she’s not angry” would classify the first part as 😊 (happy) and the second part as 😔 (not angry).

Final Emoji Decision:

The model calculates a score for each emotion category (😊 😔 🤢 😨 😠) based on the weighted matches found in the sentence.

The emoji with the highest score is selected as the final output. If there is ambiguity or a tie, predefined rules can be applied to resolve the conflict.

Final Decision Making Process
The model uses the weighted scores from the identified phrases to assign an emoji based on the highest emotional score.

In case of ties or close scores, a tie-breaking rule can be used to ensure a final decision.

Module Description
This model is a rule-based emotion detection system designed to map text sentences to one of five emojis based on emotional content. The steps include:

Text Preprocessing: Tokenizing, lowercasing, and removing punctuation.

Phrase Extraction: Identifying emotionally relevant phrases using parse trees.

Emotion Scoring: Applying weights to the emotional relevance of words and handling negation.

Final Prediction: Selecting the emoji with the highest emotional score.

Modules Used
nltk (Natural Language Toolkit):

word_tokenize: Breaks the sentence into individual tokens.

pos_tag: Tags each word with its grammatical role.

RegexpParser: Builds a parse tree based on custom grammatical rules.

Tree: Represents the parsed sentence in a structured format.

collections:

defaultdict: Used to initialize and build up emotion scores during processing.

string:

punctuation: For cleaning the input text by removing punctuation.

Data Selection and Preprocessing
Dataset Construction:

A small dataset of 10 sentences is manually constructed to represent a mix of emotions, sarcasm, negation, and emotional phrase chunks.

Preprocessing:

The sentences are preprocessed by lowercasing, removing punctuation, and tokenizing using nltk.word_tokenize.

Phrase Extraction:

Emotionally significant phrases (e.g., “very happy”, “not sad”) are extracted using POS tagging and RegexpParser.

Emotion Lexicon and Weighting:

A lexicon with weighted emotion terms is used to score sentences.

Negation Handling:

Scoped negation is applied only to the relevant emotional phrases.

README
Emotion Detection and Emoji Mapping
This project uses Natural Language Processing (NLP) techniques to map sentences to emojis based on their emotional content. The model works by analyzing the sentence structure, extracting meaningful emotional phrases, and scoring emotions based on their relevance and intensity.

Features:
Tokenizes sentences and analyzes their emotional content.

Uses Part-of-Speech (POS) tagging and Parse Trees to identify emotionally relevant phrases.

Handles negation and sarcasm to improve accuracy.

Maps the emotional content to one of five emojis: 😊 (happy), 😔 (sad), 🤢 (disgust), 😨 (fear), and 😠 (anger).

Requirements:
Python 3.x

NLTK (Natural Language Toolkit)

Installation:
Clone the repository or download the project files.

Install NLTK:

bash
Copy
Edit
pip install nltk
Usage:
Import the necessary modules:

python
Copy
Edit
from nltk.tokenize import word_tokenize
from nltk import pos_tag
from nltk.parse import RegexpParser
Use the process_sentence function to get the predicted emoji for a sentence:

python
Copy
Edit
emoji = process_sentence("I'm so happy today!")
print(emoji)
Contributions:
Feel free to contribute by submitting issues, suggestions, or pull requests!
