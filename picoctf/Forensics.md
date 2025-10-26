# trivial flag transfer protocol
## Flag: picoCTF
# tunn3l v1s10n
## Flag: picoCTF{qu1t3_a_v13w_2020}
In this challenge we were given a corrupt BMP file, we had to fix it and find the flag.
## Steps- 
I used hexedit to check the file's hex and then compared it with another bmp file's hex, there i noticed a difference
and on editing the hex i was able to open the image
![WhatsApp Image 2025-10-27 at 00 06 55](https://github.com/user-attachments/assets/9f36fbbf-780c-43bc-b14b-78c76764b49e)

![WhatsApp Image 2025-10-27 at 00 16 05](https://github.com/user-attachments/assets/7d71fb64-51c6-40dc-832e-03fd82854d50)

I then changed the hex - 

![WhatsApp Image 2025-10-27 at 00 13 55](https://github.com/user-attachments/assets/25b00bd8-4022-41a6-babe-015f5a10b1b9)

I was able to open the file 

![WhatsApp Image 2025-10-27 at 00 18 13](https://github.com/user-attachments/assets/6ec336fe-8252-4877-85f5-30aa3d8a7cb9)

As it looked like it was a cut of a bigger image, i tried changing the height of the file, to find the file's heigh
i used exiftool. Once i found the height i started changing the height. 

<img width="544" height="599" alt="image" src="https://github.com/user-attachments/assets/a16732fc-50d0-4e2a-8667-e8a5728a4426" />

After setting the height to 900 which was 0384 in hex, I got the flag,

<img width="723" height="660" alt="image" src="https://github.com/user-attachments/assets/8f7b1896-41f4-4d10-8aea-6210891c1a23" />


# m00n wa1lk 
## Flag: picoCTF{beep_boop_im_in_space}

In this CTF, we are provided an audio file, and we have to get the flag hidden in it. 

# Steps - 

I first put the audio file in Sonic-visualiser, and appled the spectogrpah layer, to see for any hidden texts in it.

<img width="1279" height="932" alt="image" src="https://github.com/user-attachments/assets/5d97b8ec-1ee1-4e48-9b78-fd7d0377e6ad" />

It looks like a sstv signal, where an image could be hidden, so i use a program called sstv that extracts the picture from the audio file.

<img width="1913" height="109" alt="image" src="https://github.com/user-attachments/assets/f4b149f4-2ae7-42a3-8b08-11e1df073084" />


Rewarded with the flag - 

<img width="834" height="644" alt="image" src="https://github.com/user-attachments/assets/7663eb8d-1642-4d19-8fe2-08d0fb8eb3db" />

