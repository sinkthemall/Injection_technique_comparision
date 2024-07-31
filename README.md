# Injection_technique_comparision
Comparision between various of injection techniques. List of injection techniques in this comparision was referenced from here: https://github.com/itaymigdal/awesome-injection?tab=readme-ov-file#section-mapping-injection

### Comparision

| **Injection tecnique**            | **Required Privilege** | **Stealth, detection rate**           | **methodology**                                                                                                                                                                                                 | **Persitence** | **implementation complexity**  | **impact**                                                 | **uses case, target** |
|-----------------------------------|------------------------|---------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------|--------------------------------|------------------------------------------------------------|-----------------------|
| process Injection                 |                        | Easy being spotted by EDR/AV          | Alloc mem (RWX) -> Copy shellcode -> Create new remote thread. Uses API: VirtualAllocEx, WriteProcessMemory, CreateRemoteThreadEx                                                                               |                | medium (base on the shellcode) | Target Process                                             |                       |
| DLL injection                     |                        |                                       | Load library -> Library execute DLLMain -> code execute Uses API:<br/> + LoadLibraryA, beside, there are VirtualAllocEx, WriteProcessMemory for loading dll path                                                |                | easy                           | Target Process                                             |                       |
| reflective DLL, PE injection      |                        | Less detention than Process injection | Copy DLL to target memory -> DLL contain reflective loader -> Re-control flow to reflective loader -> Loader parsing DLL, then execute DLLMain Uses API: VirtualAllocEx, WriteProcessMemory, CreateRemoteThread |                | hard                           | Target Process                                             |                       |
| DLL injection via SetWindowHookEx |                        |                                       | Inject Hook function to Window Procedure Message Handling chain -> trigger when required window message is met. Uses API: SetWindowsHookEx, Loadlibrary (to load dll)                                           |                | medium                         | Depend on arg in Setwindowshook Sometimes it can be global |                       |
| Section Mapping                   |                        |                                       | Section is a shared memory between process. Mapping section between processes and create thread to control flow to mapped section. Uses API: CreateRemoteThread, NtMapViewOfSection                             |                | easy                           | Can be global, base on the number of process map to        |                       |