```
This simple api has a books struct in memory
It has methods to get the entire list of books,
A method to get a book by id,  which calls another method that loops through the list and return a matching id,
A method to create a book and post it in the books list,
A checkout method which just reduces the quantity of the book
and a returnBook method which increments the books quantity.
```

Install mod.go which tracks our dependancies list for this project
`go mod init example/go-api-test`

We’re using the gin framework for api which is popular in the go community
`go get  github.com/gin-gonic/gin`

Writing the books data in memory

Main function holds the router. The router is gin.Default()
Which will handle different routes.
“/books” route is routed to getBooks function which takes in gin.Context which is basically all the information about the request and allows you to return a response
`router.GET("/books",getBooks)`
`c.IndentedJSON(http.StatusOK, books)` returns it in a serialized nicely formatted JSON object of books
router.Run("localhost:8080")
So if you run localhost:8080/books, it will return `c.IndentedJSON(http.StatusOK, books)`

Testing the api  using curl,
GET("/books", getBooks), `curl localhost:8080/books`
GET("/books/:id", bookById), `curl localhost:8080/books/2` returns book with id 2
POST("/books", createBook), `curl localhost:8080/books --include --header "Content-Type: application/json" -d @body.json --request  "POST"`
PATCH("/checkout", checkoutBook), `curl --request PATCH 'localhost:8080/checkout?id=2'`
router.PATCH("/return", returnBook), `curl --request PATCH 'localhost:8080/return?id=2'`
