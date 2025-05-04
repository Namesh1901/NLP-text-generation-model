
# Shakespeare Chatbot

This project implements a Shakespeare-style chatbot using two different approaches: a **Markov Chain** model and a **GPT-based** model. It is designed to generate Shakespearean dialogue based on user input by leveraging both traditional and modern AI techniques.

## Installation

To set up the environment and install the required packages, run the following commands:

```bash
!pip install nltk
!pip install spacy
!pip install markovify
!pip install transformers
!pip install torch
!pip install tqdm
!pip install matplotlib
!pip install datasets
!python -m spacy download en_core_web_sm
```

These packages include the essential libraries for natural language processing, machine learning, and working with pre-trained transformer models.

## Data Preparation

The data is sourced from the **NLTK Gutenberg corpus**, which includes various works by Shakespeare. The code downloads the corpus and prepares it for text generation using both the Markov Chain model and the GPT model.

## Code Explanation

### 1. **Markov Chain Model**
   - The **Markov Chain** model is a statistical model that generates sequences based on the probabilities of transitions between elements (in this case, words).
   - The `markovify` library is used to create a model that generates Shakespearean text.
   - The text is cleaned and processed using regular expressions and NLTK's Gutenberg corpus.

```python
import markovify
import nltk
from nltk.corpus import gutenberg

# Load the Shakespearean texts
shakespeare_text = gutenberg.raw('shakespeare-hamlet.txt')

# Clean and preprocess text
text_model = markovify.Text(shakespeare_text)

# Generate Shakespearean-style text
generated_text = text_model.make_sentence()
```

### 2. **GPT-based Model**
   - The **GPT-based model** uses a pre-trained **GPT-2** model to generate text.
   - The `transformers` library from Hugging Face is used to load and fine-tune the model for text generation.
   - This approach produces more context-aware and human-like responses than the Markov model.

```python
from transformers import GPT2LMHeadModel, GPT2Tokenizer

# Load GPT-2 model and tokenizer
tokenizer = GPT2Tokenizer.from_pretrained("gpt2")
model = GPT2LMHeadModel.from_pretrained("gpt2")

# Tokenize input text
input_text = "To be or not to be"
inputs = tokenizer.encode(input_text, return_tensors="pt")

# Generate Shakespearean-style text
outputs = model.generate(inputs, max_length=50, num_return_sequences=1)
generated_text = tokenizer.decode(outputs[0], skip_special_tokens=True)
```

## Comparison of Outputs

### **Markov Chain Output**:
The Markov Chain model generates text based on the probability of word sequences. It often produces grammatically correct sentences, but lacks the ability to generate contextually rich and coherent conversations.

**Example:**
```
To be, or not to be, that is the question.
```

### **GPT Output**:
The GPT-based model, being a more sophisticated deep learning model, generates more contextually relevant and coherent responses. It can maintain better conversation flow and mimic the style of Shakespeare more closely.

**Example:**
```
To be, or not to be, that is the question. But the question itself is not what matters. What matters is what we choose to do with our lives.
```

### Key Differences:
- **Markov Chain**: Generates text based on word transition probabilities, which can lead to repetitive or non-sequitur responses.
- **GPT**: Generates more coherent and contextually rich responses, providing a better user experience, especially for longer conversations.

## Conclusion

This project demonstrates two approaches to creating a Shakespearean-style chatbot. While the **Markov Chain model** is simpler and faster, the **GPT-based model** provides more natural and contextually aware responses. Depending on your use case, you can choose either approach based on performance or quality requirements.

## Requirements

- Python 3.x
- Jupyter Notebook

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
