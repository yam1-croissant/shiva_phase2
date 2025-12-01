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

# VeridisQuo

## Flag:byuctf{android_piece_0f_c4ke}

## Steps -

Here we are provided with an apk file,and we have to retrieve the flag from it, i used JADX to extract the files into one single folder.

The file had 2 folders "Resource" and "Source", i was able to find these files which gave me an idea of where to start. 

<img width="727" height="273" alt="image" src="https://github.com/user-attachments/assets/c83a8c27-5233-4e30-9c49-501847037422" />

In Utilities file-
```
package byuctf.downwiththefrench;

import android.app.Activity;
import android.widget.TextView;

/* loaded from: classes3.dex */
public class Utilities {
    private Activity activity;

    public Utilities(Activity activity) {
        this.activity = activity;
    }

    public void cleanUp() {
        TextView flag = (TextView) this.activity.findViewById(R.id.flagPart1);
        flag.setText("");
        TextView flag2 = (TextView) this.activity.findViewById(R.id.flagPart2);
        flag2.setText("");
        TextView flag3 = (TextView) this.activity.findViewById(R.id.flagPart3);
        flag3.setText("");
        TextView flag4 = (TextView) this.activity.findViewById(R.id.flagPart4);
        flag4.setText("");
        TextView flag5 = (TextView) this.activity.findViewById(R.id.flagPart5);
        flag5.setText("");
        TextView flag6 = (TextView) this.activity.findViewById(R.id.flagPart6);
        flag6.setText("");
        TextView flag7 = (TextView) this.activity.findViewById(R.id.flagPart7);
        flag7.setText("");
        TextView flag8 = (TextView) this.activity.findViewById(R.id.flagPart8);
        flag8.setText("");
        TextView flag9 = (TextView) this.activity.findViewById(R.id.flagPart9);
        flag9.setText("");
        TextView flag10 = (TextView) this.activity.findViewById(R.id.flagPart10);
        flag10.setText("");
        TextView flag11 = (TextView) this.activity.findViewById(R.id.flagPart11);
        flag11.setText("");
        TextView flag12 = (TextView) this.activity.findViewById(R.id.flagPart12);
        flag12.setText("");
        TextView flag13 = (TextView) this.activity.findViewById(R.id.flagPart13);
        flag13.setText("");
        TextView flag14 = (TextView) this.activity.findViewById(R.id.flagPart14);
        flag14.setText("");
        TextView flag15 = (TextView) this.activity.findViewById(R.id.flagPart15);
        flag15.setText("");
        TextView flag16 = (TextView) this.activity.findViewById(R.id.flagPart16);
        flag16.setText("");
        TextView flag17 = (TextView) this.activity.findViewById(R.id.flagPart17);
        flag17.setText("");
        TextView flag18 = (TextView) this.activity.findViewById(R.id.flagPart18);
        flag18.setText("");
        TextView flag19 = (TextView) this.activity.findViewById(R.id.flagPart19);
        flag19.setText("");
        TextView flag20 = (TextView) this.activity.findViewById(R.id.flagPart20);
        flag20.setText("");
        TextView flag21 = (TextView) this.activity.findViewById(R.id.flagPart21);
        flag21.setText("");
        TextView flag22 = (TextView) this.activity.findViewById(R.id.flagPart22);
        flag22.setText("");
        TextView flag23 = (TextView) this.activity.findViewById(R.id.flagPart23);
        flag23.setText("");
        TextView flag24 = (TextView) this.activity.findViewById(R.id.flagPart24);
        flag24.setText("");
        TextView flag25 = (TextView) this.activity.findViewById(R.id.flagPart25);
        flag25.setText("");
        TextView flag26 = (TextView) this.activity.findViewById(R.id.flagPart26);
        flag26.setText("");
        TextView flag27 = (TextView) this.activity.findViewById(R.id.flagPart27);
        flag27.setText("");
        TextView flag28 = (TextView) this.activity.findViewById(R.id.flagPart28);
        flag28.setText("");
    }
}
```

