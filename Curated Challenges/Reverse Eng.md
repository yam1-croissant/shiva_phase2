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

