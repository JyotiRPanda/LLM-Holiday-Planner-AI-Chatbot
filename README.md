# LLM-Holiday-Planner-AI-Chatbot

A chatbot designed to answer users' travel queries and recommend holiday packages based on a dataset using OpenAI APIs (LLM).

## TravelAssistAI

### Part 1: Introduction

#### Project Background

In today's busy and fast-paced life, everyone seeks a quick escape in the form of a holiday. However, the overwhelming number of choices and lack of personalized assistance can make holiday planning daunting. To address this, we have developed TravelAssist AI, a chatbot that combines the power of large language models and rule-based functions to ensure accurate and reliable information delivery.

#### Problem Statement

Given a dataset containing information about holiday packages (Package name, destination, number of days, sightseeing, etc.), build a chatbot that parses the dataset and provides accurate holiday recommendations based on user requirements.

#### Dataset

Data is gathered from Kaggle's MakeMyTrip dataset on holiday packages from the following link: : 'https://www.kaggle.com/datasets/promptcloud/travel-listing-from-makemytrip'. The original dataset contained 30k rows, but for this problem statement, it has been trimmed down to just 4 rows to overcome timeout issues with OpenAI.

### Approach

1. **Conversation and Information Gathering**: The chatbot will utilize language models to understand and generate natural responses. Through a conversational flow, it will ask relevant questions to gather information about the user's requirements.
2. **Information Extraction**: Once the essential information is collected, rule-based functions come into play, extracting relevant holiday packages that best match the user's needs.
3. **Personalized Recommendation**: Leveraging this extracted information, the chatbot engages in further dialogue with the user, efficiently addressing their queries and aiding them in answering any questions related to the package.

### Part 2: System Design

As shown in the image, the chatbot contains the following layers:
- Intent Clarity Layer
- Intent Confirmation Layer
- Product Mapping Layer
- Product Information Extraction Layer
- Product Recommendation Layer

#### Major Functions Behind the Chatbot

Let's look at a brief overview of the major functions that form the chatbot:
- `initialize_conversation()`: Initializes the variable conversation with the system message.
- `get_chat_model_completions()`: Takes the ongoing conversation as input and returns the response by the assistant.
- `moderation_check()`: Checks if the user's or the assistant's message is inappropriate. If any of these is inappropriate, it ends the conversation.
- `intent_confirmation_layer()`: Evaluates if the chatbot has captured the user's profile clearly, checking properties like 'Destination', 'Package', 'Origin', 'Duration', 'Budget'.
- `dictionary_present()`: Checks if the final understanding of the user's profile is returned by the chatbot as a Python dictionary.
- `compare_holiday_with_user()`: Compares the user's requirements with different holiday packages and returns the top recommendations.
- `initialize_conv_reco()`: Initializes the recommendations conversation.

### Part 3: Implementation

#### Implementing Intent Clarity & Intent Confirmation Layers

Building the `intent clarity` and `intent confirmation` layers helps in identifying user requirements and passing them on to the product matching layer. Functions used:
- `initialize_conversation()`: Uses prompt engineering and chain of thought reasoning to keep asking questions until user requirements are captured in a dictionary. Includes Few Shot Prompting to align the model about user and assistant responses at each step.
- `intent_confirmation_layer()`: Evaluates if the chatbot has captured the user's profile clearly, checking properties like Destination, Package, Origin, Duration, Budget.

#### Implementing Dictionary Present & Moderation Checks

- `dictionary_present()`: Checks if the final understanding of the user's profile is returned as a Python dictionary, used later for finding the right holiday packages.
- `moderation_check()`: Checks if the user's or the assistant's message is inappropriate, ending the conversation if necessary.

#### Implementing Product Mapping and Information Extraction Layer

Functions used to implement information extraction and product matching layers:
- `product_map_layer()`: Extracts key features and criteria from the holiday package dataset using specific rules and Few Shot Prompting.
- `extract_dictionary_from_string()`: Extracts the user requirements dictionary from the previous layer's output.
- `compare_holiday_with_user()`: Compares the user's profile with different holiday packages, filtering based on budget and matching user requirements with holiday data.

### Product Recommendation Layer

Steps involved:
1. Initialize the conversation for recommendation.
2. Generate recommendations and display them in a presentable format.
3. Ask questions based on the recommendations.

### Dialogue Management System

The `dialogue_mgmt_system()` function contains the logic of how the different layers interact, initiating the chatbot.

### User Interface

All functions are encompassed into a UI using the Flask framework, enabling seamless interaction between the bot and the user.

### Chatbot Functionalities, Limitations & Challenges

- Can cater to irrelevant requests apart from travel assistance.
- Handles offensive/prohibited content through moderation checks.
- Data limitation: Origin/Start City is only New Delhi or Mumbai, but can handle other cities.
- Handles scenarios where the user's budget is lower than the minimum value (6500 INR) in the dataset.
- Limitation: Looks for exact values entered by the user in the database, unable to recommend alternatives.
- Dataset contains only four rows, limiting positive scenarios for recommendations.
- User needs to enter 'ok' to fetch results after providing all details.
- Handles scenarios where user requirements do not match the dataset.
- Challenge: OpenAI timeout errors with larger datasets, hence using only 4 rows.
- Bot may still time out when fetching results; retry if errors occur.
