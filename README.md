# Filtering, Ordering, and Limiting Data with SQL - Lab


## Introduction
In this lab, you will practice writing SQL `SELECT` queries that limit results based on conditions, using `WHERE`, `ORDER BY`, and `LIMIT`.

## Objectives
You will practice the following:

* Order the results of your queries by using `ORDER BY` (`ASC` & `DESC`)
* Limit the number of records returned by a query using `LIMIT`
* Write SQL queries to filter and order results

## The Data

Here's a database full of famous dogs!  The `dogs` table is populated with the following data:

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

## Connecting to the Database

In the cell below, import `pandas` and `sqlite3`. Then establish a connection to the database `dogs.db`.

Look at all of the data in the table by selecting all columns from the `dogs` table with `pd.read_sql`.


```python
# Relevant imports
import pandas as pd
import sqlite3

# Create a connection
conn = sqlite3.connect('dogs.db')

# Select all
pd.read_sql("SELECT * FROM dogs;", conn)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>id</th>
      <th>name</th>
      <th>age</th>
      <th>gender</th>
      <th>breed</th>
      <th>temperament</th>
      <th>hungry</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>Snoopy</td>
      <td>3</td>
      <td>M</td>
      <td>beagle</td>
      <td>friendly</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>McGruff</td>
      <td>10</td>
      <td>M</td>
      <td>bloodhound</td>
      <td>aware</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>Scooby</td>
      <td>6</td>
      <td>M</td>
      <td>great dane</td>
      <td>hungry</td>
      <td>1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>Little Ann</td>
      <td>5</td>
      <td>F</td>
      <td>coonhound</td>
      <td>loyal</td>
      <td>0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>Pickles</td>
      <td>13</td>
      <td>F</td>
      <td>black lab</td>
      <td>mischievous</td>
      <td>1</td>
    </tr>
    <tr>
      <th>5</th>
      <td>6</td>
      <td>Clifford</td>
      <td>4</td>
      <td>M</td>
      <td>big red</td>
      <td>smiley</td>
      <td>1</td>
    </tr>
    <tr>
      <th>6</th>
      <td>7</td>
      <td>Lassie</td>
      <td>7</td>
      <td>F</td>
      <td>collie</td>
      <td>loving</td>
      <td>1</td>
    </tr>
    <tr>
      <th>7</th>
      <td>8</td>
      <td>Snowy</td>
      <td>8</td>
      <td>F</td>
      <td>fox terrier</td>
      <td>adventurous</td>
      <td>0</td>
    </tr>
    <tr>
      <th>8</th>
      <td>9</td>
      <td>None</td>
      <td>4</td>
      <td>M</td>
      <td>golden retriever</td>
      <td>playful</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>



 

## Queries

Display the outputs for each of the following query descriptions.

### Select the name and breed for all female dogs

<details>
    <summary style="cursor: pointer; display: inline"><h4>Click for hint:</h4></summary>
    <p>Use <code>WHERE</code> with the <code>=</code> operator</p>
</details>


```python
pd.read_sql("""
SELECT name, breed
  FROM dogs
 WHERE gender = 'F';
""", conn)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>name</th>
      <th>breed</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Little Ann</td>
      <td>coonhound</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Pickles</td>
      <td>black lab</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Lassie</td>
      <td>collie</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Snowy</td>
      <td>fox terrier</td>
    </tr>
  </tbody>
</table>
</div>



### Select the number of dogs that do not have a name

<details>
    <summary style="cursor: pointer; display: inline"><h4>Click for hint:</h4></summary>
    <p>Use <code>COUNT</code> and <code>IS NULL</code></p>
</details>


```python
pd.read_sql("""
SELECT COUNT(*) AS num_dogs
  FROM dogs
 WHERE name IS NULL;
""", conn)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>num_dogs</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>



### Select the names of all dogs that contain the double letters `ff` or `oo`

<details>
    <summary style="cursor: pointer; display: inline"><h4>Click for hint:</h4></summary>
    <p>Use <code>LIKE</code>, <code>%</code>, and <code>OR</code></p>
</details>


```python
pd.read_sql("""
SELECT name
  FROM dogs
 WHERE name LIKE '%ff%'
    OR name LIKE '%oo%';
""", conn)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>name</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Snoopy</td>
    </tr>
    <tr>
      <th>1</th>
      <td>McGruff</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Scooby</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Clifford</td>
    </tr>
  </tbody>
