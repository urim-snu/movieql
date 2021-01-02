# movieql

Movie API with GraphQL (GraphQL tutorial)

## #0.3 Problems solved by GraphQL

### GraphQL로 할 수 있는 것

1. Over-fetching 해결 - 요청한 영역의 정보보다 많은 정보를 받는 것
2. Under-fetching 해결 - 하나를 완성하기 위해 여러 요청을 추가적으로 해야 하는 것

over-fetching, under-fetching 없이 코드를 짜고 개발자가 어떤 정보를 원하는 지에 대해 통제하는 것  
한 query에 원하는 정보만 받게 하는 것.
URL 체계는 없다. 하나의 endpoint만 있다.

graphQL 언어로 정확히 무슨 정보를 원하는지 하나의 query로 만들 수 있다.  
답으로 JS Object를 받을 수 있다.

## #0.4 Creating a GraphQL Server with GraphQL Yoga

<pre><code>
import { GraphQLServer } from "graphql-yoga";

const server = new GraphQLServer({});

server.start(() => console.log("Graphql Server Running"));


</code></pre>

## #0.5 Creating the first Query and Resolver
