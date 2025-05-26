
# ✅ Week 1: Lexical Analysis & Project Setup
---
## ✅ Goals for Week 1
1. **Understand compiler architecture**: Learn the compilation pipeline and phases.
2. **Implement a lexical analyzer (lexer)** for C-- tokens.
3. **Set up project structure** with proper build system and testing framework.
4. **Create your first tokenized output** from C-- source code.
---
## 🛠️ Task Breakdown
### 1. Learn Compiler Fundamentals
Understand how compilers work and the role of lexical analysis:
- What are tokens and why they're needed
- How lexical analysis fits in the compilation pipeline
- Understanding finite state machines for tokenization
### 📚 Compiler Theory Basics
- [Crafting Interpreters – Scanning Chapter](https://craftinginterpreters.com/scanning.html)
- [Compiler Design – Lexical Analysis (GeeksforGeeks)](https://www.geeksforgeeks.org/compiler-design-lexical-analysis/)
- [Introduction to Compilers – YouTube (UC Davis)](https://www.youtube.com/watch?v=54bo1qaHAfk)
---
### 2. Implement C-- Lexer
Create a C++ lexer class with the following:
- **Token types**: Keywords, identifiers, numbers, operators, delimiters
- **Token class**: `Token(TokenType type, string value, int line, int column)`
- **Lexer class methods**:
  - `tokenize(const string& source)`
  - `next_token()`
  - `peek_char()`
  - `skip_whitespace()`
  - `read_number()`
  - `read_identifier()`
  - `handle_comments()`

**C-- Tokens to Support:**
```cpp
// Keywords
int, void, if, else, while, return, input, output

// Operators  
+, -, *, /, =, ==, !=, <, <=, >, >=

// Delimiters
{, }, (, ), [, ], ;, ,

// Literals & Identifiers
integers, variable names, function names
```
### 🔤 Lexical Analysis Implementation
- [Lexical Analysis Tutorial](https://www.tutorialspoint.com/compiler_design/compiler_design_lexical_analysis.htm)
- [Building a Lexer in C++ – YouTube](https://www.youtube.com/watch?v=__-wUHG2rfM)

🧪 **Testing**
- Test with provided C-- sample programs
- Verify correct token identification and line/column tracking
---
### 3. Project Setup & Build System
Set up your project structure:
```
c-minus-compiler/
├── src/
│   ├── lexer.h
│   ├── lexer.cpp
│   └── main.cpp
├── tests/
│   ├── lexer_tests.cpp
│   └── sample_programs/
├── Makefile
└── README.md
```

Write a `Makefile` that supports:
- `make` - compile the project
- `make test` - run tests
- `make clean` - clean build files
### 🛠️ Build Systems
- [Makefile Tutorial](https://makefiletutorial.com/)
- [C++ Project Structure Best Practices](https://api.csswg.org/bikeshed/?force=1&url=https://raw.githubusercontent.com/vector-of-bool/pitchfork/develop/data/spec.bs)
---
### 4. 🎯 Your First Tokenization
Write a program that:
- Reads a C-- source file
- Tokenizes it using your lexer
- Outputs tokens in a readable format showing type, value, and position

**Example Output:**
```
Token: KEYWORD(int) at line 1, col 1
Token: IDENTIFIER(main) at line 1, col 5
Token: LPAREN(() at line 1, col 9
Token: KEYWORD(void) at line 1, col 10
Token: RPAREN()) at line 1, col 14
Token: LBRACE({) at line 1, col 16
...
```