Here what we understand is that the flag is split into 28 parts, to find the location of these flag id's, i used grep 

```
grep -R "flagPart"
```

With that I find traces of flagPart being used 

```
sources/byuctf/downwiththefrench/Utilities.java:        TextView flag = (TextView) this.activity.findViewById(R.id.flagPart1);
sources/byuctf/downwiththefrench/Utilities.java:        TextView flag2 = (TextView) this.activity.findViewById(R.id.flagPart2);
sources/byuctf/downwiththefrench/Utilities.java:        TextView flag3 = (TextView) this.activity.findViewById(R.id.flagPart3);
sources/byuctf/downwiththefrench/Utilities.java:        TextView flag4 = (TextView) this.activity.findViewById(R.id.flagPart4);
sources/byuctf/downwiththefrench/Utilities.java:        TextView flag5 = (TextView) this.activity.findViewById(R.id.flagPart5);
sources/byuctf/downwiththefrench/Utilities.java:        TextView flag6 = (TextView) this.activity.findViewById(R.id.flagPart6);
sources/byuctf/downwiththefrench/Utilities.java:        TextView flag7 = (TextView) this.activity.findViewById(R.id.flagPart7);
sources/byuctf/downwiththefrench/Utilities.java:        TextView flag8 = (TextView) this.activity.findViewById(R.id.flagPart8);
sources/byuctf/downwiththefrench/Utilities.java:        TextView flag9 = (TextView) this.activity.findViewById(R.id.flagPart9);
sources/byuctf/downwiththefrench/Utilities.java:        TextView flag10 = (TextView) this.activity.findViewById(R.id.flagPart10);
sources/byuctf/downwiththefrench/Utilities.java:        TextView flag11 = (TextView) this.activity.findViewById(R.id.flagPart11);
sources/byuctf/downwiththefrench/Utilities.java:        TextView flag12 = (TextView) this.activity.findViewById(R.id.flagPart12);
sources/byuctf/downwiththefrench/Utilities.java:        TextView flag13 = (TextView) this.activity.findViewById(R.id.flagPart13);
sources/byuctf/downwiththefrench/Utilities.java:        TextView flag14 = (TextView) this.activity.findViewById(R.id.flagPart14);
sources/byuctf/downwiththefrench/Utilities.java:        TextView flag15 = (TextView) this.activity.findViewById(R.id.flagPart15);
sources/byuctf/downwiththefrench/Utilities.java:        TextView flag16 = (TextView) this.activity.findViewById(R.id.flagPart16);
sources/byuctf/downwiththefrench/Utilities.java:        TextView flag17 = (TextView) this.activity.findViewById(R.id.flagPart17);
sources/byuctf/downwiththefrench/Utilities.java:        TextView flag18 = (TextView) this.activity.findViewById(R.id.flagPart18);
sources/byuctf/downwiththefrench/Utilities.java:        TextView flag19 = (TextView) this.activity.findViewById(R.id.flagPart19);
sources/byuctf/downwiththefrench/Utilities.java:        TextView flag20 = (TextView) this.activity.findViewById(R.id.flagPart20);
sources/byuctf/downwiththefrench/Utilities.java:        TextView flag21 = (TextView) this.activity.findViewById(R.id.flagPart21);
sources/byuctf/downwiththefrench/Utilities.java:        TextView flag22 = (TextView) this.activity.findViewById(R.id.flagPart22);
sources/byuctf/downwiththefrench/Utilities.java:        TextView flag23 = (TextView) this.activity.findViewById(R.id.flagPart23);
sources/byuctf/downwiththefrench/Utilities.java:        TextView flag24 = (TextView) this.activity.findViewById(R.id.flagPart24);
sources/byuctf/downwiththefrench/Utilities.java:        TextView flag25 = (TextView) this.activity.findViewById(R.id.flagPart25);
sources/byuctf/downwiththefrench/Utilities.java:        TextView flag26 = (TextView) this.activity.findViewById(R.id.flagPart26);
sources/byuctf/downwiththefrench/Utilities.java:        TextView flag27 = (TextView) this.activity.findViewById(R.id.flagPart27);
sources/byuctf/downwiththefrench/Utilities.java:        TextView flag28 = (TextView) this.activity.findViewById(R.id.flagPart28);
sources/byuctf/downwiththefrench/R.java:        public static int flagPart1 = 0x7f0800c2;
sources/byuctf/downwiththefrench/R.java:        public static int flagPart10 = 0x7f0800c3;
sources/byuctf/downwiththefrench/R.java:        public static int flagPart11 = 0x7f0800c4;
sources/byuctf/downwiththefrench/R.java:        public static int flagPart12 = 0x7f0800c5;
sources/byuctf/downwiththefrench/R.java:        public static int flagPart13 = 0x7f0800c6;
sources/byuctf/downwiththefrench/R.java:        public static int flagPart14 = 0x7f0800c7;
sources/byuctf/downwiththefrench/R.java:        public static int flagPart15 = 0x7f0800c8;
sources/byuctf/downwiththefrench/R.java:        public static int flagPart16 = 0x7f0800c9;
sources/byuctf/downwiththefrench/R.java:        public static int flagPart17 = 0x7f0800ca;
sources/byuctf/downwiththefrench/R.java:        public static int flagPart18 = 0x7f0800cb;
sources/byuctf/downwiththefrench/R.java:        public static int flagPart19 = 0x7f0800cc;
sources/byuctf/downwiththefrench/R.java:        public static int flagPart2 = 0x7f0800cd;
sources/byuctf/downwiththefrench/R.java:        public static int flagPart20 = 0x7f0800ce;
sources/byuctf/downwiththefrench/R.java:        public static int flagPart21 = 0x7f0800cf;
sources/byuctf/downwiththefrench/R.java:        public static int flagPart22 = 0x7f0800d0;
sources/byuctf/downwiththefrench/R.java:        public static int flagPart23 = 0x7f0800d1;
sources/byuctf/downwiththefrench/R.java:        public static int flagPart24 = 0x7f0800d2;
sources/byuctf/downwiththefrench/R.java:        public static int flagPart25 = 0x7f0800d3;
sources/byuctf/downwiththefrench/R.java:        public static int flagPart26 = 0x7f0800d4;
sources/byuctf/downwiththefrench/R.java:        public static int flagPart27 = 0x7f0800d5;
sources/byuctf/downwiththefrench/R.java:        public static int flagPart28 = 0x7f0800d6;
sources/byuctf/downwiththefrench/R.java:        public static int flagPart3 = 0x7f0800d7;
sources/byuctf/downwiththefrench/R.java:        public static int flagPart4 = 0x7f0800d8;
sources/byuctf/downwiththefrench/R.java:        public static int flagPart5 = 0x7f0800d9;
sources/byuctf/downwiththefrench/R.java:        public static int flagPart6 = 0x7f0800da;
sources/byuctf/downwiththefrench/R.java:        public static int flagPart7 = 0x7f0800db;
sources/byuctf/downwiththefrench/R.java:        public static int flagPart8 = 0x7f0800dc;
sources/byuctf/downwiththefrench/R.java:        public static int flagPart9 = 0x7f0800dd;
resources/res/values/public.xml:    <public type="id" name="flagPart1" id="0x7f0800c2" />
resources/res/values/public.xml:    <public type="id" name="flagPart10" id="0x7f0800c3" />
resources/res/values/public.xml:    <public type="id" name="flagPart11" id="0x7f0800c4" />
resources/res/values/public.xml:    <public type="id" name="flagPart12" id="0x7f0800c5" />
resources/res/values/public.xml:    <public type="id" name="flagPart13" id="0x7f0800c6" />
resources/res/values/public.xml:    <public type="id" name="flagPart14" id="0x7f0800c7" />
resources/res/values/public.xml:    <public type="id" name="flagPart15" id="0x7f0800c8" />
resources/res/values/public.xml:    <public type="id" name="flagPart16" id="0x7f0800c9" />
resources/res/values/public.xml:    <public type="id" name="flagPart17" id="0x7f0800ca" />
resources/res/values/public.xml:    <public type="id" name="flagPart18" id="0x7f0800cb" />
resources/res/values/public.xml:    <public type="id" name="flagPart19" id="0x7f0800cc" />
resources/res/values/public.xml:    <public type="id" name="flagPart2" id="0x7f0800cd" />
resources/res/values/public.xml:    <public type="id" name="flagPart20" id="0x7f0800ce" />
resources/res/values/public.xml:    <public type="id" name="flagPart21" id="0x7f0800cf" />
resources/res/values/public.xml:    <public type="id" name="flagPart22" id="0x7f0800d0" />
resources/res/values/public.xml:    <public type="id" name="flagPart23" id="0x7f0800d1" />
resources/res/values/public.xml:    <public type="id" name="flagPart24" id="0x7f0800d2" />
resources/res/values/public.xml:    <public type="id" name="flagPart25" id="0x7f0800d3" />
resources/res/values/public.xml:    <public type="id" name="flagPart26" id="0x7f0800d4" />
resources/res/values/public.xml:    <public type="id" name="flagPart27" id="0x7f0800d5" />
resources/res/values/public.xml:    <public type="id" name="flagPart28" id="0x7f0800d6" />
resources/res/values/public.xml:    <public type="id" name="flagPart3" id="0x7f0800d7" />
resources/res/values/public.xml:    <public type="id" name="flagPart4" id="0x7f0800d8" />
resources/res/values/public.xml:    <public type="id" name="flagPart5" id="0x7f0800d9" />
resources/res/values/public.xml:    <public type="id" name="flagPart6" id="0x7f0800da" />
resources/res/values/public.xml:    <public type="id" name="flagPart7" id="0x7f0800db" />
resources/res/values/public.xml:    <public type="id" name="flagPart8" id="0x7f0800dc" />
resources/res/values/public.xml:    <public type="id" name="flagPart9" id="0x7f0800dd" />
resources/res/layout/activity_main.xml:        android:id="@+id/flagPart1"
resources/res/layout/activity_main.xml:        android:id="@+id/flagPart2"
resources/res/layout/activity_main.xml:        android:id="@+id/flagPart3"
resources/res/layout/activity_main.xml:        android:id="@+id/flagPart4"
resources/res/layout/activity_main.xml:        android:id="@+id/flagPart5"
resources/res/layout/activity_main.xml:        android:id="@+id/flagPart6"
resources/res/layout/activity_main.xml:        android:id="@+id/flagPart7"
resources/res/layout/activity_main.xml:        android:id="@+id/flagPart8"
resources/res/layout/activity_main.xml:        android:id="@+id/flagPart9"
resources/res/layout/activity_main.xml:        android:id="@+id/flagPart10"
resources/res/layout/activity_main.xml:        android:id="@+id/flagPart11"
resources/res/layout/activity_main.xml:        android:id="@+id/flagPart12"
resources/res/layout/activity_main.xml:        android:id="@+id/flagPart13"
resources/res/layout/activity_main.xml:        android:id="@+id/flagPart14"
resources/res/layout/activity_main.xml:        android:id="@+id/flagPart15"
resources/res/layout/activity_main.xml:        android:id="@+id/flagPart16"
resources/res/layout/activity_main.xml:        android:id="@+id/flagPart17"
resources/res/layout/activity_main.xml:        android:id="@+id/flagPart18"
resources/res/layout/activity_main.xml:        android:id="@+id/flagPart19"
resources/res/layout/activity_main.xml:        android:id="@+id/flagPart20"
resources/res/layout/activity_main.xml:        android:id="@+id/flagPart21"
resources/res/layout/activity_main.xml:        android:id="@+id/flagPart22"
resources/res/layout/activity_main.xml:        android:id="@+id/flagPart23"
resources/res/layout/activity_main.xml:        android:id="@+id/flagPart24"
resources/res/layout/activity_main.xml:        android:id="@+id/flagPart25"
resources/res/layout/activity_main.xml:        android:id="@+id/flagPart26"
resources/res/layout/activity_main.xml:        android:id="@+id/flagPart27"
resources/res/layout/activity_main.xml:        android:id="@+id/flagPart28"
grep: resources/classes2.dex: binary file matches
grep: resources/classes3.dex: binary file matches
```

