# info7375-chatbot-rag-vector-db-metrics

### How to run

1. Open `evaluation.ipynb` file
2. Comment a block of code in the `Improve the llm by these...` section
3. Then click "Run all" button and wait until `evaluation.json` or `evaluation-improved.json` file is created

### Report and Video

[Report](./REPORT.pdf)
[Video]()

### Domain Selection:

Domain: A chatbot to help users understand MongoDB official website
Scope: Provide information about MongoDB and its affiliated products.

### Notes

Ensure you have the necessary API keys and access for Pinecone and OpenAI.
Modify the INDEX_NAME if you want to use a different index name in Pinecone.

```
PINECONE_API_KEY=
OPENAI_API_KEY=
```

#### Requirements

- Python 3.x
- python-dotenv
- langchain
- langchain-community
- langchain-openai
- langchain-pinecone
- Pinecone account and API key
- giskard
- rouge-score
- scikit-learn
- pydantic
- ipytest
- bs4
- ruff
