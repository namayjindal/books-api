# Books API

A simple RESTful API built with Go (Golang) to manage a list of books. This project demonstrates core concepts in Go, including structs, HTTP handling, JSON encoding, and basic CRUD operations.

## Getting Started

### Prerequisites

- [Go](https://golang.org/dl/) (Version 1.20 or later)
- Curl or Postman (for testing endpoints)

### Installation

1. **Clone the repository**:
   ```sh
   git clone https://github.com/yourusername/books-api.git
   cd books-api
   ```

2. **Initialize Go modules**:
   ```sh
   go mod init github.com/yourusername/books-api
   go mod tidy
   ```

3. **Install Gorilla Mux** (used for routing):
   ```sh
   go get -u github.com/gorilla/mux
   ```

4. **Run the server**:
   ```sh
   go run main.go
   ```

   The server will start on `http://localhost:8080`.

---

## API Endpoints

| Method | Endpoint        | Description                  |
|--------|------------------|------------------------------|
| GET    | `/books`        | Retrieve all books           |
| GET    | `/books/{id}`   | Retrieve a book by ID        |
| POST   | `/books`        | Add a new book               |
| PUT    | `/books/{id}`   | Update a book by ID          |
| DELETE | `/books/{id}`   | Delete a book by ID          |

---

## Usage

Below are examples of how to use each endpoint. You can use [curl](https://curl.se/) or Postman for testing.

### 1. Get All Books

- **Request**:
   ```sh
   curl -X GET http://localhost:8080/books
   ```

- **Response** (example):
   ```json
   [
       {
           "id": 1,
           "title": "Go Programming",
           "author": "Alice"
       },
       {
           "id": 2,
           "title": "Learn Go",
           "author": "Bob"
       }
   ]
   ```

### 2. Get Book by ID

- **Request**:
   ```sh
   curl -X GET http://localhost:8080/books/1
   ```

- **Response**:
   ```json
   {
       "id": 1,
       "title": "Go Programming",
       "author": "Alice"
   }
   ```

### 3. Add a New Book

- **Request**:
   ```sh
   curl -X POST -H "Content-Type: application/json" -d '{"title": "New Book", "author": "John Doe"}' http://localhost:8080/books
   ```

- **Response**:
   ```json
   {
       "id": 3,
       "title": "New Book",
       "author": "John Doe"
   }
   ```

### 4. Update a Book by ID

- **Request**:
   ```sh
   curl -X PUT -H "Content-Type: application/json" -d '{"title": "Updated Book", "author": "Jane Doe"}' http://localhost:8080/books/1
   ```

- **Response**:
   ```json
   {
       "id": 1,
       "title": "Updated Book",
       "author": "Jane Doe"
   }
   ```

### 5. Delete a Book by ID

- **Request**:
   ```sh
   curl -X DELETE http://localhost:8080/books/1
   ```

- **Response** (deleted book):
   ```json
   {
       "id": 1,
       "title": "Updated Book",
       "author": "Jane Doe"
   }
   ```

---

## Project Structure and Code Explanation

### `main.go`

The main Go file (`main.go`) contains all logic for the API server.

- **Struct Definition**:
   ```go
   type Book struct {
       ID     int    `json:"id"`
       Title  string `json:"title"`
       Author string `json:"author"`
   }
   ```
   The `Book` struct defines the data model for each book, with fields `ID`, `Title`, and `Author`. JSON tags map struct fields to JSON keys.

- **Route Handlers**:
   - `getBooks`: Fetches all books in the list.
   - `getBook`: Retrieves a single book by its ID.
   - `createBook`: Adds a new book based on JSON input from the request.
   - `updateBook`: Updates the details of a book based on its ID.
   - `deleteBook`: Removes a book from the list based on its ID.

- **Router Setup and Server Start**:
   ```go
   func main() {
       router := mux.NewRouter()
       router.HandleFunc("/books", getBooks).Methods("GET")
       router.HandleFunc("/books/{id}", getBook).Methods("GET")
       router.HandleFunc("/books", createBook).Methods("POST")
       router.HandleFunc("/books/{id}", updateBook).Methods("PUT")
       router.HandleFunc("/books/{id}", deleteBook).Methods("DELETE")
       
       log.Println("Starting server on :8080")
       log.Fatal(http.ListenAndServe(":8080", router))
   }
   ```
   In the `main()` function, we set up the router and define the routes for each endpoint, using Gorilla Mux for cleaner route handling.

---

## Contributing

Feel free to submit issues or pull requests to enhance this project.