So i checked all these files / folder , and in the activity main- 

```
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android" xmlns:app="http://schemas.android.com/apk/res-auto"
    android:layout_width="match_parent"
    android:layout_height="match_parent">
    <TextView
        android:id="@+id/homeText"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="b"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.066"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.022"/>
    <TextView
        android:id="@+id/flagPart1"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginBottom="420dp"
        android:text="}"
        android:layout_marginEnd="216dp"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"/>
    <TextView
        android:id="@+id/flagPart2"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginBottom="616dp"
        android:text="t"
        android:layout_marginEnd="340dp"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"/>
    <TextView
        android:id="@+id/flagPart3"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginBottom="556dp"
        android:text="a"
        android:layout_marginEnd="332dp"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"/>
    <TextView
        android:id="@+id/flagPart4"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginBottom="676dp"
        android:text="y"
        android:layout_marginEnd="368dp"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"/>
    <TextView
        android:id="@+id/flagPart5"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginBottom="500dp"
        android:text="c"
        android:layout_marginEnd="252dp"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"/>
    <TextView
        android:id="@+id/flagPart6"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginBottom="636dp"
        android:text="c"
        android:layout_marginEnd="348dp"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"/>
    <TextView
        android:id="@+id/flagPart7"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginBottom="436dp"
        android:text="d"
        android:layout_marginEnd="364dp"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"/>
    <TextView
        android:id="@+id/flagPart8"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginBottom="496dp"
        android:text="r"
        android:layout_marginEnd="348dp"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"/>
    <TextView
        android:id="@+id/flagPart9"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginBottom="536dp"
        android:text="n"
        android:layout_marginEnd="336dp"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"/>
    <TextView
        android:id="@+id/flagPart10"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginBottom="456dp"
        android:text="i"
        android:layout_marginEnd="360dp"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"/>
    <TextView
        android:id="@+id/flagPart11"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginBottom="536dp"
        android:text="0"
        android:layout_marginEnd="276dp"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"/>
    <TextView
        android:id="@+id/flagPart12"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginBottom="516dp"
        android:text="d"
        android:layout_marginEnd="340dp"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"/>
    <TextView
        android:id="@+id/flagPart13"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginBottom="460dp"
        android:text="k"
        android:layout_marginEnd="232dp"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"/>
    <TextView
        android:id="@+id/flagPart14"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginBottom="656dp"
        android:text="u"
        android:layout_marginEnd="356dp"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"/>
    <TextView
        android:id="@+id/flagPart15"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginBottom="452dp"
        android:text="p"
        android:layout_marginEnd="320dp"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"/>
    <TextView
        android:id="@+id/flagPart16"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginBottom="476dp"
        android:text="o"
        android:layout_marginEnd="352dp"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"/>
    <TextView
        android:id="@+id/flagPart17"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginBottom="500dp"
        android:text="c"
        android:layout_marginEnd="300dp"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"/>
    <TextView
        android:id="@+id/flagPart18"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginBottom="596dp"
        android:text="f"
        android:layout_marginEnd="332dp"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"/>
    <TextView
        android:id="@+id/flagPart19"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginBottom="484dp"
        android:text="e"
        android:layout_marginEnd="308dp"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"/>
    <TextView
        android:id="@+id/flagPart20"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginBottom="436dp"
        android:text="_"
        android:layout_marginEnd="328dp"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"/>
    <TextView
        android:id="@+id/flagPart21"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginBottom="516dp"
        android:text="e"
        android:layout_marginEnd="292dp"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"/>
    <TextView
        android:id="@+id/flagPart22"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginBottom="536dp"
        android:text="_"
        android:layout_marginEnd="284dp"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"/>
    <TextView
        android:id="@+id/flagPart23"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginBottom="536dp"
        android:text="f"
        android:layout_marginEnd="268dp"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"/>
    <TextView
        android:id="@+id/flagPart24"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginBottom="468dp"
        android:text="i"
        android:layout_marginEnd="316dp"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"/>
    <TextView
        android:id="@+id/flagPart25"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginBottom="516dp"
        android:text="_"
        android:layout_marginEnd="260dp"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"/>
    <TextView
        android:id="@+id/flagPart26"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginBottom="480dp"
        android:text="4"
        android:layout_marginEnd="240dp"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"/>
    <TextView
        android:id="@+id/flagPart27"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginBottom="440dp"
        android:text="e"
        android:layout_marginEnd="224dp"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"/>
    <TextView
        android:id="@+id/flagPart28"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginBottom="576dp"
        android:text="{"
        android:layout_marginEnd="324dp"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"/>
</androidx.constraintlayout.widget.ConstraintLayout
```

