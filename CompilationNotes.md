# Code Compilation Guidelines 
1. For C -> `cl.exe /W4 /Zi main.c`

2. For C++ -> `cl.exe /W4 /Zi /EHsc main.cpp`

3. For creating a asm file for analysis can be done using `/FAs` flag

## What is `cl.exe` and `link.exe`?

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

`/MD`-> Multi Threaded DLL (references external DLLs) | Smaller in Size | If the required DLLs are not present in the target host, the execution fails  

**Note:** With the `/Zi`the sizes of default compilation and compilation with `/MT` flag has the samilar size, since `/Zi` include all the debugging data, it futher defaults to `/MTd`


Hexadecimal format specifiers for sscan_f 
```
if (sscanf_s(argv[2], "%hhx", &key) != 1) {
        printf("Error: Argument '%s' is not a valid hex byte.\n", argv[2]);
        return 1;
    }
```

| Variable Type | Bit Width | Format Specifier | Example Input |
| :--- | :--- | :--- | :--- |
| `unsigned char` | 8-bit (1 byte) | `%hhx` | `A4` |
| `unsigned short` | 16-bit (2 bytes) | `%hx` | `D3F1` |
| `unsigned int` | 32-bit (4 bytes) | `%x` | `A1B2C3D4` |
| `unsigned long long` | 64-bit (8 bytes) | `%llx` | `1A2B3C4D5E6F7G8H` |

```
DWORD flags = (DWORD)stroul(argv[1],NULL,16);
```
This function parses a string and converts it into an unsigned long integer.
- argv[1]: This is the first command-line argument passed to your program. It expects a string like "0x1A" or "F0".
- NULL: This parameter is optionally used to find where the valid number ends in the string. Passing NULL means you don't care to track where the parsing stopped.
- 16: This explicitly tells the function to parse the string as Base-16 (Hexadecimal).

`(DWORD)`
This is a typecast.In Windows development, a DWORD (Double Word) is a defined data type representing a 32-bit unsigned integer.Since strtoul returns an unsigned long (which can be 64-bit on some systems), (DWORD) explicitly forces/casts that value down into a standard Windows 32-bit integer format.

`DWORD flags = ...`
This creates a new 32-bit unsigned integer variable named flags and assigns the converted hexadecimal value to it. In low-level programming, "flags" usually represent individual bits that turn specific features, permissions, or options on or off (e.g., 0x00000001 might mean "Read-Only", 0x00000002 might mean "Hidden").


**Note:** This is form my reference, pull requests (if any) may or may not be accepted
