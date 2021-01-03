# movieql

Movie API with GraphQL (GraphQL tutorial)  
by Nomad Coder (https://nomadcoders.co/graphql-for-beginners/)

## Problems solved by GraphQL

### GraphQL로 할 수 있는 것

1. Over-fetching 해결 - 요청한 영역의 정보보다 많은 정보를 받는 것
2. Under-fetching 해결 - 하나를 완성하기 위해 여러 요청을 추가적으로 해야 하는 것

over-fetching, under-fetching 없이 코드를 짜고 개발자가 어떤 정보를 원하는 지에 대해 통제하는 것  
한 query에 원하는 정보만 받게 하는 것.
URL 체계는 없다. 하나의 endpoint만 있다.

graphQL 언어로 정확히 무슨 정보를 원하는지 하나의 query로 만들 수 있다.  
답으로 JS Object를 받을 수 있다.

## Creating a GraphQL Server with GraphQL Yoga

<pre><code>
import { GraphQLServer } from "graphql-yoga";

const server = new GraphQLServer({});

server.start(() => console.log("Graphql Server Running"));


</code></pre>

## Creating the first Query and Resolver

Schema : 주고받을 정보에 대한 서술  
schema.graphql : Mutation(정보 변형), Query(정보 받기)에 대한 정보 서술

<pre><code>
// in schema.graphql
type Query{
    name: String!
}

type Mutation{

}

// in index.js
typeDefs: ""

// in resolvers.js (해결해야 할 Query)
const resolvers = {
  Query: {
    name: () => "nicolas"
  }
};

////여기에 query를 어떻게 보내줄지를 프로그래밍한다.

export default resolvers;
</code></pre>

View나 URL로 작동되는 게 아니라, Query와 Resolver로 작동되는 GraphQL.  
localhost:4000 에서 확인.

## Extending the Schema

! : required (! 없으면 못 찾을 때 null 반환)
[] : array, multiple

새롭게 정의한 type에서 원하는 정보만 골라서 query를 요청할 수 있다.

<pre><code>
    person(id: Int!): Person
</code></pre>

## Creating Queries with Arguments

GraphQLServer가 Query나 Mutation의 정의를 발견하면 Resolver를 찾아서 해당 함수를 실행한다.  
query를 줄 때 argument를 줄 수 있다.

Resolver는 다른 API나 DB에 얼마든지 접근가능하다. 훨씬 나은 방식.

## Mutations

### Mutaion : change of stage.

<pre><code>
// in Schema
type Mutation {
  addMovie(name: String!, score: Int!): Movie!
  deleteMovie(id: Int!): Boolean!
}

// in Resolver
const resolvers = {
  Query: {
      ...
  },
  Mutation: {
    addMovie: (_, { name, score }) => addMovie(name, score),
    deleteMovie: (_, { id }) => deleteMovie(id),
  },
};

// 이 경우 자세한 함수는 db.js에서 구현
</code></pre>

## Wrapping a REST API with GraphQL

기존의 REST API를 감싸서 필요한 정보만 받을 수 있게 하자.  
기존 API에서 fetch해서 사용하는 것. (axios도 가능)  
기존 스키마에 맞게 우리의 스키마도 수정한다.

<pre><code>
// after 'yarn add node-fetch

import fetch from "node-fetch";
const API_URL = "https://yts.am/api/v2/list_movies.json";

export const getMovies = (limit, rating) => {
  return fetch(`${API_URL}`)
    .then(res => res.json())
    .then(json => json.data.movies);
};

</code></pre>

적절한 string 조작으로 URL 만들어서 조건을 줄 수도 있다.  
이 경우에 resolver.js에서 query의 argument로 줄 수도 있을 것이다.  
쉬우니까 생략
