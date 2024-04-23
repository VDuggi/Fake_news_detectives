# Fake_news_detectives
This is a group project the MSU AI Bootcamp.  For this project, we worked as a group to find and analyze a dataset of our choice. The aim of our project is to create a model that can differentiate fake vs real news.

Team Fake_news_detectives:  Gi'Anna Cheairs, Tim Carter, Vineet Duggi, Tom Clemons 

## Getting Started

### Dependencies

- Python 3.10
- vaderSentiment
- Python Matplotlib
- Jupyter Notebooks
- Python sklearn
- Pickle
- WordCloud
- STOPWORDS
- Hugging Face

### Installing

- Clone this repo to your environment 

### Notebooks and Data Files 

**Notebooks created for this project:** 
| **Notebook** | **Description** |
| --- | --- | 
| **Data Preparation:** | | 
| **fake_news_detector_data_prep.ipynb** | Reads real and fake news article data files and performs inital cleansing to create clean data files merged into 1 dataframe with class and cleaned_text columns. Then splits into 4 files due to GitHub file size restrictions  |
| | |
| **Data Modeling and Predictions:** | | 
| **fake_news_detector_pa_model.ipynb** | Calculated TF-IDF and Passive Aggressive Classifier. Calculated Accuracy & precision; then did a confusion matrix for further verification of accuracy score. Used pickle to save PAC & TF-IDF, for future ease of use. |
| **fake_news_detector_wordcloud.ipynb** | Generated 2 word clouds for real and fake articles |
| **fake_news_detector_vader.ipynb** | Takes in sentences and assigns a sentiment rating |
| **fake_news_detector_gradio_classification.ipynb** | Created a user interface that takes in both text and audio files |

**Data files created for this project:** 
| **Data File** | **Description** |
| --- | --- | 
| **fake_articles.csv** | Fake news Dataset |
| **real_articles.csv** | Real news Dataset |
| **fake_article_audio.wav** | Fake news audio file |
| **real_article_audio.wav** | Real news audio file |
| **gradio_article_example.png** | User interface png |
| **gradio_audio_example.png** | User interface png |
| **gradio_blank_fields.png** | User interface png |
| **gradio_sentiment_example.png** | User interface png |
| **VaderSentiment - Fake.png** | Fake Vader sentiment pie chart png |
| **VaderSentiment - Real.png** | Real Vader sentiment pie chart png |
| **pa_classfier.pkl** | PAC saved via pickle |
| **tfid_vectorizer.pkl** | PAC saved via pickle |
| **WordCloud - Fake.png** | Fake Wordcloud png |
| **WordCloud - Real.png** | Real Wordcloud png |
| **X_test.csv** | Split data - X_test |
| **X_train.csv** | Split data - X_train |
| **X_test.csv** | Split data - X_test |
| **y_test.csv** | Split data - y_test |
| **y_train.csv** | Split data - y_train |
| **df_merged_articles_clean_part1.csv** | Split dataframe - part 1 |
| **df_merged_articles_clean_part2.csv** | Split dataframe - part 2 |
| **df_merged_articles_clean_part3.csv** | Split dataframe - part 3 |
| **df_merged_articles_clean_part4.csv** | Split dataframe - part 4 |

**Project Presentations:** 
| **Presentation** | **Description** |
| --- | --- | 
| **Fake News Detectives - Presentation.pptm** | Powerpoint version of team presentation |
| **Fake News Detectives - Presentation.pdf** | PDF version of team presentation |

# Exploration and Clean up of data

- Reconciled which import/libraries are needed for each notebook - we initially imported multiple
- Cleaned up null dates and bad dates, there were over 12k, so we dropped the date column all together
- Added a class to determine real = 1, fake = 0
- Concatenated and merged dataframes
- Verified class totals using value.count
- Clean function
   - Removed symbols, https, urls, punctuation, made lowercase, tokenize, etc.
- Split merged df into 4 files, because it was so large

# Data Model Implementation

- PAC Model 
  - Read in 4 csv files
  - Cleaned text didn’t match the text count. We realized that some cleaned columns were null         because they had things that were dropped in the clean function: https, etc.
  - TF-IDF - calculated tfid vectorizer
  - PAC was highly accurate - we used 30% which is why the 'support' in the classification report was   only ~13,000 out of 40,000 articles 
  - Confusion matrix - ran as additional accuracy verification
  - Used pickle to save our PA model and TF-IDF, so that we don’t have to run the notebook everytime we want to use it
  - Saved split data, in case we wanted to use it in additional models. Can condense code for future models

- Word cloud
  - Repeated set up for PAC
  - Created smaller dataframe, dropping all but 2 columns needed for word cloud; ‘cleaned_text’ & ‘class’
  - Then split the DataFrame into 2 dataframes, 1 for real & 1 for fake
  - Created 2 word clouds, 1 real & 1 fake
  - Iteratively removed stop words

- VADER - sentiment analysis
  - Takes in sentences and assigns a rating
  - New import - installed a new Vader library
  - Created smaller DF dropping all but 2 cols needed for word cloud; ‘title’, ‘cleaned_text’ & ‘class’
  - Created a function that measures the sentiment of a sentence, based on language & tone of the article title, because measuring sentiment on larger strings of data becomes more inaccurate; it will lean more negative
  - Created a new column for ‘sentiment’ and added column on to the database
  - Split DataFrame into 2 dataframes; real & fake. Generated sentiment for each.

- Gradio - User Ingterface
  - Uses Hugging Face library
  - Lots of libraries imported
  - Use pickle to restore models - PAC & TF-IDF
  - Defined clean_text function
  - Defined article_prediction function
    - Cleans, vectorizes & then predicts
  - Defined get_sentiment_rating
  - Defined transcribe_text
  - Assesses sentiment of article after we ran it through the clean function
  - Defines function article_sentiment_prediction
  - Calls other functions that we just created
  - Created Gradio that takes text input, calls article_sentiment_prediction and produces output indicating sentiment & real vs fake

## Authors

- Authors:  Gi'Anna Cheairs, Tim Carter, Vineet Duggi, Tom Clemons 

## Version History

- 0.1
    - Initial Release

## Acknowledgments

- Real & Fake News Data -  https://www.simplilearn.com/tutorials/machine-learning-tutorial/how-to-create-a-fake-news-detection-system