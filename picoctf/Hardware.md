# IQ TEST
## Flag: nite{100010011000}

## Steps - 
x = 30478191278
on coverting to binary

11100011000101001000100101010101110

then i added and extra 0 on the left side, because there are 36 inputes

011100011000101001000100101010101110

And then i manual bruteforced it. 



# I like Logic
## Flag: <img width="643" height="35" alt="image" src="https://github.com/user-attachments/assets/4182f1eb-70b0-4408-8dae-c60f69edaf0e" />

In this Challenge,we are given a .sal file, so it has the raw data (analog and digital signals) of the Saleae logic device
## Steps - 

I used the Saleae logic 2 application, with Async Serial. 
<img width="1906" height="1017" alt="image" src="https://github.com/user-attachments/assets/6de67460-4e5f-4f7b-b9fb-188da00aaca4" />

# Bare Metal Alchemist
## Flag: TCCTF{h1s_1s_m_l3_4rdu1nof_f1rmw4rd}
## Steps- 

I ran the program in ghidra and got the code 

```ruby
 void main(void)


{

char cVar1;

byte bVar2;

char cVar3;

undefined1 auStack_7 [3];

undefined3 uStack_4;

undefined1 uStack_1;

R1 = 0;

uStack_1 = Y._1_1_;

uStack_4 = 0xbe;

Y = CONCAT11((char)((uint)(auStack_7 + 2) >> 8),(char)auStack_7 + '\x02');

R25R24._0_1_ = DAT_mem_0044;

R25R24._0_1_ = (byte)R25R24 | 2;

DAT_mem_0044 = (byte)R25R24;

R25R24._0_1_ = DAT_mem_0044;

R25R24._0_1_ = (byte)R25R24 | 1;

DAT_mem_0044 = (byte)R25R24;

R25R24._0_1_ = DAT_mem_0045;

R25R24._0_1_ = (byte)R25R24 | 2;

DAT_mem_0045 = (byte)R25R24;

R25R24._0_1_ = DAT_mem_0045;

R25R24._0_1_ = (byte)R25R24 | 1;

DAT_mem_0045 = (byte)R25R24;

R25R24._0_1_ = DAT_mem_006e;

R25R24._0_1_ = (byte)R25R24 | 1;

DAT_mem_006e = (byte)R25R24;

DAT_mem_0081 = 0;

R25R24._0_1_ = DAT_mem_0081;

R25R24._0_1_ = (byte)R25R24 | 2;

DAT_mem_0081 = (byte)R25R24;

R25R24._0_1_ = DAT_mem_0081;

R25R24._0_1_ = (byte)R25R24 | 1;

DAT_mem_0081 = (byte)R25R24;

R25R24._0_1_ = DAT_mem_0080;

R25R24._0_1_ = (byte)R25R24 | 1;

DAT_mem_0080 = (byte)R25R24;

R25R24._0_1_ = DAT_mem_00b1;

R25R24._0_1_ = (byte)R25R24 | 4;

DAT_mem_00b1 = (byte)R25R24;

R25R24._0_1_ = DAT_mem_00b0;

R25R24._0_1_ = (byte)R25R24 | 1;

DAT_mem_00b0 = (byte)R25R24;

R25R24._0_1_ = DAT_mem_007a;

R25R24._0_1_ = (byte)R25R24 | 4;

DAT_mem_007a = (byte)R25R24;

R25R24._0_1_ = DAT_mem_007a;

R25R24._0_1_ = (byte)R25R24 | 2;

DAT_mem_007a = (byte)R25R24;

R25R24._0_1_ = DAT_mem_007a;

R25R24._0_1_ = (byte)R25R24 | 1;

DAT_mem_007a = (byte)R25R24;

R25R24._0_1_ = DAT_mem_007a;

R25R24._0_1_ = (byte)R25R24 | 0x80;

DAT_mem_007a = (byte)R25R24;

DAT_mem_00c1 = 0;

R25R24._0_1_ = DAT_mem_002a;

R25R24._0_1_ = (byte)R25R24 | 0xf8;

DAT_mem_002a = (byte)R25R24;

R25R24._0_1_ = DAT_mem_0024;

R25R24._0_1_ = (byte)R25R24 | 3;

DAT_mem_0024 = (byte)R25R24;

bVar2 = DAT_mem_002a;

DAT_mem_002a = bVar2 & 0xfb;

R25R24._0_1_ = DAT_mem_002b;

R25R24._0_1_ = (byte)R25R24 & 7;

DAT_mem_002b = (byte)R25R24;

R25R24._0_1_ = DAT_mem_0025;

R25R24._0_1_ = (byte)R25R24 & 0xfc;

DAT_mem_0025 = (byte)R25R24;

R11 = 0xa5;

R12 = 0;

R13 = '\0';

do {

R25R24._0_1_ = DAT_mem_0029;

R25R24._0_1_ = (byte)R25R24 ^ (byte)R25R24 * '\x02';

if (((byte)R25R24 & 4) == 0) {

auStack_7 = (undefined1 [3])0x141;

z1();

}

else {

R15R14 = 0x68;

R16 = 0;

while( true ) {

Z = (byte *)R15R14;

R25R24._0_1_ = *(byte *)(uint3)R15R14;

if ((byte)R25R24 == 0) break;

Z._1_1_ = (undefined1)(R15R14 >> 8);

Z._0_1_ = (byte)R25R24 ^ R11;

if ((byte)R25R24 == 0xa5) break;

R25R24._0_1_ = DAT_mem_0029;

R25R24._0_1_ = (byte)R25R24 ^ (byte)R25R24 * '\x02';

if (((byte)R25R24 & 4) == 0) {

auStack_7 = (undefined1 [3])0x131;

z1();

break;

}

Z._0_1_ = (byte)Z - 0x30;

R17 = 0;

if ((byte)Z < 0x4e) {

Z = (byte *)CONCAT11(1,(byte)Z);

R17 = *Z;

}

auStack_7 = (undefined1 [3])0x151;

z1();

if ((R17 & 1) != 0) {

bVar2 = DAT_mem_002b;

DAT_mem_002b = bVar2 | 8;

}

if ((R17 & 2) != 0) {

bVar2 = DAT_mem_002b;

DAT_mem_002b = bVar2 | 0x10;

}

if ((R17 & 4) != 0) {

bVar2 = DAT_mem_002b;

DAT_mem_002b = bVar2 | 0x20;

}

if ((R17 & 8) != 0) {

bVar2 = DAT_mem_002b;

DAT_mem_002b = bVar2 | 0x40;

}

if ((R17 & 0x10) != 0) {

bVar2 = DAT_mem_002b;

DAT_mem_002b = bVar2 | 0x80;

}

if ((R17 & 0x20) != 0) {

bVar2 = DAT_mem_0025;

DAT_mem_0025 = bVar2 | 1;

}

if ((R17 & 0x40) != 0) {

bVar2 = DAT_mem_0025;

DAT_mem_0025 = bVar2 | 2;

}

R25R24._0_1_ = R16 & 0x1f;

cVar3 = (byte)R25R24 + 0x2d;

while (cVar1 = cVar3 + -1, cVar3 != '\0') {

Z = (byte *)0xf9f;

do {

Z = (byte *)((int)Z + -1);

cVar3 = cVar1;

} while (Z != (byte *)0x0);

}

R15R14 = CONCAT11(R15R14._1_1_ - (((char)R15R14 != -1) + -1),(char)R15R14 + '\x01');

R16 = R16 + 0x25;

}

*(byte *)(Y + 2) = R1;

*(byte *)(Y + 1) = R1;

while( true ) {

R25R24._0_1_ = *(byte *)(Y + 1);

R25R24._1_1_ = *(char *)(Y + 2);

if (R25R24._1_1_ != '\0' && ((byte)R25R24 < 0x2c) <= (byte)(R25R24._1_1_ - 1U)) break;

R25R24 = *(int *)(Y + 1) + 1;

*(char *)(Y + 2) = R25R24._1_1_;

*(byte *)(Y + 1) = (byte)R25R24;

}

}

if (R12 != R1 || R13 != (byte)(R1 + (R12 < R1))) {

auStack_7 = (undefined1 [3])0x146;

__vectors();

}

} while( true );

} 
```

What happens in here is it begins with a hardware initialization phase, configures by setting specific bits in (SFR's)

The program then enters and infinite execution loop, the location of the main data is located in the codebytes section using 0x68
<img width="1693" height="966" alt="image" src="https://github.com/user-attachments/assets/26e6a966-f6f3-48f9-aa8c-fcbd527cdead" />


On converting this using XOR operation with the 0xA5 key, to get a hex sequence

54 46 43 43 54 46 7B 54 68 31 73 5F 31 73 5F 73 6F 6D 33 5F 73 31 6D 70 6C 33 5F 34 72 64 75 31 6E 6F 5F 66 31 72 6D 77 34 72 65 7D 89 77 6A 6A 36 7A 36

Converting this into asci we get 

TCCTF{h1s_1s_m_l3_4rdu1nof_f1rmw4r7d}