i was able to find what the 29 parts were ( including the hometext)

[  b}tayccdrni0dkupocfe_e_fi_4e{       ]

but this does not look in order of the flagPart id's mentioned because isnt ,it is actually in order of the highest value of
'layout_constraintBottom' , using Android Studio to visualize this. 

<img width="1244" height="807" alt="image" src="https://github.com/user-attachments/assets/f22ca431-a6c7-419b-94a3-094a7c3ea3b7" />

# Dusty - dusty_noob

## Flag: DawgCTF{FR33_C4R_W45H!}

## Steps - 

I ran the file in ghidra.

Rust - 
 _ZN3std2rt10lang_start...... = is the naming convention used for runtime startup function
 _ZN10shinyclean4main17... = is the naming convention used for main function of program (shinyclean::main)

```ruby
void main(int param_1,undefined8 param_2)

{
  _ZN3std2rt10lang_start17h91ff47afc442db24E
            (_ZN10shinyclean4main17h4b15dd54e331d693E,(long)param_1,param_2,0);
  return;
}
```

so this basically calls rust's runtime start function and execute the program's main function

```
it cannot just run your program it needs, runtime initalization, thread local storage bla bla, its like the arch of programing
```

So looking into the main()

```ruby

void _ZN10shinyclean4main17h4b15dd54e331d693E(void)

{
  int iVar1;
  ulong uStack_100;
  byte bStack_f1;
  ulong uStack_f0;
  byte abStack_de [23];
  byte abStack_c7 [23];
  ulong uStack_b0;
  undefined1 auStack_a8 [48];
  byte *pbStack_78;
  code *pcStack_70;
  byte *pbStack_68;
  code *pcStack_60;
  undefined1 auStack_58 [48];
  byte *pbStack_28;
  code *pcStack_20;
  byte *pbStack_18;
  code *pcStack_10;
  byte *pbStack_8;
  
  memset(abStack_de,0,0x17);
  abStack_c7[0] = 0x7b;
  abStack_c7[1] = 0x5e;
  abStack_c7[2] = 0x48;
  abStack_c7[3] = 0x58;
  abStack_c7[4] = 0x7c;
  abStack_c7[5] = 0x6b;
  abStack_c7[6] = 0x79;
  abStack_c7[7] = 0x44;
  abStack_c7[8] = 0x79;
  abStack_c7[9] = 0x6d;
  abStack_c7[10] = 0xc;
  abStack_c7[0xb] = 0xc;
  abStack_c7[0xc] = 0x60;
  abStack_c7[0xd] = 0x7c;
  abStack_c7[0xe] = 0xb;
  abStack_c7[0xf] = 0x6d;
  abStack_c7[0x10] = 0x60;
  abStack_c7[0x11] = 0x68;
  abStack_c7[0x12] = 0xb;
  abStack_c7[0x13] = 10;
  abStack_c7[0x14] = 0x77;
  abStack_c7[0x15] = 0x1e;
  abStack_c7[0x16] = 0x42;
  uStack_b0 = 0;
  do {
    if (uStack_b0 < 0x17) {
      bStack_f1 = abStack_c7[uStack_b0];
      uStack_f0 = uStack_b0;
      if (uStack_b0 < 0x17) goto LAB_00107c1d;
      _ZN4core9panicking18panic_bounds_check17h8307ccead484a122E(uStack_b0,0x17,&PTR_DAT_00154590);
    }
    else {
      _ZN4core9panicking18panic_bounds_check17h8307ccead484a122E(uStack_b0,0x17,&PTR_DAT_00154578);
LAB_00107c1d:
      abStack_de[uStack_f0] = bStack_f1 ^ 0x3f;
      uStack_100 = uStack_b0 + 1;
      if (0xfffffffffffffffe < uStack_b0) {
        _ZN4core9panicking11panic_const24panic_const_add_overflow17hf2f4fb688348b3b0E
                  (&PTR_DAT_001545a8);
        goto LAB_00107c83;
      }
    }
    uStack_b0 = uStack_100;
    if (uStack_100 == 0x17) {
LAB_00107c83:
      iVar1 = _ZN3std7process2id17hcbcee05e6d949703E();
      if (iVar1 == 0x1c1e8b2) {
        pbStack_18 = abStack_de;
        pcStack_10 = 
        _ZN4core5array69_$LT$impl$u20$core..fmt..Debug$u20$for$u20$$u5b$T$u3b$$u20$N$u5d$$GT$3fmt17h f6f6e41e4948d91cE
        ;
        pbStack_8 = abStack_de;
        pbStack_78 = abStack_de;
        pcStack_20 = 
        _ZN4core5array69_$LT$impl$u20$core..fmt..Debug$u20$for$u20$$u5b$T$u3b$$u20$N$u5d$$GT$3fmt17h f6f6e41e4948d91cE
        ;
        pcStack_60 = 
        _ZN4core5array69_$LT$impl$u20$core..fmt..Debug$u20$for$u20$$u5b$T$u3b$$u20$N$u5d$$GT$3fmt17h f6f6e41e4948d91cE
        ;
        pcStack_70 = 
        _ZN4core5array69_$LT$impl$u20$core..fmt..Debug$u20$for$u20$$u5b$T$u3b$$u20$N$u5d$$GT$3fmt17h f6f6e41e4948d91cE
        ;
        pbStack_68 = pbStack_78;
        pbStack_28 = pbStack_78;
        _ZN4core3fmt9Arguments6new_v117hfac9ebf3d99d1264E(auStack_a8,&DAT_001545c0,&pbStack_78);
        _ZN3std2io5stdio6_print17he7d505d4f02a1803E(auStack_a8);
      }
      else {
        _ZN4core3fmt9Arguments9new_const17hf72ed85907e377bbE(auStack_58,&PTR_DAT_001545e0);
        _ZN3std2io5stdio6_print17he7d505d4f02a1803E(auStack_58);
      }
      return;
    }
  } while( true );
}

```

