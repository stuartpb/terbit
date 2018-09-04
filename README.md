# terbit

A Turing tarpit VM with a three-bit instruction set

Terbit is basically a generalization of [Brainfuck](https://en.wikipedia.org/wiki/Brainfuck), which was itself essentially an implementation of [P''](https://en.wikipedia.org/wiki/P%E2%80%B2%E2%80%B2).

## Operating Environment

Terbit defines an abstract array of signed integers with no width (though Head Cell and User Value operations may be specified through out-of-spec configuration to operate on integers as if they were a certain width, for wraparound and block purposes respectively).

## The Instructions

| oct | bi  | abr | bf  |
|-----|-----|-----|-----|
|   0 | 000 | HCA | `+` |
|   1 | 001 | HCS | `-` |
|   2 | 010 | HPA | `>` |
|   3 | 011 | HPS | `<` |
|   4 | 100 | ZLB | `[` |
|   5 | 101 | ZLT | `]` |
|   6 | 110 | UVI | `.` |
|   7 | 111 | UVO | `,` |

Implementations may interpret these instructions as a sort of RISC architecture, where higher-level "instructions" are derived from certain patterns of base instructions (such as ZLB HCS ZLT effectively forming a "set to zero" instruction, when cell values are fixed width or all positive).

Each instruction described below will also include other suggested names for the instruction (on its own or repeated), using other words that can represent it in [alphabinary](https://alpha.bi/).

### Instruction 0: Head Cell Addition

Increments the value of the current cell by 1.

Suggested synonyms: `add`, `big add`, `big big add`

### Instruction 1: Head Cell Subtraction

Decrements the value of the current cell by 1.

Suggested synonyms: `dip`, `far dip`, `far far dip`

### Instruction 2: Head Pointer Addition

Moves the Head one Cell to the right.

Suggested synonyms: `jog`, `jog jog`, `jog and jog`, `jog and end jog`, `jog and jog and jog`, `jog and jog and end jog`

### Instruction 3: Head Pointer Subtraction

Moves the Head one Cell to the left.

Suggested synonyms: `hop`, `hop hop`, `hop for hop`, `hop for its hop`, `hop for hop for hop`, `hop for hop for its hop`

### Instruction 4: Zero Loop Begin

If the current Head Cell value is nonzero, adds a new stack frame for a loop, which will be jumped to at the next ZLT instruction if the Head Cell value is nonzero.

If the current Head Cell value is zero, ignores all instructions to advance to the end of the next ZLT instruction.

Suggested alphabinary verb: `rig`

### Instruction 5: Zero Loop Terminate

If the current Head Cell value is nonzero, jumps to the last ZLB on the stack.

If the current Head Cell value is zero, pops the loop frame established by the last ZLB instruction off of the stack.

Suggested alphabinary verb: `rep`

### Instruction 6: User Value Input

Reads a value from the operating environment into the Head Cell.

Suggested alphabinary verb: `use`, `rub rub`

### Instruction 7: User Value Output

Writes the value of the current Head Cell to the operating environment.

Suggested alphabinary verb: `put`, `put out`, `put out put`
