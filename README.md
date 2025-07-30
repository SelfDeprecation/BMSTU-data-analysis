# BMSTU-data-analysis

## Table of contents:
 - [Homework I](https://github.com/SelfDeprecation/BMSTU-data-analysis?tab=readme-ov-file#homework-i-description)
 - [Homework II](https://github.com/SelfDeprecation/BMSTU-data-analysis?tab=readme-ov-file#homework-ii-description)

# Homework I description

## Text Analysis Tool

**Main objective**: Create a text analysis tool that processes text entries (such as user reviews, articles, or book excerpts) and provides some insights, statistics, and transformations. Then, apply the text analysis tool according to your variant and draw conclusions about the nature of the text.

## Task 1: Data Collection and Preprocessing

Write a function `preprocess_text` that takes a text as input and cleans it. The function should:
   - Convert the text to lowercase.
   - Remove unnecessary punctuation and special characters but preserve sentence-ending punctuation marks (`.` `!` `?`).
   - Remove extra spaces between words.
   - Return the cleaned text.

**Example**:
```python
input_texts = [
    "Hello, World!\n   This is a test...",
    "Python is fun!!! #coding",
    "  Spaces should be    removed."
]

# Expected output:
# [
#     "hello world! this is a test.",
#     "python is fun! coding",
#     "spaces should be removed."
# ]
```

## Task 2: Word Frequency Analysis

Write a function `word_frequency` that takes cleaned text (from Task 1) and returns a dictionary where the keys are words and the values are their frequency in the text. The function should:
   - Count how often each word appears in the text.
   - Ignore any common stopwords. You can use the predefined list provided below or your own. Consider making it customizable.

**Predefined Stopwords**:
```python
stop_words = ["and", "the", "is", "in", "it", "you", "that", "to", "of", "a", "with", "for", "on", "this", "at", "by", "an"]
```

**Example**:
```python
input_text = "hello world this is a test. python is fun coding. spaces should be removed."

# Using predefined stopwords 

# Expected output:
# {
#     "hello": 1,
#     "world": 1,
#     "test": 1,
#     "python": 1,
#     "fun": 1,
#     "coding": 1,
#     "spaces": 1,
#     "removed": 1
# }
```

## Task 3: Information Extraction

Write a function `extract_information` that takes raw text (**not from Task 1**) and extracts specific types of information based on customizable regex patterns provided as keyword arguments. The function should return a dictionary where the keys are the match types, and the values are lists of found matches.

**Supported Information Types**:
1. Email addresses
2. Phone numbers
3. Dates
4. Times
5. Prices
6. Additional user-defined data

**Example**:
```python
input_text = "Contact me at john.doe@example.com or call +123 456 7890. Meeting on 10/05/2024 at 3:00 PM. The price is $19.99. Birthday on 15-08-2023."

# Custom patterns can be provided as needed.

# Expected output:
# {
#     "emails": ["john.doe@example.com"],
#     "phone_numbers": ["+123 456 7890"],
#     "dates": ["10/05/2024", "15-08-2023"],
#     "times": ["3:00 PM"],
#     "prices": ["$19.99"]
# }
```

## Task 4: Sentiment Analysis

Write a function `analyze_sentiment` that takes cleaned text (from Task 1) and analyzes its sentiment based on predefined positive and negative words. The function should return a sentiment score for the text.

**Predefined Word Lists**:
- **Positive words** (default):
```python
positive_words = ["good", "great", "happy", "joy", "excellent", "fantastic", "love", "best"]
```
- **Negative words** (default):
```python
negative_words = ["bad", "sad", "hate", "terrible", "awful", "poor", "worst"]
```

**Example**:
```python
example_texts = [
    "I love this product! It's fantastic and makes me very happy.",
    "This is the worst experience I've ever had.",
    "Great service but the food was bad."
]

example_results = {
    "I love this product! It's fantastic and makes me very happy.": 3,
    "This is the worst experience I've ever had.": -1,
    "Great service but the food was bad.": 0
}
```

## Task 5: Text Summarization

Write a function `summarize_text` that takes cleaned text (from Task 1) and summarizes it by extracting the most important sentences based on their relevance. The function should allow the user to specify a desired compression ratio as a parameter.

**Example**:
```python
input_text = (
    "I love this product! It's fantastic and makes me very happy. "
    "This is the worst experience I've ever had. "
    "Great service but the food was bad. "
    "The atmosphere was amazing, and the location is perfect."
)

# Assuming a compression ratio of 0.6
# Expected output (may vary based on ranking criteria):
# "I love this product! It's fantastic and makes me very happy. The atmosphere was amazing, and the location is perfect."
```

## Task 6: Word Frequency Visualization

Write a function `visualize_word_frequency` that takes a word frequency dictionary (obtained in Task 2) and visualizes the frequencies in a text-based format.

**Example**:
```python
word_frequencies = {
    "hello": 5,
    "world": 3,
    "python": 4,
    "coding": 2
}

# Expected output:
# hello:  *****
# python: ****
# world:  ***
# coding: **
```

Higher-Order Functions for Text Analysis
Write a function `apply_analysis` that takes a list of analysis functions and a single text entry. The function should apply each analysis function to the text entry and return a dictionary of results.


## Task 7: Higher-Order Functions for Text Analysis

Write a function `apply_analysis` that takes a list of analysis functions and a single text entry. The function should apply each analysis function to the text entry and return a dictionary of results.

**Example**:
```python
def word_frequency(text):
    # Implementation of word frequency analysis
    pass

def analyze_sentiment(text):
    # Implementation of sentiment analysis
    pass

input_text = "I love this product! It's fantastic and makes me very happy."

# Using the apply_analysis function
results = apply_analysis(input_text, [word_frequency, analyze_sentiment])

# Expected output might look like:
# {
#     "word_frequency": {"love": 1, "product": 1, "fantastic": 1, "happy": 1},
#     "sentiment": 3  # Assuming a sentiment score based on the defined method
# }
```

## Task 8: Wrap Everything in a Class

Create a class `TextAnalyzer` that encapsulates all the functionality from the previous tasks. The class should include methods for each of the following actions:

1. **Initialization**:
   - The class should take a single text upon initialization, store the original text, and automatically create its preprocessed version.

2. **Methods**:
   - `word_frequency`: Analyzes word frequency from the preprocessed text.
   - `extract_information`: Extracts emails, phone numbers, dates, times, and prices from the preprocessed text.
   - `analyze_sentiment`: Performs sentiment analysis on the preprocessed text.
   - `summarize_text`: Summarizes the preprocessed text based on a compression ratio.
   - `visualize_word_frequency`: Visualizes word frequency data in the text.
   - `apply_analysis`: Applies a list of analysis functions to the preprocessed text.

**Example**:
```python
class TextAnalyzer:
    def __init__(self, text: str):
        self.original_text = text
        self.cleaned_text = self.preprocess_text(text)

    def word_frequency(self) -> dict:
        # Implementation of word frequency analysis
        pass

    def extract_information(self, **patterns) -> dict:
        # Implementation of information extraction
        pass

    def analyze_sentiment(self, positive_words=None, negative_words=None) -> int:
        # Implementation of sentiment analysis
        pass

    def summarize_text(self, compression_ratio: float) -> str:
        # Implementation of text summarization
        pass

    def visualize_word_frequency(self) -> None:
        # Implementation of word frequency visualization
        pass

    def apply_analysis(self, analysis_functions: list) -> dict:
        # Implementation of applying analysis functions
        pass

# Sample usage
analyzer = TextAnalyzer("Some example text here.")
analyzer.visualize_word_frequency()
```

## Task 9: Text Analysis

Analyze the text assigned to you according to your variant. Use the developed tools to:

- Normalize the text
- Identify the most frequent words
- Assess the sentiment of the text
- Determine the key information in the text

Present your analysis results and draw conclusions about the content of the text.


# Homework II description

## Descriptive data analysis: Analysis of Worldwide Governance Indicators (WGI)

## Objective of the work:

To gain experience in solving practical data analysis tasks, such as data loading, transformation, calculation of basic statistics, and data visualization through graphs and charts, using the Python programming language.

The following indicator to be used is Control of Corruption (CC) and its metrics `rank` and `estimate`.

- Datasets:
    - [WGI](Homework%20II/data/wgidataset.xlsx)
    - [Regions](Homework%20II/data/regions.xlsx)
- [WGI Documentaton](http://info.worldbank.org/governance/wgi/)

## Stages of work:

1. Load data into a DataFrame and save it to `DF_WGI`. Then sort the data in descending order of the DataFrame index and save it to `DF_SORTED`.

2. Display WGI index data for 2022 as a horizontal bar chart (`rank`). An approximate example of the graph is shown below.

![](Homework%20II/img/cpi_2016_.png)

3. Create a DataFrame from the original data for the Europe and Central Asia region and save it to `DF_REGION`

4. Plot the WGI index for 1996-2022 for countries in the region Europe and Central Asia (`estimate`). An approximate example of the graph is shown below.

  ![](Homework%20II/img/fig_springfield_region.png)

5. Find countries with the highest and lowest WGI values in the Europe and Central Asia region for 2022 (`estimate`). Save these countries into a single DataFrame `DF_MINMAX` with corresponding labels.

    ⚠️ **Note.** Several countries may share the same ranking position due to identical index values.

6. Calculate the region's average values for each year from 1996 to 2022 (`estimate`) and store them in a Series `S_MEANS` containing only the mean values for each year.

7. Plot the WGI index from 1996 to 2022 for countries in the Europe and Central Asia region, highlight countries with the highest and lowest WGI values in 2022, and display the regional average along with Russia's values. An approximate example of the graph is shown below.

![](Homework%20II/img/fig_springfield_region_comb.png)

8. Calculate the change in the `rank` indicator value ($2022 - 1996$).

9. Display a table for the Europe and Central Asia region (WGI - `rank`) and save it to the `RES_TABLE`.

|             | Region | Country | Rank 1996 | Rank 2022 | Difference |
| ----------- | ------ | ------- | --------- | --------- | ---------- |
| mean_2022   | -      | -       | -         | -         | -          |
| max_2022    | -      | -       | -         | -         | -          |
| min_2022    | -      | -       | -         | -         | -          |
| Russia_2022 | -      | -       | -         | -         | -          |

**⚠️Note!** In the `Country` column, the row `mean_2022` must contain a hyphen `-`.

10. Display a `boxplot` of the WGI index for 2022 for all countries and for each region separately (on a single graph) (`estimate`).