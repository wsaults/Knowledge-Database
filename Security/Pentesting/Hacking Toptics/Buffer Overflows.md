# Buffer Overflows.md

> Icetray anology

## Concepts

- Boundary checks
- Strcpy()
- Programming vulnerabilities
- Ignorant programmers
- Understand stacks (LIFO, FIFO)
- HEAP's dynamic Mem malloc()
- Push / Pop (Extended Information Pointer, Extended Base Pointer, Extended Stack Pointer) next instruction set when processing the code
- Shellcode
- Null operator (No-op, NOOP)

## Tools

- Ollydbg
- IDAPro
- Heap.exe

## Countermeasures

- Manually audit code
- Use good compilers
- Safe library support
- Disabling stack execution
- Use runtime checking
- Design with secruity in mind
- Stack guards (prevents buffer overflow)
- Restrict gets, strcpy(), etc...
- Data execution prevention (DEP)