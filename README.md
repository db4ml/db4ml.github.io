**CS-A1155: Databases for Data Science**

This repository contains materials for the course **CS-A1155: Databases for Data Science** at Aalto University.

A central theme of the course is the **relational data model**, which provides a precise framework for 
defining and reasoning about datasets. These datasets are essential for training and validating AI 
systems.

Datasets consist of data points, which are objects that carry information. For example, a real-world dataset 
could be a herd of cows:

<img src="./assets/Cows_in_the_Swiss_Alps.jpg" alt="Cows in the Swiss Alps" width="400" />

We can access the information carried by these data points (cows) in different ways, such as measuring their 
weight and height or placing a [sensor in their stomach](https://cordis.europa.eu/article/id/422078-trust-your-gut-a-stomach-based-sensor-to-monitor-cow-health).

However, directly working with such datasets can be impractical. Instead, we use a **data model** to approximate 
real-world datasets. Maybe the most widely used example of such a model is the **relational data model**. This data model 
revolves around the concept of a **relation (or table)** at its core. For example, a relation representing the above cow dataset 
might look like this:

| CowID | Weight(kg) | Age(years) | Height(cm) | Stomach_temp |
|--------|------------|-------------|-------------|------------|
| Zenzi  | 100        | 4           | 100         | 25  |
| Berta   | 140        | 3           | 130         |23  |
| Resi   | 120        | 4         | 120         | 31  |



## Accessing the Repository

You can find the full repository and additional resources [here](https://github.com/db4ml/db4ml.github.io).



### Image Acknowledgment

*“Cows in the Swiss Alps” by User:Huhu Uet is licensed under [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/).*
