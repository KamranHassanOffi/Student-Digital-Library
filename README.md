# Student-Digital-Library


<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Student Digital Library</title>
  <link href="https://cdn.jsdelivr.net/npm/tailwindcss@2.2.19/dist/tailwind.min.css" rel="stylesheet">
  <style>
    .glow {
    box-shadow: 0 0 15px rgba(0, 255, 255, 0.6);
  }
  .glow-orange {
    box-shadow: 0 0 10px rgba(255, 100, 0, 0.6);
  }
  .fade-in {
    animation: fadeIn 0.5s ease-in-out;
  }
  @keyframes fadeIn {
    from { opacity: 0; transform: translateY(10px); }
    to { opacity: 1; transform: translateY(0); }
  }

  /* 💥 Here's the hover effect for book cards */
  .book-card {
    transition: transform 0.3s ease, box-shadow 0.3s ease;
  }
  .book-card:hover {
    transform: scale(1.05);
    box-shadow: 0 0 20px rgba(0, 255, 255, 0.8), 0 0 30px rgba(0, 255, 255, 0.3);
  }

    body {
      background-color: #0c0f2c;
      font-family: 'Segoe UI', sans-serif;
    }
    .glow {
      box-shadow: 0 0 15px rgba(0, 255, 255, 0.6);
    }
    .glow-orange {
      box-shadow: 0 0 10px rgba(255, 100, 0, 0.6);
    }
    .fade-in {
      animation: fadeIn 0.5s ease-in-out;
    }
    @keyframes fadeIn {
      from { opacity: 0; transform: translateY(10px); }
      to { opacity: 1; transform: translateY(0); }
    }
  </style>
