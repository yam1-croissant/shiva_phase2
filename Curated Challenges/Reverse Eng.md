# JoyDivision 
## Flag: sunshine{C3A5ER_CR055ED_TH3_RUB1C0N}

## Steps - 

Checked the contents of the file given flag.txt was a data dump so was 'disorder' file.

I used Ghidra to open disorder and then looked at the decomplined code 

```ruby
undefined8 main(void)

{
  byte bVar1;
  undefined1 *puVar2;
  void *__ptr;
  int iVar3;
  long lVar4;
  ulong uVar5;
  undefined8 uVar6;
  FILE *pFVar7;
  undefined1 *puVar8;
  long in_FS_OFFSET;
  undefined1 auStack_88 [8];
  int local_80;
  int local_7c;
  FILE *local_78;
  long local_70;
  undefined1 *local_68;
  undefined8 local_60;
  undefined8 local_58;
  void *local_50;
  FILE *local_48;
  long local_40;
  
  local_40 = *(long *)(in_FS_OFFSET + 0x28);
  puts(
      "\nMay Jupiter strike you down Caeser before you seize the treasury!! You will have to tear me  apart"
      );
  puts(
      "for me to tell you the flag to unlock the Roman Treasury and fund your civil war. I, Lucius C aecilius"
      );
  puts(
      "Metellus, shall not let you pass until you get this password right. (or threaten to kill me-) \n"
      );
  local_78 = fopen("palatinepackflag.txt","r");
  fseek(local_78,0,2);
  lVar4 = ftell(local_78);
  local_7c = (int)lVar4 + 1;
  fseek(local_78,0,0);
  local_70 = (long)local_7c + -1;
  uVar5 = (((long)local_7c + 0xfU) / 0x10) * 0x10;
  for (puVar8 = auStack_88; puVar8 != auStack_88 + -(uVar5 & 0xfffffffffffff000);
      puVar8 = puVar8 + -0x1000) {
    *(undefined8 *)(puVar8 + -8) = *(undefined8 *)(puVar8 + -8);
  }
  lVar4 = -(ulong)((uint)uVar5 & 0xfff);
  if ((uVar5 & 0xfff) != 0) {
    *(undefined8 *)(puVar8 + ((ulong)((uint)uVar5 & 0xfff) - 8) + lVar4) =
         *(undefined8 *)(puVar8 + ((ulong)((uint)uVar5 & 0xfff) - 8) + lVar4);
  }
  pFVar7 = local_78;
  iVar3 = local_7c;
  local_68 = puVar8 + lVar4;
  *(undefined8 *)(puVar8 + lVar4 + -8) = 0x101bfa;
  fgets(puVar8 + lVar4,iVar3,pFVar7);
  puVar2 = local_68;
  iVar3 = local_7c;
  *(undefined8 *)(puVar8 + lVar4 + -8) = 0x101c0b;
  flipBits(puVar2,iVar3);
  puVar2 = local_68;
  iVar3 = local_7c;
  *(undefined8 *)(puVar8 + lVar4 + -8) = 0x101c1c;
  uVar6 = expand(puVar2,iVar3);
  iVar3 = local_7c * 2;
  local_60 = uVar6;
  *(undefined8 *)(puVar8 + lVar4 + -8) = 0x101c34;
  uVar6 = expand(uVar6,iVar3);
  iVar3 = local_7c * 4;
  local_58 = uVar6;
  *(undefined8 *)(puVar8 + lVar4 + -8) = 0x101c50;
  local_50 = (void *)expand(uVar6,iVar3);
  *(undefined8 *)(puVar8 + lVar4 + -8) = 0x101c5e;
  anti_debug();
  for (local_80 = 0; local_80 < local_7c * 8; local_80 = local_80 + 1) {
    bVar1 = *(byte *)((long)local_50 + (long)local_80);
    *(undefined8 *)(puVar8 + lVar4 + -8) = 0x101c81;
    putchar((uint)bVar1);
  }
  *(undefined8 *)(puVar8 + lVar4 + -8) = 0x101c9a;
  putchar(10);
  *(undefined8 *)(puVar8 + lVar4 + -8) = 0x101cb3;
  pFVar7 = fopen("flag.txt","wb");
  __ptr = local_50;
  iVar3 = local_7c << 3;
  local_48 = pFVar7;
  *(undefined8 *)(puVar8 + lVar4 + -8) = 0x101cd5;
  fwrite(__ptr,1,(long)iVar3,pFVar7);
  pFVar7 = local_48;
  *(undefined8 *)(puVar8 + lVar4 + -8) = 0x101ce1;
  fclose(pFVar7);
  if (local_40 != *(long *)(in_FS_OFFSET + 0x28)) {
                    /* WARNING: Subroutine does not return */
    __stack_chk_fail();
  }
  return 0;
}
```

