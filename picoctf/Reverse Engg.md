# GDB baby step1 
## Flag: pico{549698}
In this CTF, we were given a ELF 64-bit executable file, with the flag ( a decimal) written as a hex code, the flag was hidden in a eax registry.

## Steps -

```
strings /home/yam1/Downloads/debugger0_a | less 
```
Did not get any useful information so i used ghidra. 
<img width="1920" height="1080" alt="ss1" src="https://github.com/user-attachments/assets/f81147ae-8633-445a-9f64-aee2fec9a32b" />
we can see the hexcode here 0x86342, this is the flag.


# ARMssembly 1
# Vault door 3
