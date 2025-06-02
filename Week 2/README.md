

# ✅ Week 2: Parsing & Abstract Syntax Trees
---
## ✅ Goals for Week 2
1. **Understand context-free grammars** and parsing techniques.
2. **Implement recursive descent parser** for C-- grammar.
3. **Build Abstract Syntax Trees (ASTs)** during parsing.
4. **Handle syntax errors** gracefully with recovery.
---
## 🛠️ Task Breakdown
### 1. Learn Parsing Theory
Understand how parsers convert tokens into structured representations:
- Context-free grammars and BNF notation
- Recursive descent parsing technique
- Parse trees vs Abstract Syntax Trees
- Error recovery strategies
### 📖 Parsing Fundamentals
- [Crafting Interpreters – Parsing Expressions](https://craftinginterpreters.com/parsing-expressions.html)
- [Recursive Descent Parsing – YouTube](https://www.youtube.com/watch?v=SToUyjAsaFk)
- [Context-Free Grammars Explained](https://www.geeksforgeeks.org/classification-of-context-free-grammars/)
---
### 2. Design C-- Grammar
Define the formal grammar for C-- in BNF notation:
```bnf
program        → declaration-list
declaration    → var-declaration | fun-declaration
var-declaration → type-specifier ID ';' | type-specifier ID '[' NUM ']' ';'
fun-declaration → type-specifier ID '(' params ')' compound-stmt
type-specifier → 'int' | 'void'
compound-stmt  → '{' local-declarations statement-list '}'
statement      → expression-stmt | compound-stmt | selection-stmt | 
                 iteration-stmt | return-stmt
expression     → var '=' expression | simple-expression
simple-expression → additive-expression relop additive-expression
factor         → '(' expression ')' | var | call | NUM
```
### 3. Implement AST Node Classes
Create a hierarchy of AST node classes:
- **Base class**: `ASTNode` with virtual methods
- **Declaration nodes**: `VarDeclaration`, `FunDeclaration`, `Parameter`
- **Statement nodes**: `CompoundStmt`, `IfStmt`, `WhileStmt`, `ReturnStmt`
- **Expression nodes**: `BinaryOp`, `UnaryOp`, `Variable`, `Call`, `Number`

**Key Methods:**
```cpp
class ASTNode {
public:
    virtual ~ASTNode() = default;
    virtual void print(int indent = 0) const = 0;
    virtual void accept(Visitor& visitor) = 0;
};
```
### 🌳 AST Design Patterns
- [Abstract Syntax Trees Explained](https://ruslanspivak.com/lsbasi-part7/)
- [Visitor Pattern for ASTs](https://en.wikipedia.org/wiki/Visitor_pattern)

🧪 **Testing**
- Parse various C-- programs successfully
- Verify AST structure with tree visualization
- Test error recovery with malformed input
---
### 4. Recursive Descent Parser Implementation
Implement parser class with methods for each grammar rule:
```cpp
class Parser {
    vector<Token> tokens;
    int current;
    
public:
    unique_ptr<ASTNode> parse_program();
    unique_ptr<ASTNode> parse_declaration();
    unique_ptr<ASTNode> parse_expression();
    unique_ptr<ASTNode> parse_statement();
    // ... other parsing methods
    
    void error_recovery();
    void synchronize();
};
```
### 5. 🎯 Your First Parse Tree
Create a program that:
- Takes tokenized C-- code as input
- Parses it into an AST
- Pretty-prints the AST structure
- Shows syntax error messages with location information

---
