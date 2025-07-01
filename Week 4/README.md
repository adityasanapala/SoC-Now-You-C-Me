# 🔄 Week 4: Intermediate Code Generation
---
## ✅ Goals for Week 4
1. **Design intermediate representation (IR)** for the compiler.
2. **Implement code generation** from AST to IR.
3. **Perform basic optimizations** on the IR.
4. **Prepare for target code generation**.

---
## 🛠️ Task Breakdown

### 1. Learn Intermediate Code Theory
Understand IR design and generation:
- Three-address code representation
- Basic blocks and control flow graphs
- Temporary variable management
- Code generation patterns

### 📖 Intermediate Code Resources
- [Dragon Book – Intermediate Code Generation](https://www.amazon.com/Compilers-Principles-Techniques-Tools-2nd/dp/0321486811)
- [Three-Address Code Tutorial](https://www.geeksforgeeks.org/three-address-code-compiler/)
- [LLVM IR Tutorial](https://llvm.org/docs/tutorial/)

---
### 2. Design Three-Address Code IR
Create a simple but effective IR:
```cpp
enum class OpCode {
    ADD, SUB, MUL, DIV, MOD,
    EQ, NE, LT, LE, GT, GE,
    AND, OR, NOT,
    ASSIGN, COPY,
    GOTO, IF_FALSE, IF_TRUE,
    PARAM, CALL, RETURN,
    ARRAY_ACCESS, ARRAY_ASSIGN,
    LABEL, FUNCTION_BEGIN, FUNCTION_END
};

class IRInstruction {
public:
    OpCode op;
    string result;
    string arg1;
    string arg2;
    
    string to_string() const;
};

class IRGenerator : public ASTVisitor {
    vector<IRInstruction> instructions;
    int temp_counter;
    int label_counter;
    
public:
    string new_temp();
    string new_label();
    void emit(OpCode op, string result = "", string arg1 = "", string arg2 = "");
    
    void visit(BinaryOp& node) override;
    void visit(Call& node) override;
    void visit(IfStmt& node) override;
    void visit(WhileStmt& node) override;
};
```

### 3. Implement Code Generation Patterns
Create generation methods for each construct:
- **Expressions**: Convert to postfix with temporaries
- **Control flow**: Generate labels and conditional jumps
- **Function calls**: Handle parameter passing and return values
- **Arrays**: Generate address calculations

### 4. Basic Optimization Passes
Implement simple optimizations:
```cpp
class IROptimizer {
public:
    void constant_folding(vector<IRInstruction>& instructions);
    void dead_code_elimination(vector<IRInstruction>& instructions);
    void copy_propagation(vector<IRInstruction>& instructions);
    void algebraic_simplification(vector<IRInstruction>& instructions);
};
```

### 5. Control Flow Graph Construction
Build CFG for advanced analysis:
```cpp
class BasicBlock {
public:
    vector<IRInstruction> instructions;
    set<BasicBlock*> predecessors;
    set<BasicBlock*> successors;
    string label;
};

class ControlFlowGraph {
    vector<unique_ptr<BasicBlock>> blocks;
    BasicBlock* entry_block;
    
public:
    void build_from_ir(const vector<IRInstruction>& instructions);
    void print_graph() const;
};
```

### 🧪 **Testing**
- Generate IR for various C-- constructs
- Verify correctness of generated three-address code
- Test optimization passes
- Validate control flow graph construction

---