</table>
</div>



### Select the names of all dogs listed in alphabetical order.  Notice that SQL lists the nameless dog first.

<details>
    <summary style="cursor: pointer; display: inline"><h4>Click for hint:</h4></summary>
    <p>Use <code>ORDER BY</code></p>
</details>


```python
pd.read_sql("""
SELECT name
  FROM dogs
 ORDER BY name;
""", conn)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>name</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>None</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Clifford</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Lassie</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Little Ann</td>
    </tr>
    <tr>
      <th>4</th>
      <td>McGruff</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Pickles</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Scooby</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Snoopy</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Snowy</td>
    </tr>
  </tbody>
</table>
</div>



### Select the name and breed of only the hungry dogs and list them from youngest to oldest


```python
pd.read_sql("""
SELECT name, breed
  FROM dogs
 WHERE hungry = 1
 ORDER BY age;
""", conn)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>name</th>
      <th>breed</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Snoopy</td>
      <td>beagle</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Clifford</td>
      <td>big red</td>
    </tr>
    <tr>
      <th>2</th>
      <td>None</td>
      <td>golden retriever</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Scooby</td>
      <td>great dane</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Lassie</td>
      <td>collie</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Pickles</td>
      <td>black lab</td>
    </tr>
  </tbody>
</table>
</div>



### Select the oldest dog's name, age, and temperament

<details>
    <summary style="cursor: pointer; display: inline"><h4>Click for hint:</h4></summary>
    <p>Use <code>ORDER BY</code> with <code>LIMIT</code></p>
</details>


```python
pd.read_sql("""
SELECT name, age, temperament
  FROM dogs
 ORDER BY age DESC
 LIMIT 1;
""", conn)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>name</th>
      <th>age</th>
      <th>temperament</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Pickles</td>
      <td>13</td>
      <td>mischievous</td>
    </tr>
  </tbody>
</table>
</div>



### Select the name and age of the three youngest dogs


```python
pd.read_sql("""
SELECT name, age
  FROM dogs
 ORDER BY age
 LIMIT 3;
""", conn)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>name</th>
      <th>age</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Snoopy</td>
      <td>3</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Clifford</td>
      <td>4</td>
    </tr>
    <tr>
      <th>2</th>
      <td>None</td>
      <td>4</td>
    </tr>
  </tbody>
</table>
</div>



### Select the name and breed of the dogs who are between five and ten years old, ordered from oldest to youngest

<details>
    <summary style="cursor: pointer; display: inline"><h4>Click for hint:</h4></summary>
    <p>Use <code>WHERE</code> with <code>BETWEEN</code></p>
</details>


```python
pd.read_sql("""
SELECT name, breed
  FROM dogs
 WHERE age BETWEEN 5 AND 10
 ORDER BY age DESC;
""", conn)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>name</th>
      <th>breed</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>McGruff</td>
      <td>bloodhound</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Snowy</td>
      <td>fox terrier</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Lassie</td>
      <td>collie</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Scooby</td>
      <td>great dane</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Little Ann</td>
      <td>coonhound</td>
    </tr>
  </tbody>
</table>
</div>



### Select the name, age, and hungry columns for hungry dogs between the ages of two and seven.  This query should also list these dogs in alphabetical order.


```python
pd.read_sql("""
SELECT name, age, hungry
  FROM dogs
 WHERE hungry = 1
   AND age BETWEEN 2 AND 7
 ORDER BY name;
""", conn)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>name</th>
      <th>age</th>
      <th>hungry</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>None</td>
      <td>4</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Clifford</td>
      <td>4</td>
      <td>1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Lassie</td>
      <td>7</td>
      <td>1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Scooby</td>
      <td>6</td>
      <td>1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Snoopy</td>
      <td>3</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>



## Close the Database Connection


```python
conn.close()
```

## Summary

Great work! In this lab you practiced writing more complex SQL statements to not only query specific information but also define the quantity and order of your results. 
