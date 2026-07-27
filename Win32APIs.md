## Win32APIs/NTAPIs 
Posting here the I have used throughout the Course while solving labs and challenges, while learning C/C++ for malware development and evasions

This would help me track the pitfalls and issues i ran into, This would act as a knowlege base for me in the future

APIs
-----
### GetUserNameA
- Gets User Name in lpBuffer of Size nSize 
- lpBuffer should be char array of size[unlen+1]
- for 'unlen' we need to include Lmcons.h
- nSize can be set using sizeOf(lpBuffer)
- Reference: https://learn.microsoft.com/en-us/windows/win32/api/winbase/nf-winbase-getusernamea#syntax


### GetComputerNameA
- Gets Computer Name in lpBuffer of Size nSize 
- lpBuffer should be char array of size[256]
- nSize can be set using sizeOf(lpBuffer)
- Reference: https://learn.microsoft.com/en-us/windows/win32/api/winbase/nf-winbase-getcomputernamea#syntax


### LookupAccountNameA
- Accepts System Name and account name as input and retrieves the SID 
- in C we need to add a Struct for PSID_NAME_USE, CPP handles it automatically
- SID is of type byte array of size SECURITY_MAX_SID_SIZE  

### ConvertSidToStringSidA
- Takes the SID enum as an input an stores String SID in the output 
- Reference: https://learn.microsoft.com/en-us/windows/win32/api/sddl/nf-sddl-convertsidtostringsida

### WriteFile
- Writes data to a file 
- Reference: https://learn.microsoft.com/en-us/windows/win32/api/fileapi/nf-fileapi-writefile





















**Note:** This is form my reference, pull requests (if any) may or may not be accepted
