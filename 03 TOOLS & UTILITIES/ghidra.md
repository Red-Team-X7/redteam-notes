# 💢 ghidra
Tags: #💢
Related to: 
See also: 
Previous: [[Reverse Engineering]]

---
## Description

A software reverse engineering (SRE) suite of tools developed by NSA's Research Directorate in support of the Cybersecurity mission.

## Usage Examples

### Find password validation logic

Reverse Engineer binary to find credentials:

	sudo apt-get install ghidra

Run ghidra. Create a Project. Load SERVER.EXE. Run CodeBrowser.

	Window => Defined Strings => Filter: Password	// "Correct Password!"
	Click "Correct Password"						// shows corresponding function name in Listing Window.
	Symbol Tree => Browse to that function			// FUN_10476cb0
	Functions => F => FUN_104 => FUN_1047 => FUN_10476 => FUN_10476cb0
	Window => Decompile: FUN_10476cb0

We confirm that the function FUN_10476cb0 contains the password validation logic.
thunk_FUN_10484890 looks like a strcpy_s call, where it is copying the user input 2048 (0x800)
bytes in size to a destination buffer of only 1024 bytes in size.

```
void __cdecl FUN_10476cb0(char *param_1)

{
  int iVar1;
  char local_404 [1024];
  
  _strncpy_s(local_404,0x801,param_1,0x800);
  iVar1 = _strncmp(&DAT_104d79a0,s_P@$$worD_104d51a8,8);
  if (iVar1 == 0) {
    thunk_FUN_10476fd0(s_Correct_Password!_104d51b4);
  }
  else {
    thunk_FUN_10476fd0(s_Wrong_password!_104d51c8);
  }
  return;
}
```

This is a clear buffer overflow.

---
## References
- [[]]