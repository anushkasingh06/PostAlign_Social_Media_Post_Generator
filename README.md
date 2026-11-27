# PostAlign - AI-Driven Social Media Post Generator

## Introduction

PostAlign is a Streamlit application for generating LinkedIn-style posts from a selected topic. A user can choose a topic from the available trending headlines, enter a topic manually, or select one of the tags extracted from example posts. The generated text can be tailored by length, language, and tone.

The generation flow uses a language model through Groq and LangChain, while a small collection of example posts helps guide the style of the output.

## Overview

The application is organized into separate modules. `main.py` provides the Streamlit interface and collects the user's selections. `post_generator.py` builds a prompt using the requested topic, length, language, and tone, then sends it to the configured language model.

The `FewShotPosts` class reads the processed post data and filters examples by tag, language, length, and tone. These examples are added to the prompt so the model has relevant writing samples to follow.

The preprocessing module enriches raw post text with metadata such as line count, language, tags, and tone. It uses the language model to extract the metadata and to map similar tags to a smaller, more consistent set. Trending headlines are retrieved separately through NewsAPI.

## Main Functionality

- Choose a topic from current headlines, enter a custom topic, or select a prepared tag.
- Generate short, medium, or long posts.
- Select from the supported language options in the interface.
- Choose a professional, casual, humorous, inspirational, or neutral tone.
- Use filtered example posts as few-shot prompt context.
- View trending headlines in the Streamlit sidebar.

## Implementation

- **Language:** Python
- **Interface:** Streamlit
- **Language model integration:** Groq, LangChain
- **Model configured in code:** Llama 3.1 8B Instant
- **Data processing:** Pandas, JSON
- **Headline retrieval:** NewsAPI
- **Configuration:** Environment variables loaded through `python-dotenv`

## Running the Application

Install the packages listed in `requirements.txt`, configure the required API keys in a local environment file, and start the interface:

```bash
pip install -r requirements.txt
streamlit run main.py
```

The application expects the processed post data at `data/processed_posts.json`. The preprocessing script can be run to create that file from the raw post data, provided the input file and API configuration are available.

## Notes

Generated posts depend on the language model response, prompt examples, and the quality of the selected topic. Review and edit generated content before publishing it.
