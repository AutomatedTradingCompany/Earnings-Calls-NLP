# Stock Price Predictions from Earnings Calls

Rice Data Analytics Program
Team Members: Radhika Balasubramaniam, Chad Dubiel, Katy Fuentes, Pankaj Tahiliani

##Background
Every quarter, public companies report earnings and company updates. Companies host a conference call in order to provide additional commentary and answer questions from participants. 

##Data
The dataset used consists of earnings call transcripts for S&P 500 companies.
The team webscraped Seeking Alpha earning transcripts. The transcripts include a prepared remarks section, a question-and-answer section, and instructions from the call operator. 

## Key Considerations
Is there a change in stock price after an earnings call?
Does an earnings call influence the stock price?
Was is the call’s sentiment? What are common words/topics used across company earnings calls?
What is the price change for the stock before and after the call? Is there a trend or can you predict the change in price?

##Process
Download S&P100 and then S&P500 list from Wikipedia
Scrape Seeking Alpha webpages for each company transcript with date, title, URL
Narrow list to only earning call transcript URLs 
Scrape each Seeking Alpha webpage for the earnings call transcript and save to text file
Scrape Yahoo finance webpage by Stock symbol and download 2015 through 2020 stock price history
Read text files and preprocess text


### TF-IDF and count vectorization


#### Classification


#### Logistic Regression


### Text and Sentiment Analysis
For the purpose of this analysis, only the prepared remarks for 2020 earnings calls for S&P100 companies compared to the full transcript text to compare the difference.
The transcripts were modified by the following processing steps: 
• Removed numbers and punctuation
•Preprocessed text by cleaning up contractions, removing html, tokenizing words, lemmatized words, removed stop words, and minimum character words
• Removed infrequent words
Sentiment analysis is used to measure the attitude, sentiments, evaluations, or emotions of a speaker based on the algorithmic treatment of subjectivity in a text.


	#### Latent Dirichlet Allocation (LDA)
	Latent Dirichlet Allocation (LDA) models can be used to reveal a hidden structure in a collection of texts representing the weight of text in a topic space. The process involves loading data, cleaning, exploring general output in form of a word cloud, preparing the data for LDA analysis, training the LDA model, and analyzing the results with a visual. The earning call transcripts were uploaded in the raw format and cleaned with the various steps detailed above.  The wordcloud for the full transcript and prepared remarks are different but mostly contain the same common words. Next, the text was tokenized into a corpus and dictionary for each. The model was trained on 25 topics which was a combination of keywords based on a weight to the topic. To visual the topics pyLDAvis was used to better understand and interpret individual topics and their relationships.  For the most part the terms overlapped in the full transcript and prepared remarks, but the topic distribution varied significantly between the two.
	
	#### VADER Sentiment Intensity Analyzer (SIA) polarity scoring 
	VADER (Valence Aware Dictionary for Sentiment Reasoning) is a model used for text sentiment analysis that is sensitive to both polarity (positive/negative) and intensity. VADER sentimental analysis relies on a prepackaged dictionary that maps lexical features into scores, which categorize text into positive, neutral, and negative. These texts are aggregated by document to arrive at overall opinion. VADER uses a combination of sentiment lexicon and list of lexical features which are generally labelled according to their semantic orientation as either positive or negative .
	VADER was applied across the processed text of the full and prepared remarks section of the earnings call transcripts. The prepacked VADER Sentiment Intensity Analyzer (SIA) polarity scoring and lexicon was used and compared to Hu Liu  (HL) and Loughran McDonald   (LM) word lists to compare tone and impact of classifying a call’s sentiment correctly.    The Hu-Liu lexicon was developed from a feature space of online movie reviews that were assigned negativity/positivity scores by the reviewers themselves. The HL lexicon consists of 6,786 words labeled positive or negative. The LM lexicon was constructed from words that are prevalent in 10-K reports of publicly-traded companies. The positive and negative labels assigned to these words are specific to the finance domain. The LM lexicon consists of 2,707 positive or negative words. 
	
	Sentiment Totals	Using HL Dictionary	Using LM Dictionary
	Positive 		255			374
	Negative		88			16
	Neutral			58			11


	#### Linear Discriminant Analysis on sentiment scores and price
	Linear Discriminant Analysis is the linear classification technique for multi-classes of data. LDA consists of statistical properties of the data calculated for each class. LDA was applied across the processed text of the full and prepared remarks section of the earnings call transcripts. For purposes of this model, the “X” input consists of the adjusted close, close, high, low, open stock price and the SIA polarity which consists computations of subjectivity, polarity, negative, positive, and neutral scores. The “y” input consists of an imputed “label” value that measured the positivity score and assigned 1 for positive scores over 0.15 in the full transcript, based on the average of 0.150631, and 0.10 in the prepared remarks, based on the average of 0.143419. Based on the f1 score and classification numbers the model performed better with the condensed text in the prepared remarks which makes sense due to the variety of questions and answers included in the full transcript of the calls.


### LSTM



### GRU





##### Data Sources

S&P 100/500 List https://en.wikipedia.org/wiki/List_of_stock_exchanges 
Earnings Calls Transcripts* https://seekingalpha.com/earnings/earnings-call-transcripts 
*The transcripts from Seeking Alpha are protected by copyright and cannot be used for commercial purposes. This is an educational project for the Data Visualization Program at Rice University and the use of the information should be permitted on the Copyright Fair Use principal.  
Yahoo Finance Historical stock price- https://sg.finance.yahoo.com/ 

###### Next applications
Backtrack results
Predict trends
Predict price
Embed sentiment in model

