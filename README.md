# compilecs
Use build-in compiler csc.exe and other tools to insert entrypoint in dll

If one don't want to use VS to compile C# and insert entrypoint in dll, grap a copy of ildasm.exe from SDK, remember to copy assemble DLL's to C:\compile or add then with /r

compile.bat:

del C:\compile\\%1.il

del C:\compile\\%1.res

del C:\compile\\%1.dll
C:\Windows\Microsoft.NET\Framework64\v4.0.30319\csc.exe /platform:anycpu /r:System.Management.Automation.dll /target:library /unsafe %1.cs

C:\compile\ildasm.exe /out:%1.il %1.dll

notepad.exe C:\\compile\\%1.il

C:\Windows\Microsoft.NET\Framework64\v4.0.30319\ilasm.exe %1.il /DLL /output=%1.dll

example: (the file is called magic.cs)

compile.bat magic

then notepad open magic.il file, insert .export [1], in this example the Main() become the entrypoint in the DLL




  .method private hidebysig static void  Main() cil managed
  
  {
  
  .export [1]
  
    // Code size       101 (0x65)
    .maxstack  6
    .locals init (uint8[] V_0,
    
    
    
 save file
 
 now one can call your C# DLL like this rundll32 magic.dll,Main
 
 
