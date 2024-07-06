# Whatsapp_Chat_Analyzer:
This is a streamlit app created by me that analyzes whatsapp chats. It is very useful to analyze the chats, it can be used for fun or by investigating agensies for investigation

A WhatsApp Chat Analyzer project involves analyzing the chat data from WhatsApp to gain insights and statistics about the conversations. This project can provide various metrics such as message counts, most active participants, common words, and activity trends over time.

### Key Steps:

1. **Data Extraction**:
   - **Export Chat**: Export the WhatsApp chat to a text file from the WhatsApp application.
   - **Read Data**: Load the exported text file into a Python script for analysis.

2. **Data Preprocessing**:
   - **Parse Messages**: Extract dates, times, senders, and messages from the text file.
   - **Clean Data**: Handle special characters, emojis, and other non-textual data. Convert dates and times to a standard format.

3. **Exploratory Data Analysis (EDA)**:
   - **Message Counts**: Calculate the total number of messages sent by each participant.
   - **Activity Trends**: Analyze message frequency over different time periods (daily, weekly, monthly).
   - **Word Frequency**: Identify the most common words and phrases used in the chat.

4. **Visualization**:
   - **Plots and Charts**: Create visualizations such as bar charts, line graphs, and word clouds to present the findings.
   - **Libraries**: Use libraries like Matplotlib, Seaborn, and WordCloud for creating visualizations.

5. **Advanced Analysis**:
   - **Sentiment Analysis**: Analyze the sentiment of the messages using natural language processing (NLP) techniques.
   - **Topic Modeling**: Identify common topics discussed in the chat using techniques like Latent Dirichlet Allocation (LDA).

### Basic Code Example (Python):
```python
import pandas as pd
import matplotlib.pyplot as plt
from wordcloud import WordCloud
import re

# Function to parse the chat file
def parse_chat(file_path):
    with open(file_path, 'r', encoding='utf-8') as file:
        chat_data = file.readlines()

    messages = []
    for line in chat_data:
        match = re.match(r'(\d{1,2}/\d{1,2}/\d{2,4}), (\d{1,2}:\d{2} [APM]{2}) - (.*?): (.*)', line)
        if match:
            date, time, sender, message = match.groups()
            messages.append({'date': date, 'time': time, 'sender': sender, 'message': message})

    return pd.DataFrame(messages)

# Load and parse the chat data
df = parse_chat('WhatsAppChat.txt')

# Convert date to datetime format
df['date'] = pd.to_datetime(df['date'], format='%m/%d/%y')

# Message count by sender
message_counts = df['sender'].value_counts()

# Plot message counts
message_counts.plot(kind='bar')
plt.title('Message Counts by Sender')
plt.xlabel('Sender')
plt.ylabel('Number of Messages')
plt.show()

# Word cloud of the messages
all_messages = ' '.join(df['message'])
wordcloud = WordCloud(width=800, height=400, max_words=100).generate(all_messages)

plt.figure(figsize=(10, 5))
plt.imshow(wordcloud, interpolation='bilinear')
plt.axis('off')
plt.title('Word Cloud of Messages')
plt.show()
```

### Applications:
- **Personal Insights**: Gain personal insights into messaging habits and interactions with friends and family.
- **Group Analysis**: Understand dynamics and engagement in group chats.
- **Business Insights**: For businesses using WhatsApp for customer service, analyze customer interactions and feedback.

### Tools and Libraries:
- **Pandas**: For data manipulation and analysis.
- **Matplotlib/Seaborn**: For creating plots and visualizations.
- **WordCloud**: For generating word clouds.
- **NLTK/TextBlob**: For natural language processing tasks such as sentiment analysis.

A WhatsApp Chat Analyzer project can reveal interesting patterns and insights about communication habits, providing both quantitative and qualitative analysis of chat data.