Here what's happening is, the contents of file called "palantinepackflag.txt" is being manipulated and is saved in a file "flag.txt" which we have access to.

Reading carefully, we understand that a function called 'flipbites' manipulates the bytes of the contents and function 'expand' basically, expands the size of the contents
from 1x--->2x--->4x---->8x. So if we have to retrieve the data, we first need to cut the size down, and then 'unflip' the contents. 

Reading the function 'expand' 

```
void * expand(long param_1,int param_2)

{
  bool bVar1;
  void *pvVar2;
  byte local_1d;
  int local_18;
  
  bVar1 = false;
  local_1d = 0x69;
  pvVar2 = malloc((long)(param_2 * 2)); ------1
  for (local_18 = 0; local_18 < param_2; local_18 = local_18 + 1) {
    if (bVar1) {
      *(byte *)((long)pvVar2 + (long)(local_18 * 2)) =
           *(byte *)(param_1 + local_18) & 0xf0 | local_1d >> 4;
      *(byte *)((long)pvVar2 + (long)(local_18 * 2) + 1) =
           *(byte *)(param_1 + local_18) & 0xf | local_1d << 4;
    }
    else {
      *(byte *)((long)pvVar2 + (long)(local_18 * 2)) =
           *(byte *)(param_1 + local_18) & 0xf | local_1d << 4;
      *(byte *)((long)pvVar2 + (long)(local_18 * 2) + 1) =
           *(byte *)(param_1 + local_18) & 0xf0 | local_1d >> 4;
    }
    local_1d = local_1d * '\v';
    bVar1 = !bVar1;
  }
  printf("fie");
  return pvVar2;
}
```

First it allocates a new buffer which is twice the size of input we can see at line 1.
Then it splits the bytes into two nibbles (hence expanding it). It then combines the keys in 
combination using a key which is generated every time it is expanded.

The dynamic key (local_1d) starts with 0x69, and then multiplied by 11 ( '\n'). 
The combination used bvar1, so swap order of the high and low nibble.

Similarly reading the function 'flipbits' -

```ruby
void flipBits(long param_1,int param_2)

{
  bool bVar1;
  undefined1 local_11;
  undefined4 local_c;
  
  bVar1 = false;
  local_11 = 0x69;
  for (local_c = 0; local_c < param_2; local_c = local_c + 1) {
    if (bVar1) {
      *(byte *)(param_1 + local_c) = *(byte *)(param_1 + local_c) ^ local_11;
      local_11 = local_11 + 0x20;
    }
    else {
      *(byte *)(param_1 + local_c) = ~*(byte *)(param_1 + local_c);
    }
    bVar1 = !bVar1;
  }
  return;
}
```

Here, param_1 is the data buffer, and param_2 is the size of the buffer and it undergoes alternate modification.
Odd Bytes - (bVar1 is false) it performs a bitwise NOT operation (inverts the binary)
Even Bytes - (bVar1 is true) it perfroms a XOR operation with a key (local_11) , the key changes after every XOR operation by 0x20

To get the flag we have to perform the opposite, first we unexpand it and then unflip. 

