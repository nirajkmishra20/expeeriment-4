# expeeriment-4
Library Management UI with Search, Add, and Remove Book Functionality
index.html

<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Library Management</title>
    <link rel="stylesheet" href="styles.css" />
    <!-- React + Babel + ReactDOM -->
    <script
      crossorigin
      src="https://unpkg.com/react@18/umd/react.development.js"
    ></script>
    <script
      crossorigin
      src="https://unpkg.com/react-dom@18/umd/react-dom.development.js"
    ></script>
    <script src="https://unpkg.com/babel-standalone@6/babel.min.js"></script>
  </head>
  <body>
    <div id="root"></div>
    <script type="text/babel" src="script.js"></script>
  </body>
</html>


style.css
.container {
  border: 2px solid #000;
  padding: 20px;
  width: 80%;
  margin: 30px auto;
  border-radius: 5px;
  font-family: Arial, sans-serif;
}

h2 {
  font-size: 22px;
  margin-bottom: 10px;
}

input {
  padding: 8px;
  margin: 5px;
  border: 1px solid #ccc;
  border-radius: 4px;
}

button {
  padding: 8px 12px;
  margin: 5px;
  border: 1px solid #888;
  border-radius: 4px;
  background-color: #f8f8f8;
  cursor: pointer;
}

button:hover {
  background-color: #ddd;
}

.book-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  border: 1px solid #ccc;
  border-radius: 5px;
  padding: 8px 12px;
  margin-top: 10px;
}

.book-item strong {
  font-weight: bold;
}


script.js

function LibraryManagement() {
  const [books, setBooks] = React.useState([
    { title: "1984", author: "George Orwell" },
    { title: "The Great Gatsby", author: "F. Scott Fitzgerald" },
    { title: "To Kill a Mockingbird", author: "Harper Lee" },
  ]);

  const [searchTerm, setSearchTerm] = React.useState("");
  const [newTitle, setNewTitle] = React.useState("");
  const [newAuthor, setNewAuthor] = React.useState("");

  // Add new book
  const addBook = () => {
    if (newTitle.trim() && newAuthor.trim()) {
      setBooks([...books, { title: newTitle, author: newAuthor }]);
      setNewTitle("");
      setNewAuthor("");
    }
  };

  // Remove a book
  const removeBook = (index) => {
    const updated = books.filter((_, i) => i !== index);
    setBooks(updated);
  };

  // Filtered book list
  const filteredBooks = books.filter(
    (book) =>
      book.title.toLowerCase().includes(searchTerm.toLowerCase()) ||
      book.author.toLowerCase().includes(searchTerm.toLowerCase())
  );

  return (
    <div className="container">
      <h2>Library Management</h2>
      <input
        type="text"
        placeholder="Search by title or author"
        value={searchTerm}
        onChange={(e) => setSearchTerm(e.target.value)}
      />
      <br />
      <input
        type="text"
        placeholder="New book title"
        value={newTitle}
        onChange={(e) => setNewTitle(e.target.value)}
      />
      <input
        type="text"
        placeholder="New book author"
        value={newAuthor}
        onChange={(e) => setNewAuthor(e.target.value)}
      />
      <button onClick={addBook}>Add Book</button>

      {filteredBooks.map((book, index) => (
        <div className="book-item" key={index}>
          <span>
            <strong>{book.title}</strong> by {book.author}
          </span>
          <button onClick={() => removeBook(index)}>Remove</button>
        </div>
      ))}
    </div>
  );
}

ReactDOM.createRoot(document.getElementById("root")).render(<LibraryManagement />);

