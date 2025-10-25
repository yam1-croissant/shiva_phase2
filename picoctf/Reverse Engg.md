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
## Flag: picoCTF{0000715}
In this CTF, we are given an ARM assembly file, and we are expected to decode the information using the chall.S file.

## Steps / understanding - 

1.sp+12 ---- has arg w0 stored (input)
2. w0 = 85
3. now this w0 is stored at sp+16
4. w0 = 6 stored at sp+20
5. w0 = 3 
6. now w0 is stored at sp+24
7. loads w0 = 6 ( sp+20) and loads w1 = 85(sp+16)
8. lsl ( logical shift left) w0,w1,w0  meaning w0 = 85 << 6 
 this leads to 5440
9. store this value of w0 at sp+28 (w0 = 5184)
10. load w1 = 5440 and load w0 = 3 ( sp+24) 
11. sdiv w0,w1,w0 means w0 = 5440 / 3 
as it is signed integer div we get an integer instead of decimal and we move forward
12. w0 = 1813 , stored at sp+28
13. load w1 = 1813 and load w0 =(input) 
14. sub w0,w1,w0 w0 = 1813 - input
15. this value is saved at sp+28


IF the function w0 = 0 only then will it print WIN so for it to print win, 
w0 = 0 = 1813 - input, so input must be 1813, where hex of 1813 is 715
<img width="592" height="992" alt="image" src="https://github.com/user-attachments/assets/4fc7a1fb-6c95-4802-879c-3922098d858b" />

 
# Vault door 3
## Flag: picoCTF{jU5t_a_s1mpl3_an4gr4m_4_u_c79a21}
In this CTF, we need to use the already given critria for password, to crack it

## Steps / Understanding - 

After looking at the code, i rewrote the script and ran it online.

<img width="1489" height="899" alt="image" src="https://github.com/user-attachments/assets/e5e20d57-4da3-46a2-a47e-afbabb2bfa79" />