```ruby
import sys
import os # Added os for clarity

# --- 1. un_expand Function Definition ---
def un_expand(data_in):
    """Reverses one call of the expand function (2X size -> 1X size)."""
    size_in = len(data_in)
    size_out = size_in // 2
    
    if size_out == 0 and size_in != 0:
        # Handle case where size is odd (shouldn't happen with correct logic)
        raise ValueError("Input data size for un_expand is not an even number.")
    
    data_out = bytearray(size_out)
    bVar1 = False # Must match the original 'expand' initialization
    
    for i in range(size_out):
        A = data_in[i * 2]
        B = data_in[i * 2 + 1]

        original_high_nibble = 0
        original_low_nibble = 0

        if bVar1:
            # Reverses original Case 1: A = X_H | K_L, B = X_L | K_H
            original_high_nibble = A & 0xF0
            original_low_nibble  = B & 0x0F
        else:
            # Reverses original Case 2: A = X_L | K_H, B = X_H | K_L
            original_low_nibble  = A & 0x0F
            original_high_nibble = B & 0xF0
        
        data_out[i] = original_high_nibble | original_low_nibble
        
        bVar1 = not bVar1 

    return data_out


# --- 2. un_flip_bits Function Definition ---
def un_flip_bits(data_in):
    """Reverses the flipBits function (same logic as the original)."""
    size_in = len(data_in)
    data_out = bytearray(data_in) # Work on a copy of the final 1x data
    
    bVar1 = False # Must match the original 'flipBits' initialization
    local_11 = 0x69 # Initial XOR key
    
    for i in range(size_in):
        current_byte = data_out[i]
        
        if bVar1:
            # Corresponds to the 'if (bVar1)' branch: XOR with dynamic key
            current_byte = current_byte ^ local_11
            local_11 = (local_11 + 0x20) & 0xFF # Key updates
        else:
            # Corresponds to the 'else' branch: NOT operation
            current_byte = (~current_byte) & 0xFF
            
        data_out[i] = current_byte
        bVar1 = not bVar1
        
    return data_out


# --- 3. main Function Definition and Execution ---
def main():
    input_file = "flag.txt"
    output_file = "recovered_palatinepackflag.txt"
    
    try:
        with open(input_file, "rb") as f:
            data_8x = f.read()
    except FileNotFoundError:
        print(f"Error: {input_file} not found. Ensure it is in the same directory.")
        return

    print(f"--- Reversing Transformations on {len(data_8x)} bytes ---")

    # 1. Reverse Call 3: 8X -> 4X
    data_4x = un_expand(data_8x)
    print(f"1. un_expand (8X -> 4X) complete. Size: {len(data_4x)} bytes.")
    
    # 2. Reverse Call 2: 4X -> 2X
    data_2x = un_expand(data_4x)
    print(f"2. un_expand (4X -> 2X) complete. Size: {len(data_2x)} bytes.")

    # 3. Reverse Call 1: 2X -> 1X (Original size)
    data_1x = un_expand(data_2x)
    print(f"3. un_expand (2X -> 1X) complete. Size: {len(data_1x)} bytes.")
    
    # 4. Reverse the flipBits operation
    original_flag_bytes = un_flip_bits(data_1x)
    
    # Output Results
    print("\n--- Recovered palatinepackflag.txt Content ---")
    try:
        # Try decoding as standard text
        original_flag_text = original_flag_bytes.decode('ascii').strip()
        print(original_flag_text)
    except UnicodeDecodeError:
        # Fallback to printing raw bytes if it's non-text data
        print("Could not decode as ASCII text. Raw bytes follow:")
        print(original_flag_bytes)
        
    with open(output_file, "wb") as f:
        f.write(original_flag_bytes)
    
    print(f"\n[Success] Final result saved to {output_file}")


if __name__ == "__main__":
    main()
```

<img width="639" height="201" alt="image" src="https://github.com/user-attachments/assets/5126a320-044a-4606-954f-e100f295ff4d" />


# Worthy.knight 
## Flag: KCTF{NjkSfTYaIi}

## Steps - 

in this challenge we need to enter the right 10 characters and wrap it around KCTF{}. 

Using Ghidra , we can see the decomplied code at FUN_001010d0

