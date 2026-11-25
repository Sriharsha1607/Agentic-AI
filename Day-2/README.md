## TASK-2: Groq Chatbot

Install the required Python package in Google Colab:

```python
!pip install -q openai
```

## API Key Setup

1. Open the **Secrets** section in Google Colab.
2. Add a secret named `GROQ_API_KEY`.
3. Enable notebook access to this secret.

## Usage

Run the notebook cells in order. The chatbot uses Groq's API to answer customer questions about Sweet Crumbs Home Bakery, including menu prices, eggless options and ordering details.

Start the interactive chat by running the final cell. Enter your questions at the `You:` prompt and type `bye`, `exit` or `quit` to end the conversation.

Example:

```text
You: Do you have eggless cup cakes?

Bot: Yes! We offer eggless versions of all our cakes,
including cup cakes. Let me know if you'd like to order!
```

The chatbot is instructed to respond in English or Telugu, depending on the customer's language, and to keep its responses short and friendly.

The notebook also includes examples of Python dictionaries, JSON, functions, decorators and basic error handling, along with a function to calculate menu prices based on quantity.
