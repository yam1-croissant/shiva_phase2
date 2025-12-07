# I like logic more

## Flag: HTB{unp2073c73d_532141_p2070c015_0n_53cu23_d3vic3s}

## Steps - 

With the given hint that the description talks about microsd it might be a MicroSD protocol decoding (SPI mode) . Using Logic 2 we see 4 channels -

<img width="1753" height="853" alt="image" src="https://github.com/user-attachments/assets/df5beaea-0425-46e3-9e92-abfa3aac0e60" />

<img width="1882" height="858" alt="f8bfd75c-8b5c-49ca-906d-69beca0d96d9" src="https://github.com/user-attachments/assets/10f0c31c-94cf-4691-bd60-aabd60809add" />

In SPI communication their 4 channels are MOSI, MISO, CS and CLK. They have their own unique waveforms

CLK - usually goes from 0-1-0-1-0-1 and flips rapidly ,so D3 channel matches it

CS - is usually high most of the time and then low when a command is being sent so that would be D2 Channel [ dont be fooled, scroll more to the side you'll see its mostly high]

MOSI - it changes during clock pulses when CS is low so , D1 Channel


MISO - shows bursts of data AFTER the MOSI command so , D0 Channel

After understanding and choosing the right channels, with the help of SPI (spy) analyzer we get this

<img width="1860" height="938" alt="image" src="https://github.com/user-attachments/assets/e86ce39b-d5e3-4d68-a416-b7f959bbc242" />

After that by changing to ascii, and scrolling through a whole lot of data 

<img width="475" height="758" alt="image" src="https://github.com/user-attachments/assets/fdf53e74-f8fa-40ec-b6a5-9f3825c21083" />
so we get this -

<img width="292" height="681" alt="image" src="https://github.com/user-attachments/assets/69917ff2-752f-4406-ad56-82b9a075656c" />
<img width="331" height="403" alt="image" src="https://github.com/user-attachments/assets/841cb0fc-3657-43fc-ba59-e3c758b5a5a0" />

```
HTB{unp2073c73d_532141_p2070c015_0n_53cu23_d3vic3s}
```
# Red Devil

## Flag: HTB{RF_H4ck1n6_1s_c00l!!!}

## Steps - 

The file given to us was a .cf32 file which on researching is a complex float 32 IQ data, its basically radio samples . To access the file i used Inspectrum and then URH ( universal radio hacker). With inspectrium i had no breakthrough so i switched to URH.

I first thought it was FSK but after a little hit and trial i got that it is ASK, as with FSK or PSK the bits i was getting were either entirely only 1's or 0's .

<img width="791" height="423" alt="image" src="https://github.com/user-attachments/assets/384a7f36-f733-46ec-b394-d7984a92ed76" />

Under "analysis" i then checked from bits to ASCII and from NRZ to Mancherster II as the hint red devils and 'foot ball team' made sense. 

<img width="798" height="397" alt="image" src="https://github.com/user-attachments/assets/d14b6906-be0a-4f38-8766-02493a780778" />


<img width="783" height="409" alt="image" src="https://github.com/user-attachments/assets/65ef0c01-81f9-4c41-a873-7dc7073d3b51" />


# Formware 

## Flag: HTB{N0w_Y0u_C4n_L0g1n}

## Steps: 

After extracting files from the zip file, i tried going through them thats when i got this 
<img width="492" height="276" alt="image" src="https://github.com/user-attachments/assets/bc8e9d87-9404-445c-9a7d-4fc1d5aa30e4" />

I did 

```
binwalk rootfs
```
which gave me the info i needed

<img width="947" height="263" alt="d773fad0-9330-4f9e-a719-bd8d455fe3c3" src="https://github.com/user-attachments/assets/bf1d2a10-f679-4e84-8966-e032842766aa" />

i installed squashfs tools, and after reading through the manual i did

```
unsquashfs rootfs
```

After extracting the files which i could ( some of it couldnt cuz of perms) i used grep

```
grep -R "{" -n .
```
<img width="927" height="885" alt="image" src="https://github.com/user-attachments/assets/1cf8afe0-3a8e-4889-a897-38cc5c2f90dc" />

here i got the flag.

# Speed thrills but kills

## Flag: HTB{v1n_c42_h4ck1n9_15_1337!*0^}

## Steps: 
we are given a .sal file on opening we get

<img width="1860" height="782" alt="image" src="https://github.com/user-attachments/assets/fccba864-aa0a-43b6-8e9c-f61308bd092f" />

We see 2 channels wires, CAN - H and CAN - L and it has a voltage diffential 
its baud rate is in the range 125K, 250K, 500K etc etc

First we need to calculate the baud rate (bit rate) , to use a analyzer (CAN) - 

Baud rate = 1 / bit width ( smallest)

so here its 1 / 7.64 micro secs = 130,890 so the closest Baud rate is 125,000 

<img width="672" height="430" alt="image" src="https://github.com/user-attachments/assets/7206f0b8-7d24-4d49-9057-23d1ee14890a" />

<img width="1425" height="247" alt="image" src="https://github.com/user-attachments/assets/83c285a5-47e7-4a93-a2a6-27d04f366ab7" />

After going through the data, i found the other parts of the flag. 

<img width="337" height="574" alt="image" src="https://github.com/user-attachments/assets/5b585255-a106-4ab9-888b-6fbc7950dab5" />

<img width="342" height="584" alt="image" src="https://github.com/user-attachments/assets/c7a9741e-0486-4741-a029-d1e6ad487bef" />

```
HTB{v1n_c42_h4ck1n9_15_1337!*0^}
```
# Gates of Mayhem

## Flag: 011000110110100101101001101000111010000110100001110101010110110011110110011000100110100101101101100111100100001110001110011101101100001100011110110001110001101111111011001110110000011011101000001101111111000110011011011100101101111111011010011011000001000011110111000110011001110001010111110111011000111100100000111000011001001100010000110001011001010010011101000100110110111011100010001011101101101010101111


## Steps: 

<img width="1160" height="759" alt="image" src="https://github.com/user-attachments/assets/55fe8de6-97ab-4b77-b931-44a876c6ce0e" />


The transistors are placed such that they form logic gates ( Resistor - Transistor Logic)

https://docs.google.com/spreadsheets/d/1LlSutEi1KJd9pugVLaHP2_mlvtbURqGiuXwl28nqYmc/edit?usp=sharing

<img width="587" height="668" alt="image" src="https://github.com/user-attachments/assets/250f6e1b-37b9-495e-9607-b6c5db5b9977" />

<img width="575" height="539" alt="image" src="https://github.com/user-attachments/assets/37384e1c-e86b-4514-b52a-011d8b2e4bfe" />

<img width="517" height="522" alt="image" src="https://github.com/user-attachments/assets/2463c936-fa4f-45c1-9402-176c5e6b24bb" />