```ruby
undefined4 FUN_001010d0(void)

{
  byte bVar1;
  ushort uVar2;
  ushort uVar3;
  int iVar4;
  char *pcVar5;
  size_t sVar6;
  ushort **ppuVar7;
  byte *pbVar8;
  undefined4 uVar9;
  char *pcVar10;
  long in_FS_OFFSET;
  ushort local_10c;
  undefined1 local_10a;
  byte local_108 [16];
  char local_f8 [32];
  char local_d8 [16];
  undefined1 local_c8 [16];
  undefined1 local_b8 [16];
  undefined1 local_a8 [16];
  undefined1 local_98 [16];
  undefined1 local_88 [16];
  undefined1 local_78 [16];
  undefined1 local_68 [16];
  undefined1 local_58 [16];
  long local_40;
  
  local_40 = *(long *)(in_FS_OFFSET + 0x28);
  puts(
      "                       (Knight\'s Adventure)                \n\n         O                                              \n        <M>            .---.                            \n        /W\\           ( -.- )--------.                  \n   ^    \\|/            \\_o_/         )    ^             \n  /|\\    |     *      ~~~~~~~       /    /|\\            \n  / \\   / \\  / |\\                    /    / \\            \n~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~ ~~~~~~~~~\nWelcome, traveler. A mighty dragon blocks the gate.\nSpeak the secret incantation ( 10 runic letters) to continue.\n"
      );
  local_c8 = (undefined1  [16])0x0;
  local_b8 = (undefined1  [16])0x0;
  local_a8 = (undefined1  [16])0x0;
  local_98 = (undefined1  [16])0x0;
  local_88 = (undefined1  [16])0x0;
  local_78 = (undefined1  [16])0x0;
  local_68 = (undefined1  [16])0x0;
  local_58 = (undefined1  [16])0x0;
  printf("Enter your incantation: ");
  pcVar5 = fgets(local_c8,0x80,stdin);
  if (pcVar5 == (char *)0x0) {
    puts("\nSomething went awry. Fare thee well...");
  }
  else {
    sVar6 = strcspn(local_c8,"\n");
    local_c8[sVar6] = 0;
    sVar6 = strlen(local_c8);
    if (sVar6 == 10) {
      ppuVar7 = __ctype_b_loc();
      pbVar8 = local_c8;
      do {
         uVar2 = (*ppuVar7)[*pbVar8];
         if (((uVar2 & 0x400) == 0) || (uVar3 = (*ppuVar7)[pbVar8[1]], (uVar3 & 0x400) == 0)) {
           puts("\nThe runes fail to align. The incantation is impure.");
           puts(&DAT_001022b8);
           goto LAB_0010124c;
         }
         if ((((uVar2 & 0x100) != 0) && ((uVar3 & 0x100) != 0)) ||
            (((uVar2 & 0x200) != 0 && ((uVar3 & 0x200) != 0)))) {
           puts("\nThe ancient seals do not resonate with your runes.");
           puts(&DAT_001022b8);
           goto LAB_0010124c;
         }
         pbVar8 = pbVar8 + 2;
      } while (pbVar8 != local_c8 + 10);
      if ((byte)(local_c8[1] ^ local_c8[0]) == 0x24) {
         if (local_c8[1] == 0x6a) {
           if ((local_c8[2] ^ local_c8[3]) == 0x38) {
             if (local_c8[3] == 0x53) {
                local_10a = 0;
                pbVar8 = local_108;
                local_10c = local_c8._4_2_ << 8 | (ushort)local_c8._4_2_ >> 8;
                sVar6 = strlen((char *)&local_10c);
                MD5((uchar *)&local_10c,sVar6,pbVar8);
                pcVar5 = local_f8;
                do {
                  bVar1 = *pbVar8;
                  pcVar10 = pcVar5 + 2;
                  pbVar8 = pbVar8 + 1;
                  sprintf(pcVar5,"%02x",(ulong)bVar1);
                  pcVar5 = pcVar10;
                } while (local_d8 != pcVar10);
                local_d8[0] = '\0';
                iVar4 = strcmp(local_f8,"33a3192ba92b5a4803c9a9ed70ea5a9c");
                if (iVar4 == 0) {
                  if ((local_c8[6] ^ local_c8[7]) == 0x38) {
                    if (local_c8[7] == 0x61) {
                      if ((byte)(local_c8[9] ^ local_c8[8]) == 0x20) {
                         if (local_c8[9] == 0x69) {
                           printf("\n%s\n",
                                   "   The kingdom\'s gates open, revealing the hidden realm...    \n                         ( (                                 \n                          \\ \\                                \n                     .--.  ) ) .--.                         \n                    (    )/_/ (    )                        \n                     \'--\'       \'--\'                         \n    \"Huzzah! Thy incantation is true. Onward, brave knight!\" \n"
                                  );
                           printf("The final scroll reveals your reward: KCTF{%s}\n\n",local_c8);
                           uVar9 = 0;
                           goto LAB_00101251;
                         }
                         puts("\nThe wards reject your Pair 5 second char.");
                         puts(&DAT_001022b8);
                      }
                      else {
                         puts("\nThe wards reject your Pair 5.");
                         puts(&DAT_001022b8);
                      }
                    }
                    else {
                      puts("\nThe wards reject your Pair 4 second char.");
                      puts(&DAT_001022b8);
                    }
                  }
                  else {
                    puts("\nThe wards reject your Pair 4.");
                    puts(&DAT_001022b8);
                  }
                }
                else {
                  puts("\nThe dragon\'s eyes glow red... The final seal remains locked.");
                  puts(&DAT_001022b8);
                }
             }
             else {
                puts("\nThe wards reject your Pair 2 second char.");
                puts(&DAT_001022b8);
             }
           }
           else {
             puts("\nThe wards reject your Pair 2.");
             puts(&DAT_001022b8);
           }
         }
         else {
           puts("\nThe wards reject your Pair 1 second char.");
           puts(&DAT_001022b8);
         }
      }
      else {
         puts("\nThe wards reject your Pair 1.");
         puts(&DAT_001022b8);
      }
    }
    else {
      puts("\nScribe\'s note: The incantation must be exactly 10 runic symbols.");
      puts(&DAT_001022b8);
    }
  }
LAB_0010124c:
  uVar9 = 1;
LAB_00101251:
  if (local_40 == *(long *)(in_FS_OFFSET + 0x28)) {
    return uVar9;
  }
                      /* WARNING: Subroutine does not return */
  __stack_chk_fail();
}
```

