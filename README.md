# Windbg-Guide


-  ### How to get a structure Size?
    -  `?? sizeof` exp: get the _teb structure size `?? sizeof(ntdll!_teb)`
    
-  ### How to get PE mitigation like ASLR , ....?
    -  Need to check `_IMAGE_DOS_HEADER` > `_IMAGE_NT_HEADERS` > `_IMAGE_OPTIONAL_HEADER` > `DllCharacteristics`
    For example we want check sample.exe : `lm m sample.exe` > in result select `start`. for example it's `1000000` .So `dt ntdll!_IMAGE_DOS_HEADER 100000`. 
    In result select `e_lfanew` value. But use `?` command to convert hexadecimal. For example `? 0n120` . result is `78`. now use this command :
    `dt ntdll!_IMAGE_NT_HEADERS 0x00100000+0x78` . in the result select `OptionalHeader` filed for example it is `18`. Now use this command : 
    `dt ntdll!_IMAGE_OPTIONAL_HEADER 0x00100000+0x78+0x18` Now we have `DllCharacteristics` value. For parse is use [this link](https://learn.microsoft.com/en-us/windows/win32/api/winnt/ns-winnt-image_optional_header32)