memset , fills a block of memory with a value, so here we read that abStack_de is empty with 23 bytes size

```ruby
memset (*buffer,int value, size_t size)

to make it empty we enter value as 0, which fills the array filled with 23 zeros
```

Next we understand that abStack_c7 is the encoded byte, and the _de is the decoded flag


```
bStack_f1 = abStack_c7[uStack_b0];
      uStack_f0 = uStack_b0;
.
.
.
 abStack_de[uStack_f0] = bStack_f1 ^ 0x3f; ---------------here basically the byte to be encoded is encoded using XOR 0x3F. the [i] is just the index like it is numbered
```

This process of encoding is used to loop all the 23 bytes.

```ruby
  uStack_100 = uStack_b0 + 1; --------------------look here uStack_b0 is the index and its like saying n+1
      if (0xfffffffffffffffe < uStack_b0) {
        _ZN4core9panicking11panic_const24panic_const_add_overflow17hf2f4fb688348b3b0E
                  (&PTR_DAT_001545a8);
        goto LAB_00107c83;
      }
    }
    uStack_b0 = uStack_100; --------- new index set at n+1
    if (uStack_100 == 0x17) {
```
After encoding all the bytes, the program checks the PID using the 

```
iVar1 = std:process::id()

if (iVar1 == 0x1c1e8b2) 

then print flag
else print no flog

```

 But the issue with that is the, PID required is in the millions quite literally, and apparents thats not possible meaning the flag wont print ---- makes sense why when i tried running the program in gdb it didnt run