so here we understand what type of characters we can use - 

c0 c1 c2 c3 c4 c5 c6 c7 c8 c9 

```
if (((uVar2 & 0x400) == 0) || (uVar3 = (*ppuVar7)[pbVar8[1]], (uVar3 & 0x400) == 0))
puts("\nThe runes fail to align. The incantation is impure.");
```

This line of code says the characters need to be alphabets ( we know this because of 0x400 is the hex for the bit mask isalpha)

```
                     if ((((uVar2 & 0x100) != 0) && ((uVar3 & 0x100) != 0)) ||
                             (((uVar2 & 0x200) != 0 && ((uVar3 & 0x200) != 0)))) {
                           puts("\nThe ancient seals do not resonate with your runes.");
```

This line of code says that the characters cannot be both (pair) capitals or lowecase ( 0x100 is uppercase and 0x200 for lower)

Lets begin finding the characters - 
```
                if ((byte)(local_c8[1] ^ local_c8[0]) == 0x24) {
                     if (local_c8[1] == 0x6a) {
```

c0 ^ c1 = 0x24 ( XOR = 36)
where c1 = 0x6a ( j)

so c1 = 0x24 ^ 0x6a = 0x4e (N)

```
                           if ((local_c8[2] ^ local_c8[3]) == 0x38) {
                                if (local_c8[3] == 0x53)
```

(c2 ^ c3) == 0x38
c3 == 0x53  (S)

so c2 = 0x53 ^ 0x38 = 0x6b = 'k'

```
local_10c = local_c8._4_2_ << 8 | (ushort)local_c8._4_2_ >> 8;
MD5((uchar *)&local_10c, sVar6, pbVar8);
strcmp(md5_result, "33a3192ba92b5a4803c9a9ed70ea5a9c");
```

This is different, here via brute forcing we get 
c4 = T , c5 = f 

