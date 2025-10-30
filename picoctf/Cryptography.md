# RSA ORACLE
## Flag:  picoCTF{su((3ss_(r@ck1ng_r3@_24bcbc66}
This CTF is around RSA algorith, which is used for encrypting messages. 

## Steps - 

We are provided with 2 files, password.enc and secret.enc. Secret.enc contains the flag but it is encrypted and the password is in ascii, we know this because when we CAT the file we get SALTED__, which is used by aes-256-cbc to decrypt.

To get the contents we need to use a decryption password. This 'password' is again encrypted, the encryption process is as follows - 

text  ------> m = hex ------> cipher = m^(e mod n) (RSA) , we are provided with 'THE ORACLE' that does this encryption and decryption. We cannot just put this 'password' into the ORACLE and decrypt it, because that would be to easy. 

<img width="887" height="137" alt="image" src="https://github.com/user-attachments/assets/0f7b8104-b962-4078-a34d-8a6d5cb48ca0" />


So, I used the principles of modular algebra and concept of RSA, and encryption of 'THE ORALE' where 2^(e mod n) * m^(e mod n) = 2m^(e mod n). While decrypting 'THE ORACLE' decrypts the cipher in hex, now if the cipher multiplied by 2 , then so is its hex , then we can convert the hex into decimal, divide it by 2, then convert it back to hex, and at least hex to ascii. 

To do this i used the python code -

```
from pwn import *

server = remote('titan.picoctf.net', 49448)
response = server.recvuntil('decrypt.')
print(response.decode())

input = b'E' + b'\n'
server.send(input)

response = server.recvuntil('keysize):')
print(response.decode())

input = b'\x02' + b'\n'
server.send(input)
response = server.recvuntil('ciphertext (m ^ e mod n)')
response = server.recvline()
num=int(response.decode())*
2575135950983117315234568522857995277662113128076071837763492069763989760018604733813265929772245292223046288098298720343542517375538185662305577375746934
response = server.recvuntil('decrypt.')
print(response.decode())
input = b'D' + b'\n'
server.send(input)

response = server.recvuntil('decrypt:')
print(response.decode())
server.send(str(num)+'\n')

response = server.recvuntil('hex (c ^ d mod n):')
print(response.decode())
response = server.recvline()
print(response.decode())
```
We get - 
<img width="950" height="665" alt="image" src="https://github.com/user-attachments/assets/01114743-5189-44fb-bb28-d52878eaf2e1" />

Converting this hext to decimal we get 431254456004, dividing it by 2 ,  its 
215627228002. Converting it into hex again its 3234626362, now at last into ascii we get 24bcb. 

Now this is the key to the secret.enc file. Using openssl, to read contents, as it is .enc coded.

<img width="742" height="141" alt="image" src="https://github.com/user-attachments/assets/d1133893-ec84-4d3f-b912-e9b5ef7957d8" />

# Custom Encryption
## Flag:

# mini RSA
## Flag: picoCTF{n33d_a_lArg3r_e_606ce004}
In this challenge, we are provided N, e and c (ciphertext) and we need to crack the cipher. 

## Steps - 
As we bascially know C = M^e mod N , where M is our message, and to get the message M = C^d mod N,. We can find d, using this criteria (d * e) ≡ 1 mod Φ(n). We can run a python script to solve this, i used dcode.com as it has an RSA solver.

<img width="1869" height="1002" alt="image" src="https://github.com/user-attachments/assets/cfe92bcc-af52-41f0-84e9-ca571e6dc2bd" />

