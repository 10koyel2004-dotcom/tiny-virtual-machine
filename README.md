# Tiny Virtual Machine for Intermediate Code Execution

## Project Title

Tiny Virtual Machine for Intermediate Code Execution

## Objective

This project implements a stack-based virtual machine that executes a small intermediate-code language. It demonstrates an important Compiler Design concept: source-level operations can be converted into intermediate instructions and executed by a target virtual machine.

## Compiler Design Connection

A compiler commonly has these stages:

Source Program
→ Lexical Analysis
→ Syntax Analysis
→ Semantic Analysis
→ Intermediate Code Generation
→ Code Generation

This project focuses on the execution of intermediate code.

The `.tvm` file represents intermediate code. The parser reads the code, and the Tiny Virtual Machine executes each instruction using the fetch-decode-execute cycle.

## Architecture

`.tvm Program File`
→ `Parser`
→ `Instruction List and Label Table`
→ `Tiny Virtual Machine`
→ `Stack, Memory, Program Counter`
→ `Output`

## Main Components

### 1. Parser

The parser reads the `.tvm` input file.

It:
- Removes comments.
- Identifies labels.
- Creates instruction objects.
- Validates opcode names.
- Creates a label-to-address table.

### 2. Virtual Machine

The Tiny Virtual Machine contains:

- Program Counter (PC): Stores the address of the current instruction.
- Stack: Stores operands and intermediate arithmetic results.
- Memory: Stores variable names and values.
- Label Table: Stores label names with their instruction positions.
- Execution Loop: Fetches, decodes, and executes instructions.

### 3. Fetch-Decode-Execute Cycle

1. Fetch the instruction using the Program Counter.
2. Decode the opcode and operand.
3. Execute the operation.
4. Update the stack, memory, or Program Counter.
5. Repeat until `HALT` is reached.

## Instruction Set

| Instruction | Description |
|---|---|
| `LOADI n` | Push integer `n` onto the stack |
| `LOAD x` | Push value of variable `x` onto the stack |
| `STORE x` | Pop stack value and save it in variable `x` |
| `ADD` | Pop two values, add them, push result |
| `SUB` | Pop two values, subtract second from first |
| `MUL` | Pop two values, multiply them |
| `DIV` | Pop two values, integer divide first by second |
| `MOD` | Pop two values, find remainder |
| `DUP` | Duplicate the top stack value |
| `POP` | Remove the top stack value |
| `EQ` | Push `1` if values are equal, otherwise push `0` |
| `LT` | Push `1` if first value is less than second value |
| `GT` | Push `1` if first value is greater than second value |
| `JMP label` | Unconditionally jump to a label |
| `JZ label` | Jump to label if popped condition is zero |
| `PRINT` | Pop and display stack value |
| `HALT` | Stop program execution |

## Folder Structure

```text
tiny-virtual-machine/
├── main.py
├── vm.py
├── parser.py
├── instructions.py
├── README.md
└── programs/
    ├── addition.tvm
    ├── factorial.tvm
    └── loop_demo.tvm
```

## How to Run

Open the project folder in VS Code.

Run the addition program:

```bash
python main.py programs/addition.tvm
```

Run the factorial program with execution trace:

```bash
python main.py programs/factorial.tvm --trace
```

Show parsed code, labels, and trace:

```bash
python main.py programs/factorial.tvm --show-code --trace
```

## Sample Output

For the factorial program:

```text
OUTPUT: 120
```

## Error Handling

The VM handles:
- Invalid instruction names.
- Missing operands.
- Missing labels.
- Duplicate labels.
- Stack underflow.
- Undefined variables.
- Division by zero.
- Program counter errors.

## Future Enhancements

- Add a graphical user interface.
- Add function call and return instructions.
- Add arrays.
- Add a register-based VM version.
- Create a simple compiler that converts arithmetic expressions into `.tvm` code.
- Add breakpoints and step-by-step debugging.