```

 iVar1 = _ZN3std7process2id17hcbcee05e6d949703E();
      if (iVar1 == 0x1c1e8b2) {
        pbStack_18 = abStack_de;
```

So we need to modify the PID, and then decode the flag to do that, i use gdb

```
break _ZN10shinyclean4main17h4b15dd54e331d693E
.
.
.
disassemble
.
.
.
0x000055555555bc89 <+329>:	cmp    eax,0x1c1e8b2
.
.
.
breaking at the address where the program compares eax and pid
```
Now that we know that the address [0x000055555555bc89], i re run the program and break at the address and set $eax as the pid given and continue

<img width="1900" height="831" alt="image" src="https://github.com/user-attachments/assets/a55d68f9-0c85-459a-9510-ffbb8684e22d" />

Rewarded with - 

[68,97,119,103,67,84,70,123,70,82,51,51,95,67,52,82,95,87,52,53,72,33,125]

in ascii it is -

DawgCTF{FR33_C4R_W45H!}

# dusty_intermidate

## Flag:

## Steps -
```
_ZN3std4sync4mpsc7channel - creates a channel ( includes a sender that sends inputs to a supposed worker thread and reciever which receives it back, all this data is stored in variables such as 'ustack' 238) 
```
```
mpsc::channel() to communicate between threads
```

