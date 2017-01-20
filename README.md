# SwiftActiveResource
[ActiveResource for Swift] Transparently read/write resources over network.

UNDER CONSTRUCT

# Usage

```swift
struct Book: ActiveResource, JSONResource, Decodable {
    var site: String {
        return "https://localhost:3030/"
    }
    
    var id: String?
    var title: String
    var author: String
    
    override static func decode(_ e: Extractor) throws -> Book {
        return Book(
            id: e <|? "id",
            title: e <| "title",
            author: e <| "author" 
        )
    }
}

let book: Book = Book.find(1) // => GET https://localhost:3030/books/1 then serialize it into Book.
let books: [Book] = Book.all // => GET https://localhost:3030/books then serialize them into [Book].

book.title = "Alice in Wonderland"
book.save() // => PUT https://localhost:3030/books/1

let newBook = Book(title: "Harry Potter", author: "J.K. Rolling")
newBook.save() // => POST https://localhost:3030/books
```
