# The orgine of music

## Introduction 

We will be studying the dataset called *Geographical Original of Music* which can be found on the [UCI Machine learning site](https://archive.ics.uci.edu/ml/datasets/Geographical+Original+of+Music)
This dataset contains audio features from 1059 songs labelled with their country of origine (longitude and lattitude).
The purpose of this dataset is to predict the country of origine of songs automaticaly.


Their are 33 countries represented in this dataset.
The music used is traditional, ethnic or "world" only, as classified by the publishers of the product on which it appears. Any Western music is not included because its influence is global - what we seek are the aspects of music that most influence location
The features where extracted from the waves files using the program MARSYAS

This dataset was used in the article *"Predicting the Geographical Origin of Music"* by Fang Zhou, Q. Claire and Ross D. King which I was not able to find for free :(
The problem can be adressed using 
 * regression : but the spheric coordinates complexify the problem
 * classification : we first need to transform the target from a {longitude;lattitude} couple to a country

## Detailled problem description

The input is a 70 x 1059 CSV file where the first 68 columns are numbers between -1 and 1 describing the feature extracted from the wave files using the MARSYAS program.  
The last two columns are number representing the latitude and longitute where the music orgines from.  

Our objective will be to be able to predict the country of origine of a new song from its 68 MARSYAS feature.  

We will be using a classification algorithm (regularized logistic regression)  

The First transformation on this dataset will be to replace the last two columns by the country code corresponding to the lattitude and longitude points provided.
This will be done using the geonames.org API which can return a crountry code from a {lattitude ; longitude} couple.

Then we will randomly reorder the dataset and split it into training, testing and validation dataset. 

At this point we will be ready to run our algorithme on the training dataset and adjust our regularisation parameter on the testing dataset.

The effectiveness of the algorithme will be assessed by measuring the share of well classified songs. This metrics looks good given songs are fairly well distributed accross the 33 represented countries.

Using Tom Mitchell's definition of machine learning problem :  
 * Our experience E is MARSYAS feature labbeled with the geo origine of the song  
 * Our program's task is to infer a songs country of origine from its 68 MARSYAS feature 
 * Our program's performance is measured by the share of well classified songs

## Proposed solution

Given the small amount of exemple and the relatively large number of feature using logistic regression and including quadratic feature might result in overfitting.  
We will thus use a neuron network with one layer of 68 neurons.

It's hard to think of a very basic benchmark model given the exemple are well spread accross all possible class. 
We could use the most frequent one which is India (70 out of 1059)