_ZN3std2io5stdio5stdin..read_line - reads a full line of text from stdin into a String buffer (auStack_1b8) , so auStack_1b8 contains the input string

```
_ZN3std6thread5spawn17hc82cf960114777baE(&uStack_168,&uStack_150); - this is a worker thread
```
```
  auVar6 = _ZN65_$LT$alloc..string..String$u20$as$u20$core..ops..deref..Deref$GT$5deref17h959f382726 60c74eE
                     (auStack_1b8);
  auVar6 = _ZN4core3str21_$LT$impl$u20$str$GT$5bytes17h9904487a65a9711fE(auVar6._0_8_,auVar6._8_8_);
  auStack_130 = _ZN63_$LT$I$u20$as$u20$core..iter..traits..collect..IntoIterator$GT$9into_iter17h0da a883d0d141f71E
                          (auVar6._0_8_,auVar6._8_8_);
  while( true ) {
    bStack_11a = _ZN81_$LT$core..str..iter..Bytes$u20$as$u20$core..iter..traits..iterator..Iterator$ GT$4next17h46258fd237e9d369E
```
this block? converts the string to bytes then sends each byte via _ZN3std4sync4mpsc15Sender$LT$T$GT$4send17h389f8f24c1d1c8a7E(&uStack_238); which is in form 

Sender::send(&uStack_238, byte)

After the loop finishes, it sends a 0 via send(&uStack_238, 0) to indicate end-of-stream

```ruby
auStack_118 = _ZN3std6thread19JoinHandle$LT$T$GT$4join17ha0b12799c7fbcb23E(&uStack_108)

 _ZN5alloc3vec16Vec$LT$T$C$A$GT$4push17h4bb1f2c545013614E(auStack_e8);
  }
```
this is join thread "JoinHandle::join" waits for the worker to finish to pushing the processed byres to reciever, after that the main function recieves data and pushes each data into [Vec<u8> auStack_e8]
until the receiving stops . So auStack_e8 now contains the bytes received back


