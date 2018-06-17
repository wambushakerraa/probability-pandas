# probability-pandas
import pandas as pd

#creating empty list
list_cars = []

# Asks the user for the number of cars (i.e. data instances)
no_of_instances = input('Enter the number of car instances:\t')

#For each car, asks the user to enter the following fields: make, model, type, rating 
for i in range(no_of_instances):
    columns=['make','model','type','rating']
    features = raw_input("Enter the make,model,type,rating:\t")
    list_zip = features.split(',')
    dict_list = zip(columns, list_zip)
    d= dict(dict_list)
    list_cars.append(d)

#Save the feature values for each car in a DataFrame object.
df = pd.DataFrame(list_cars)
df = df[['make','model','type','rating']]

#Displays the resulting DataFrame
print df


#Computes the probability of each rating and outputs to the screen
rating_probs = df.groupby('rating').size().div(len(df))

#For each type t, computes the conditional probability of that type, given each of the ratings
typet_probs = df.groupby(['type', 'rating']).size().div(len(df)).div(rating_probs, axis=0, level=1)

#Displays the conditional probabilities to the screen.
print rating_probs
print typet_probs

