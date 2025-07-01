# 🎯 Week 5: Code Generation & Assembly
---
## ✅ Goals for Week 5
1. **Implement target code generation** (x86-64 assembly).
2. **Handle register allocation** and memory management.
3. **Generate executable assembly code**.
4. **Implement runtime support** for C-- programs.

---
## 🛠️ Task Breakdown

### 1. Learn Assembly Generation
Understand target architecture:
- x86-64 instruction set basics
- Calling conventions and stack management
- Register allocation strategies
- Memory addressing modes

### 📖 Assembly Generation Resources
- [x86-64 Assembly Tutorial](https://cs.brown.edu/courses/cs033/docs/guides/x64_cheatsheet.pdf)
- [System V ABI](https://wiki.osdev.org/System_V_ABI)
- [Register Allocation Algorithms](https://www.cs.cmu.edu/~fp/courses/15411-f13/lectures/09-regalloc.pdf)

---
### 2. Design Assembly Generator
Create code generator for x86-64:
```cpp
class AssemblyGenerator {
    map<string, string> register_map;
    vector<string> available_registers;
    int stack_offset;
    ofstream output_file;
    
public:
    void generate_from_ir(const vector<IRInstruction>& instructions);
    void emit_instruction(const string& instr);
    void emit_function_prologue(const string& func_name);
    void emit_function_epilogue();
    
    string allocate_register(const string& temp);
    void free_register(const string& reg);
    string get_memory_location(const string& var);
};
```

### 3. Register Allocation Implementation
Implement simple register allocation:
```cpp
class RegisterAllocator {
    map<string, string> temp_to_register;
    set<string> used_registers;
    vector<string> register_pool = {"rax", "rbx", "rcx", "rdx", "rsi", "rdi"};
    
public:
    string allocate_register(const string& temp);
    void free_register(const string& temp);
    void spill_to_memory(const string& temp);
    void load_from_memory(const string& temp);
};
```

### 4. Runtime System Implementation
Create minimal runtime support:
```cpp
// Runtime functions for C-- programs
class RuntimeGenerator {
public:
    void generate_startup_code();
    void generate_io_functions();
    void generate_memory_management();
    void generate_error_handling();
};
```

### 5. Assembly Code Templates
Create templates for common patterns:
- **Function calls**: Parameter passing, stack management
- **Array access**: Address calculation and bounds checking
- **Control flow**: Conditional jumps and loops
- **System calls**: I/O operations

### 🧪 **Testing**
- Generate assembly for simple C-- programs
- Test register allocation effectiveness
- Verify assembly correctness with assembler
- Run generated programs and validate output

---

