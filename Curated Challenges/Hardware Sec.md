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

# Formware 

# Speed thrills but kills

# Gates of Mayhem