the rest are similar to the prior 

```

                                           if ((local_c8[6] ^ local_c8[7]) == 0x38) {
                                                if (local_c8[7] == 0x61)

                                                      if ((byte)(local_c8[9] ^ local_c8[8]) == 0x20) {
                                                           if (local_c8[9] == 0x69)
```

c6 = Y, c7 = a, c8 = I, c9 = i 

so the characters are - 

```
NjkSfTYaIi
```

<img width="774" height="496" alt="image" src="https://github.com/user-attachments/assets/93c24297-fd87-439c-8126-38d63c3d2e4e" />

# Time 

## Flag: 

## Steps- 

In this challenge we have to enter the right number in the program to get the flag. After using ghidra i find what the program does 

```ruby

undefined8 main(void)

{
  undefined4 uVar1;
  undefined8 uVar2;
  long in_FS_OFFSET;
  int iStack_18;
  int iStack_14;
  long lStack_10;
  
  lStack_10 = *(long *)(in_FS_OFFSET + 0x28);
  uVar1 = time(0);
  srand(uVar1);
  iStack_14 = FUN_00400790();
  puts("Welcome to the number guessing game!");
  puts("I\'m thinking of a number. Can you guess it?");
  puts("Guess right and you get a flag!");
  printf("Enter your number: ");
  fflush(stdout);
  __isoc99_scanf(&DAT_00400bbc,&iStack_18);
  printf("Your guess was %u.\n",iStack_18);
  printf("Looking for %u.\n",iStack_14);
  fflush(stdout);
  if (iStack_14 == iStack_18) {
    puts("You won. Guess was right! Here\'s your flag:");
    giveFlag();
  }
  else {
    puts("Sorry. Try again, wrong guess!");
  }
  fflush(stdout);
  uVar2 = 0;
  if (lStack_10 != *(long *)(in_FS_OFFSET + 0x28)) {
    uVar2 = __stack_chk_fail();
  }
  return uVar2;
}
```

giveflag function: 

```ruby
void giveFlag(void)

{
  long lVar1;
  long in_FS_OFFSET;
  undefined1 local_118 [264];
  long local_10;
  
  local_10 = *(long *)(in_FS_OFFSET + 0x28);
  memset(local_118,0,0x100);
  lVar1 = fopen("/home/h3/flag.txt",&DAT_00400ad8);
  if (lVar1 == 0) {
    puts("Flag file not found!  Contact an H3 admin for assistance.");
  }
  else {
    fgets(local_118,0x100,lVar1);
    fclose(lVar1);
    puts(local_118);
  }
  if (local_10 != *(long *)(in_FS_OFFSET + 0x28)) {
    __stack_chk_fail();
  }
  return;
}
```
FUN_00400790()
 
```
void FUN_00400790(void)

{
  rand();
  return;
}
```

So the program basically, using the 'time' to make the secret number, using the time in seconds as an input for srand(), and then the FUN_00400790() which just does rand(), we can use gdb, to break at the point where srand() is used and print the input it used, after that using a simple C program we can get the secret number.

```
uVar1 = time(0);
  srand(uVar1);
```
this gave it away. 

Now using gdb, i created a break point at srand()

```ruby

gdb-peda$ break srand()
```

After creating the break point and running the program, it stops 

<img width="824" height="815" alt="image" src="https://github.com/user-attachments/assets/cbb24781-ccd9-4176-b986-733fe954c569" />

using 
```
print $rdi
```

we get the input which was 
```
$1 = 0x692c1235
```

Once we got the input ( basically this is seconds in time in hex), using a simple C code we can calculate what the secret number is going to be 

```ruby
#include <stdio.h>
#include <stdlib.h>

int main() {
    unsigned int seed = 0x692c0f42;
    srand(seed);
    int secret = rand();
    printf("u%\n",secret);
    return 0;
}
```
we get the number [1360983517]

now, resuming the program in gdb it asks for the number, and i enter the number we got. 

<img width="521" height="223" alt="image" src="https://github.com/user-attachments/assets/a1718859-9d36-4bc7-8339-6dd131b6f08e" />