</head>
<body class="text-white">

  
  <div class="p-6">
    <h1 class="text-center text-4xl font-bold mb-8 text-cyan-400 glow">📚 Student Digital Library</h1>

    <div class="flex justify-center mb-6">
      <input id="searchInput" type="text" placeholder="Search books..." class="w-1/2 p-3 rounded-full bg-transparent border-2 border-cyan-400 text-white placeholder-white focus:outline-none glow transition duration-300" />
    </div>
    <div class="flex justify-center space-x-4 mb-10 flex-wrap">
      <button class="filter-btn px-4 py-2 mb-2 rounded-full border border-orange-400 text-orange-400 glow-orange hover:bg-orange-400 hover:text-white transition duration-300" data-category="Fiction">Fiction</button>
      <button class="filter-btn px-4 py-2 mb-2 rounded-full border border-orange-400 text-orange-400 glow-orange hover:bg-orange-400 hover:text-white transition duration-300" data-category="Science">Science</button>
      <button class="filter-btn px-4 py-2 mb-2 rounded-full border border-orange-400 text-orange-400 glow-orange hover:bg-orange-400 hover:text-white transition duration-300" data-category="Philosophy">Philosophy</button>
      <button class="filter-btn px-4 py-2 mb-2 rounded-full border border-orange-400 text-orange-400 glow-orange hover:bg-orange-400 hover:text-white transition duration-300" data-category="Programming">Programming</button>
      <button class="filter-btn px-4 py-2 mb-2 rounded-full border border-orange-400 text-orange-400 glow-orange hover:bg-orange-400 hover:text-white transition duration-300" data-category="Math">Math</button>
      <button class="filter-btn px-4 py-2 mb-2 rounded-full border border-orange-400 text-orange-400 glow-orange hover:bg-orange-400 hover:text-white transition duration-300" data-category="Comics">Comics</button>
      <button id="resetBtn" class="px-4 py-2 mb-2 rounded-full border border-gray-500 text-gray-300 hover:bg-gray-600 hover:text-white transition duration-300">Reset</button>
    </div>
    <div id="bookGrid" class="grid grid-cols-1 md:grid-cols-3 gap-8 px-10">
      <!-- Book Cards -->
    </div>
  </div>

  <script>
    const books = [
    { title: "The Art of War", author: "Sun Tzu", category: "Philosophy", image: "https://covers.openlibrary.org/b/id/11172241-L.jpg", pdf: "https://www.gutenberg.org/cache/epub/132/pg132-images.html" },
  { title: "Frankenstein", author: "Mary Shelley", category: "Fiction", image: "https://covers.openlibrary.org/b/id/10432729-L.jpg", pdf: "https://www.gutenberg.org/cache/epub/84/pg84-images.html" },
  { title: "Pride and Prejudice", author: "Jane Austen", category: "Fiction", image: "https://covers.openlibrary.org/b/id/10532058-L.jpg", pdf: "https://www.gutenberg.org/cache/epub/1342/pg1342-images.html" },
  { title: "The Time Machine", author: "H.G. Wells", category: "Science", image: "https://covers.openlibrary.org/b/id/11057685-L.jpg", pdf: "https://www.gutenberg.org/cache/epub/35/pg35-images.html" },
  { title: "A Tale of Two Cities", author: "Charles Dickens", category: "Fiction", image: "https://covers.openlibrary.org/b/id/10608624-L.jpg", pdf: "https://www.gutenberg.org/cache/epub/98/pg98-images.html" },
  { title: "Dracula", author: "Bram Stoker", category: "Fiction", image: "https://covers.openlibrary.org/b/id/10522050-L.jpg", pdf: "https://www.gutenberg.org/cache/epub/345/pg345-images.html" },
  { title: "The Picture of Dorian Gray", author: "Oscar Wilde", category: "Philosophy", image: "https://covers.openlibrary.org/b/id/10437352-L.jpg", pdf: "https://www.gutenberg.org/cache/epub/174/pg174-images.html" },
  { title: "The War of the Worlds", author: "H.G. Wells", category: "Science", image: "https://covers.openlibrary.org/b/id/10846507-L.jpg", pdf: "https://www.gutenberg.org/cache/epub/36/pg36-images.html" },
  { title: "Moby Dick", author: "Herman Melville", category: "Fiction", image: "https://covers.openlibrary.org/b/id/10592288-L.jpg", pdf: "https://www.gutenberg.org/cache/epub/2701/pg2701-images.html" },
  { title: "On the Origin of Species", author: "Charles Darwin", category: "Science", image: "https://covers.openlibrary.org/b/id/10444778-L.jpg", pdf: "https://www.gutenberg.org/cache/epub/2009/pg2009-images.html" },

  { title: "Clean Code", author: "Robert C. Martin", category: "Programming", image: "https://covers.openlibrary.org/b/id/9646196-L.jpg", pdf: "https://github.com/ryanmcdermott/clean-code-javascript/blob/master/README.md" },
  { title: "You Don’t Know JS", author: "Kyle Simpson", category: "Programming", image: "https://covers.openlibrary.org/b/id/9301535-L.jpg", pdf: "https://github.com/getify/You-Dont-Know-JS/archive/refs/heads/master.zip" },
  { title: "Calculus Made Easy", author: "Silvanus P. Thompson", category: "Math", image: "https://covers.openlibrary.org/b/id/10533577-L.jpg", pdf: "https://www.gutenberg.org/cache/epub/33283/pg33283-images.html" },
  { title: "A Brief History of Time", author: "Stephen Hawking", category: "Science", image: "https://covers.openlibrary.org/b/id/8225636-L.jpg", pdf: "https://archive.org/details/briefhistoryofti0000hawk" },
  { title: "The Adventures of Sherlock Holmes", author: "Arthur Conan Doyle", category: "Fiction", image: "https://covers.openlibrary.org/b/id/10718666-L.jpg", pdf: "https://www.gutenberg.org/cache/epub/1661/pg1661-images.html" },
  { title: "Comic Book History of Comics", author: "Fred Van Lente", category: "Comics", image: "https://covers.openlibrary.org/b/id/10861947-L.jpg", pdf: "https://www.comixology.com/Comic-Book-History-of-Comics/comics-series/45912" },
  { title: "HTML and CSS", author: "Jon Duckett", category: "Programming", image: "https://covers.openlibrary.org/b/id/10530807-L.jpg", pdf: "https://www.pdfdrive.com/html-and-css-design-and-build-websites-d15724007.html" },
  { title: "Introduction to Algorithms", author: "Cormen et al.", category: "Programming", image: "https://covers.openlibrary.org/b/id/10594734-L.jpg", pdf: "https://drive.google.com/file/d/1eUtmRjoRHq8sZ_w4Hux9Hkxj6Qt2iM2m/view?usp=sharing" },
  { title: "The Elements of Style", author: "Strunk & White", category: "Philosophy", image: "https://covers.openlibrary.org/b/id/10584306-L.jpg", pdf: "https://www.gutenberg.org/cache/epub/37134/pg37134-images.html" },
  { title: "Flatland", author: "Edwin A. Abbott", category: "Math", image: "https://covers.openlibrary.org/b/id/10621600-L.jpg", pdf: "https://www.gutenberg.org/cache/epub/201/pg201-images.html" },

  { title: "Code Complete", author: "Steve McConnell", category: "Programming", image: "https://covers.openlibrary.org/b/id/8099256-L.jpg", pdf: "https://drive.google.com/file/d/1-hZnpGRgm-jhHJyOjSxh9m7z9l5z5ApP/view?usp=sharing" },
  { title: "Structure and Interpretation of Computer Programs", author: "Harold Abelson & Gerald Jay Sussman", category: "Programming", image: "https://covers.openlibrary.org/b/id/8231996-L.jpg", pdf: "https://mitpress.mit.edu/sites/default/files/sicp/full-text/book/book.html" },
  { title: "Introduction to the Theory of Computation", author: "Michael Sipser", category: "Computer Science", image: "https://covers.openlibrary.org/b/id/8231997-L.jpg", pdf: "https://www.pdfdrive.com/introduction-to-the-theory-of-computation-d29897741.html" },
  { title: "The Pragmatic Programmer", author: "Andrew Hunt & David Thomas", category: "Programming", image: "https://covers.openlibrary.org/b/id/8231998-L.jpg", pdf: "https://www.pdfdrive.com/the-pragmatic-programmer-d20608127.html" },
  { title: "Design Patterns: Elements of Reusable Object-Oriented Software", author: "Erich Gamma et al.", category: "Programming", image: "https://covers.openlibrary.org/b/id/8231999-L.jpg", pdf: "https://www.pdfdrive.com/design-patterns-elements-of-reusable-object-oriented-software-d20741295.html" },
  { title: "Artificial Intelligence: A Modern Approach", author: "Stuart Russell & Peter Norvig", category: "Computer Science", image: "https://covers.openlibrary.org/b/id/8232000-L.jpg", pdf: "https://drive.google.com/file/d/1lh-fhgH2eHqZXKnKbY_EnMmaFE7JTO01/view?usp=sharing" },
  { title: "Operating System Concepts", author: "Abraham Silberschatz et al.", category: "Computer Science", image: "https://covers.openlibrary.org/b/id/8232001-L.jpg", pdf: "https://www.pdfdrive.com/operating-system-concepts-d18481838.html" },
  { title: "Computer Networks", author: "Andrew S. Tanenbaum", category: "Computer Science", image: "https://covers.openlibrary.org/b/id/8232002-L.jpg", pdf: "https://drive.google.com/file/d/1VhFL3jRupFLDb4ES4HwnFS58sJwQwY9v/view?usp=sharing" },

  { title: "Modern Operating Systems", author: "Andrew S. Tanenbaum", category: "Computer Science", image: "https://covers.openlibrary.org/b/id/8232003-L.jpg", pdf: "https://www.pdfdrive.com/modern-operating-systems-d19138138.html" },
  { title: "Compilers: Principles, Techniques, and Tools", author: "Alfred V. Aho et al.", category: "Computer Science", image: "https://covers.openlibrary.org/b/id/8232004-L.jpg", pdf: "https://www.pdfdrive.com/compilers-principles-techniques-and-tools-d19062555.html" },
  { title: "Introduction to Algorithms", author: "Thomas H. Cormen et al.", category: "Computer Science", image: "https://covers.openlibrary.org/b/id/8232005-L.jpg", pdf: "https://drive.google.com/file/d/1Ewv5dcFqN9bGPOgg_zAKF4iK2waXfjdF/view?usp=sharing" },
  { title: "The C Programming Language", author: "Brian W. Kernighan & Dennis M. Ritchie", category: "Programming", image: "https://covers.openlibrary.org/b/id/8232006-L.jpg", pdf: "https://www.pdfdrive.com/the-c-programming-language-d18661529.html" },
  { title: "Effective Java", author: "Joshua Bloch", category: "Programming", image: "https://covers.openlibrary.org/b/id/8232007-L.jpg", pdf: "https://www.pdfdrive.com/effective-java-d18516384.html" },
  { title: "Clean Architecture", author: "Robert C. Martin", category: "Programming", image: "https://covers.openlibrary.org/b/id/8232008-L.jpg", pdf: "https://github.com/ryanmcdermott/clean-code-javascript/blob/master/README.md" },
  { title: "Refactoring: Improving the Design of Existing Code", author: "Martin Fowler", category: "Programming", image: "https://covers.openlibrary.org/b/id/8232009-L.jpg", pdf: "https://www.pdfdrive.com/refactoring-improving-the-design-of-existing-code-d18372322.html" },
  { title: "Domain-Driven Design", author: "Eric Evans", category: "Programming", image: "https://covers.openlibrary.org/b/id/8232010-L.jpg", pdf: "https://www.pdfdrive.com/domain-driven-design-d18370656.html" },
  { title: "The Mythical Man-Month", author: "Frederick P. Brooks", category: "Programming", image: "https://covers.openlibrary.org/b/id/8232011-L.jpg", pdf: "https://www.pdfdrive.com/the-mythical-man-month-d18368743.html" },
  { title: "Design Patterns in Java", author: "Steven John Metsker", category: "Programming", image: "https://covers.openlibrary.org/b/id/8232012-L.jpg", pdf: "https://www.pdfdrive.com/design-patterns-in-java-d18510496.html" }
      
    ];

    document.addEventListener('DOMContentLoaded', () => {
      const bookGrid = document.getElementById('bookGrid');
      books.forEach(book => {
        const card = document.createElement('div');
        card.className = `book-card fade-in p-4 bg-gradient-to-b from-cyan-900 to-cyan-700 rounded-2xl glow`;
        card.setAttribute('data-category', book.category);
        card.setAttribute('data-title', book.title);
        card.innerHTML = `
          <img src="${book.image}" onerror="this.src='https://via.placeholder.com/150x220?text=No+Image'" class="mx-auto mb-4 rounded" alt="${book.title}">
          <p class="text-center font-bold mb-2">${book.title}</p>
          <p class="text-center text-sm text-gray-300 mb-4">${book.author}</p>
          <a href="${book.pdf}" target="_blank" class="block mx-auto bg-cyan-500 px-4 py-2 rounded-full text-white hover:bg-cyan-600 transition text-center">READ / DOWNLOAD</a>
        `;
        bookGrid.appendChild(card);
      });
    });
  </script>

  <script>
    const filterButtons = document.querySelectorAll('.filter-btn');
    const searchInput = document.getElementById('searchInput');
    const resetBtn = document.getElementById('resetBtn');

    filterButtons.forEach(button => {
      button.addEventListener('click', () => {
        const category = button.getAttribute('data-category');
        document.querySelectorAll('.book-card').forEach(card => {
          card.style.display = card.getAttribute('data-category') === category ? 'block' : 'none';
        });
      });
    });

    searchInput.addEventListener('input', () => {
      const term = searchInput.value.toLowerCase();
      document.querySelectorAll('.book-card').forEach(card => {
        const title = card.getAttribute('data-title').toLowerCase();
        card.style.display = title.includes(term) ? 'block' : 'none';
      });
    });

    resetBtn.addEventListener('click', () => {
      searchInput.value = '';
      document.querySelectorAll('.book-card').forEach(card => card.style.display = 'block');
    });
  </script>
</body>
</html>
