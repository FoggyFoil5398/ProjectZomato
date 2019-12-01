# ProjectZomato

### Requirements :

1. Selenium
2. Spacy
3. Beautiful Soup
4. Fuzzy Wuzzy
5. Vader Sentiment

## This project is used to generate ratings for food items from reviews of a specific restaurant.

1. The Food items extracted are extracted by custom NER model (Read more below in Section 1)
2. The ratings are calculated for each extracted Food item from reviews (Read more below in Section 2)

## Section 1

A custom NER model is made in the file 'Food_NER_model_generator.ipynb' 

The process :

1. You are required to create an excel file to be used to train custom NER model
2. You can use the already present excel file foodcsv.xlsx or increase the data in the same file and then use it
3. To learn more about how to add more data, read the foodcsv.xlsx file, or read here https://spacy.io/usage/training

What you have to do :

1. If you are using the already provided foodcsv.xlsx then just call function 'generate_food_model' in Food_NER_model_generator.ipynb with parameters df_path = path where your foodcsv.xlsx is stored locally in your system and output_dir = location of directory where you want custom model to be saved
2. If you are using your own excel file, follow the approach in above point, just change df_path to path where your new excel file is stored

## Section 2

### Calculating the ratings

The thought process used behind calculating rating for food items is as follows

1. Extract reviews along with ratings of reviews and store it in a dataframe. The extraction is done using Selenium and BeautifulSoup
2. Create a dictionary for each food item extracted using custom NER model as key and the reviews containing these food items as values
3. For each key (food item) present, use fuzzywuzzy to merge food items having similarity more than the score '90'
4. For each sentence corresponding to a food item, calculate the rating based on the following

4.1 If the rating is present in the review (Example Momos 4.5/5), use the rating directly

4.2 If the rating is not present in review, use VaderSentiment and normalise it to get a rating out of 5

5. For each rating obtained for a food item, average it to obtain corresponding rating to that specific food item

## What can be done to improve

1. The NER model can be made better by increasing the examples in foodcsv.xlsx
2. The sentiment calculated by vader sentiment for the sentence, corresponds same score to every item in sentence. Example "Pizza was good, Pasta was bad."

If in the above sentence, vadersentiment calculates 2.5 rating, it will correspond it to both Pizza and Pasta. Nlp techniques can be used to solve this which I am currently unfamiliar with, If you have suggestions, please feel free to tell those !
