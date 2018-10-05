
# Filtering and Ordering - Lab

## Introduction
In this lab, we will write more `SELECT` statements to solidify our ability to query a SQL database.  We will also write more specific queries using the tools we learned in the previous lesson.

## Objectives
You will be able to:
* Limit the number of records returned by a query using `LIMIT`
* Filter results using `BETWEEN` and `IS NULL`
* Order the results of your queries by using `ORDER BY` (`ASC` & `DESC`)

## Famous Dogs

We have a database full of famous dogs!  The `dogs` table is populated with the following data:

|name      |age    |gender |breed           |temperament|hungry |
|----------|-------|-------|----------------|-----------|-------|
|Snoopy    |3      |M      |beagle          |friendly   |1      |
|McGruff   |10     |M      |bloodhound      |aware      |0      |
|Scooby    |6      |M      |great dane      |hungry     |1      |
|Little Ann|5      |F      |coonhound       |loyal      |0      |
|Pickles   |13     |F      |black lab       |mischievous|1      |
|Clifford  |4      |M      |big red         |smiley     |1      |
|Lassie    |7      |F      |collie          |loving     |1      |
|Snowy     |8      |F      |fox terrier     |adventurous|0      |
|NULL      |4      |M      |golden retriever|playful    |1      |

## Queries

Write your SQL queries in the `select.py` file.  Fill the empty string in each method with the proper query to get the tests in `test/index_test.py` to pass.

* `select_all_female_dogs_name_and_breed` returns the name and breed for all female dogs

* `select_all_dogs_names_in_alphabetical_order` returns the names of all dogs listed in alphabetical order.  Notice that SQL lists the nameless dog first.

* `select_nameless_dog` returns all information for any dog that doesn't have a name

* `select_hungry_dogs_name_and_breed_ordered_by_youngest_to_oldest` returns the name and breed of only the hungry dogs and lists them from youngest to oldest

* `select_name_age_and_temperament_of_oldest_dog` returns the oldest dog's name, age, and temperament

* `select_name_and_age_of_three_youngest_dogs` returns the three youngest dogs

* `select_name_and_breed_of_dogs_between_age_five_and_ten_ordered_by_oldest_to_youngest` returns the name and breed of only the dogs who are between five and ten years old

* `select_name_age_and_hungry_of_hungry_dogs_between_age_two_and_seven_in_alphabetical_order` returns the name, age, and hungry columns for hungry dogs between the ages of two and seven.  This query should also list these dogs in alphabetical order.

## Summary

Great work! In this lab we practiced writing more complex SQL statements to not only query specific information but also define the quantity of results and the order of our results. 
