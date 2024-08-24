# Prep exercise week 4

As a preparation step for the upcoming Q&A, you need to work on the following exercise, which is based on the prep
exercise of the previous week.

## Exercise

Last week you updated your database to be normalized. Now that you have some more NoSQL knowledge, convert your database
to a document-based database. Think about the following:

### 1. What are the collections?

- **Ingredients**
- **Steps**
- **Categories**
- **Recipes**

### 2. What information will you embed in a document and which will you store normalized?

**Embedded Information within Recipes Collection:**
- **Ingredients** (as arrays with ingredient IDs)
- **Steps** (as arrays with step IDs)
- **Categories** (as arrays with category IDs)

### Discussion

#### 1. What made you decide when to embed information? What assumptions did you make?

The decision to embed information was guided by the following considerations:

- **Data Hierarchy**: Recipes naturally consist of steps, ingredients, and categories. Embedding them within the `recipes` document reflects the real-world relationship where these elements are tightly coupled.

- **Performance**: Embedding these related data within the `recipes` document optimizes read performance by minimizing the need for multiple queries. All necessary information for a recipe is available in a single document, which reduces latency and enhances performance.

- **Consistency**: Keeping all relevant information together within a recipe document ensures that the data remains consistent. This approach assumes that the steps, ingredients, and categories are not frequently shared or reused across different recipes. If these elements were to be shared across multiple recipes, a normalized approach might be more suitable to avoid redundancy.

- **Write Frequency**: If the steps, ingredients, or categories are not frequently updated independently of the recipes, embedding them is a logical choice. The assumption here is that recipes are more frequently read than written, and when they are written, they include all necessary details at once.

#### 2. If you were given MySQL and MongoDB as choices to build the recipe's database at the beginning, which one would you choose and why?

Given the nature of the data:

- **MongoDB**: I would choose MongoDB for building the recipe's database because:
  - **Document Structure**: The hierarchical nature of recipes, which includes ingredients, steps, and categories, is a good fit for a document-based model where these related entities can be embedded within a single document.
  - **Flexibility**: MongoDB provides flexibility in schema design, allowing for easy adjustments to the data structure as the application evolves.
  - **Scalability**: MongoDB is well-suited for applications that require horizontal scaling and can handle large volumes of data across distributed systems.
  - **Performance**: For read-heavy applications where the recipe data is frequently accessed, MongoDB's ability to retrieve all relevant information in a single query enhances performance.

- **MySQL**: However, if the requirements involved complex transactions, strong data consistency, or frequent independent updates to ingredients, steps, or categories, MySQL might be a better choice due to its ACID (Atomicity, Consistency, Isolation, Durability) properties and the robustness of relational databases in handling complex queries and transactions.

In summary, the choice between MongoDB and MySQL depends on the specific use case. For a recipe database with a focus on flexibility, performance, and hierarchical data, MongoDB would be the preferred option. However, for applications requiring strong consistency and complex transactions, MySQL would be more appropriate.