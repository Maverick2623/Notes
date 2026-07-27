## Code Compilation Guidelines 
1. For C -> `cl.exe /W4 /Zi main.c`

2. For C++ -> `cl.exe /W4 /Zi /EHsc main.cpp`

3. For creating a asm file for analysis can be done using `/FAs` flag

# What is `cl.exe` and `link.exe`?

- CL is a compiler which reads the c/c++ file and creates .obj file
- Link.exe is a linker which reads one or more .obj files, and any .lib files, finds the references and produces a .exe, .dll or .lib file

## MSVC 
- Runs the both in sequence when cl.exe is invoked

To Execute in separate steps 
```
cl.exe /c main.c
link.exe main.obj
```

Compiling with multiple source files 
```
cl.exe main.c utils.c 
```

Linking against Windows Libraries
```
cl.exe main.c /link user32.lib
# for messageBoxA 
```
Exception Handling Model 
```
# CPP Only 
cl.exe /EHsc main.c /link user32.lib
```


Reference: https://learn.microsoft.com/en-us/windows/win32/api/winuser/nf-winuser-messageboxa#requirements

Use `/WX` in cl.exe to convert warnings to errors, this dose not let Compiler compile in case of any warnings
```
# for C 
cl.exe main.c /WX /W4 /Zi abc.c /link user32.lib

# For CPP 
cl.exe main.c /WX /W4 /Zi /EHsc abc.cpp /link user32.lib
```

### C/C++ Runtime Library (CRT)
`/MT` -> Multi Threaded Static  (copies code into our code) | Larger in size 
`/MD`-> Multi Threaded DLL (references external DLLs) | Smaller in Size 

