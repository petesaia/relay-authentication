An example app demonstrating role based authentication and file upload with Relay and GraphQL.

- [Authentication](#authentication)
- [File Upload] (#file-upload)
- [Getting Started](#getting-started)
- [Commands](#commands)
  - [test](#test)
  - [update-schema](#update-schema)
- [Credits and Further Information](#credits-and-further-information)
- [Changelog](#changelog)

## Overview
Users may have a role of type **reader**, **publisher** or **admin**. Readers can access a list of all posts and their own profile. Publishers can additionally create posts and see a list of their own posts. Admin role is not used widely yet.

## Authentication

Uses [cookie-session](https://github.com/expressjs/cookie-session) and [jsonwebtoken](https://github.com/auth0/node-jsonwebtoken) to save session data in form of a JSON Web Token in a cookie. This data contains the users id and its role and is made available as **rootValue** in GraphQL schema.

### Server

- **/server/graphQlServer.js** contains the express middleware used to get session data from the cookie.
- **/graphql/mutation/LoginMutation.js** contains the GraphQL mutation type for logging in.
- **/graphql/type/UserType.js** includes an example on how to use **rootValue** for retrieving restricted data in its **posts** field.

### Client

- **/client/mutation/LoginMutation.js** contains the client side login mutation.
- **/client/pages/user/login/login.js** utilizes this mutation.
- **/client/pages/user/posts/UserPosts.js** displays restricted user data.

## File Upload

### Client

- **/client/mutation/CreatePostMutation.js** uses [getFiles()](https://facebook.github.io/relay/docs/api-reference-relay-mutation.html#getfiles) to pass file data to the GraphQL server.
- **/client/pages/user/createPost/CreatePost.js** uses this mutation by passing it a [File](https://developer.mozilla.org/en/docs/Web/API/File) object retrieved from a HTML input element

### Server

- **/server/graphQlServer.js** contains a wrapper around [multer](https://github.com/expressjs/multer) middleware, which saves the image to disk and passes its file name to GraphQL. See [this comment](https://github.com/graphql/express-graphql/issues/9#issuecomment-143331902) for more information.

## Getting Started

```sh
$ npm install
```

Start the local dev server:

```sh
$ npm start
```

Navigate to **http://localhost:3000/** to view the app. Login with email **reader@test.com**, **publisher@test.com** or **publisher2@test.com** and password **qwerty**.

## Commands

### test

```sh
$ npm test:server
```

### update-schema

```sh
$ npm update-schema
```

## Credits and Further Information

Based on [Essential React](https://github.com/pheuter/essential-react) starter kit 

### Authentication

- [Issue](https://github.com/facebook/relay/issues/294) on Relay
- [Answer](http://stackoverflow.com/a/34974614/3489363) on stackoverflow
- [Question](http://stackoverflow.com/questions/33550843/authentication-and-access-control-with-relay) on stackoverflow

### File Upload

- [Comment](https://github.com/graphql/express-graphql/issues/9#issuecomment-143331902) on Relay issue by [murz](https://github.com/murz)

## [Changelog](CHANGELOG.md)
