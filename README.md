## Learning Objectives

- The students should be able to understand the fundamental differences between GraphQL and REST APIs and articulate the benefits of using GraphQL over REST for specific use cases.
- The students should be able to describe the key concepts of GraphQL, including queries, and mutations.
- The students should be able to differentiate between various GraphQL types and fields.

### Intro to GraphQL

GraphQL is a query language for your API, designed to give clients the power to ask for exactly what they need and nothing more. It provides a more  flexible alternative to traditional REST APIs.

Remeber REST apis rely on hitting endpoints with pre-built queries. Where as GraphQL queries can be customized on the fly.

## Key Benefits of GraphQL

1. **Efficiency:** With GraphQL, each client can request precisely what they need, reducing over-fetching of data. 

2. **Flexibility:** GraphQL lets clients define their data requirements, avoiding the need for multiple endpoints catering to different needs. 


## Basics of GraphQL Queries and Mutations

### **Queries: Ordering Your Data**

In a bakery, making a query is like placing an order for your favorite pastry. You specify what you want – the type, flavor, and any additional toppings. For example,

```graphql
# (graphql syntax)
query { #submitting a query
    #querying a using, name to filter
  pastry(name: "chocolate croissant") { 
    name #These are the fields we want returned to us. (name,price, ingredients)
    price
    flavor
  }
}
```
### Mutations: Creating and Updating data

```graphql
# (graphql syntax)
mutation { #creating a mutation
    #mutation function addPastry() creates a pastry Object with the following fields/parameters
  addPastry(name: "Blueberry Muffin", flavor: "blueberry", price: 2.50) {
    name    #once created the following fields are returned
    price
  }
}
```

### Types

Types in GraphQL are a combination of predefined datatypes, aswell as types you define yourself as a Type Object. The types are used to define the structure of your data, and API capabilities.


- Scalar Types: Are your basic units of data, Strings Ints, Booleans, IDs, Floats

```graphQL
type User {
  #The following are scalar types
  id: ID!
  name: String!
  age: Int
  height: Float
  isActive: Boolean
}
```
- Objects Types: Object types are similar to python classes, and represent complex objects with multiple fields

```graphQL
#User is our Object type, made up of Scalar types
type User {
  id: ID! #exclamation points indicate that a field cannot be null
  name: String!
  age: Int
}

type Query {
  user: User #user field is of type User
}
```

- Query Types: Special type that defines what can be queried from the data base

```graphQL
#Defining our available queries
type Query {
  users: [User]
  user(id: ID!): User #When quering a single userm you need to pass in an id 
  Posts: [Post]
  post(id: ID!): Post
}

#actually running a query and selecting what fields we want
query {
  users {
    name
  } #Returns a list of users, but only their name included
}
```
- Mutation Type: Special type that allows us to manipulate/ add data to our database
```graphQL
type Mutation {
  addBook(title: String!, author: String!): Book!
  addUser(id: ID!, name: String!, age: Int): User! #function to create a user, and returns a User object which is required
}
```
### Fields

Fields are equivalent to the columns of a database, or the keys in the Object type

