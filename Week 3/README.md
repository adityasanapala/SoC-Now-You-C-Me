# 🔍 Week 3: Semantic Analysis & Symbol Tables
---
## ✅ Goals for Week 3
1. **Build symbol table management** for variable and function declarations.
2. **Implement semantic analysis** with type checking and scope resolution.
3. **Perform static analysis** to catch semantic errors.
4. **Add semantic annotations** to the AST.

---
## 🛠️ Task Breakdown

### 1. Learn Semantic Analysis Theory
Understand how compilers analyze program meaning:
- Symbol tables and scope management
- Type systems and type checking
- Semantic error detection
- Attribute grammars and semantic actions

### 📖 Semantic Analysis Fundamentals
- [Crafting Interpreters – Resolving and Binding](https://craftinginterpreters.com/resolving-and-binding.html)
- [Symbol Tables in Compilers](https://www.geeksforgeeks.org/symbol-table-compiler/)
- [Type Checking in Compilers](https://cs.brown.edu/courses/cs126/2019/static.html)

---
### 2. Design Symbol Table Architecture
Create a hierarchical symbol table system:
```cpp
class Symbol {
public:
    string name;
    SymbolType type;
    int scope_level;
    SourceLocation location;
    
    virtual ~Symbol() = default;
};

class VariableSymbol : public Symbol {
public:
    DataType data_type;
    bool is_array;
    int array_size;
    bool is_parameter;
};

class FunctionSymbol : public Symbol {
public:
    DataType return_type;
    vector<unique_ptr<VariableSymbol>> parameters;
    bool is_defined;
};

class SymbolTable {
    unordered_map<string, unique_ptr<Symbol>> symbols;
    SymbolTable* parent;
    vector<unique_ptr<SymbolTable>> children;
    
public:
    void enter_scope();
    void exit_scope();
    bool declare_symbol(unique_ptr<Symbol> symbol);
    Symbol* lookup_symbol(const string& name);
    Symbol* lookup_current_scope(const string& name);
};
```

### 3. Implement Semantic Analyzer
Create a semantic analyzer using the Visitor pattern:
```cpp
class SemanticAnalyzer : public ASTVisitor {
    SymbolTable symbol_table;
    vector<string> errors;
    FunctionSymbol* current_function;
    
public:
    void visit(Program& node) override;
    void visit(VarDeclaration& node) override;
    void visit(FunDeclaration& node) override;
    void visit(BinaryOp& node) override;
    void visit(Call& node) override;
    void visit(Variable& node) override;
    
    void check_type_compatibility(DataType expected, DataType actual);
    void check_array_bounds(Variable& var);
    void check_function_call(Call& call);
    void check_return_statement(ReturnStmt& stmt);
    
    vector<string> get_errors() const { return errors; }
};
```

### 4. Type System Implementation
Add comprehensive type checking:
- **Variable type checking**: Ensure assignments are type-compatible
- **Function signature verification**: Check parameter types and counts
- **Array bounds checking**: Validate array access expressions
- **Return type validation**: Ensure functions return correct types

### 5. Error Reporting Enhancement
Improve error messages with context:
```cpp
class SemanticError {
public:
    string message;
    SourceLocation location;
    ErrorType type;
    
    string format_error() const;
};
```

### 🧪 **Testing**
- Validate symbol table construction for nested scopes
- Test type checking with valid and invalid programs
- Verify error reporting accuracy and clarity
- Check function call validation

---

