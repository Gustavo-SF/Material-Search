# Material-Search

> This repository is part of the Construction Supply Chain Pipeline for the MSc Thesis developed in Mota-Engil with support from Faculty of Sciences of the University of Lisbon.

## Introduction

In this section of the work, we are focusing in building a material search application that can be used by workers in Mota-Engil to find the materials they require. This repository has a `.ipynb` file that goes through the data exploration of the material data. Main outcomes from this exploration were:
- we will only use the material description information to help cluster the materials
- `editdistance` library is already a very fast implementation of the levenshtein distance between two words
- using the multiprocessing library is the fastest way to find the closest materials to each other using a custom function

## Sub-Repositories

### Material-Search-Processing

This repository is focused in doing the general processing of all of the data. This way we can upload all the clusters in the database and access them anytime we need. For example, when one user selects one material, he can immediately see which other materials are similar to that one.

For this processing to happen, I use a Virtual Machine to run a cron job every month. This job will do the multiprocessing of all of the data taking around 2h for 100,000 materials. To deploy all of the code and set up the machine, I use ansible.

### Material-Search-Model-Deployment

This last deployment is supposed to help with the general search. I create a model that will process the database data and according to a search query. This way, the user gets multiple results according to their search so he can more easily find what he requires.

This is all done using a deployment to the Azure Machine Learning, that creates an endpoint to make requests using the application.

### Material-Search-App

The last repository is the Flask App for material search, built using Flask. The app only allows a system configured user to sign-in. They are then able to use a search bar to find a material they need, and if they select one of the materials they can also find others closest to these.

The deployment is also done using ansible.