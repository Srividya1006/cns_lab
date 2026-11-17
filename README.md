1st 
def encrypt(text, key):
    result = ""
    for ch in text:
        if ch.isalpha():
            base = ord('A') if ch.isupper() else ord('a')
            result += chr((ord(ch)-base+key)%26+base)
        else:
            result += ch
    return result

text = input("Enter Text: ")
key = int(input("Enter Key: "))

cipher = encrypt(text, key)
print("Encrypted:", cipher)
print("Decrypted:", encrypt(cipher, -key))




2nd 

import math

def encrypt(text, key):
    text = text.replace(" ", "").upper()
    rows = math.ceil(len(text)/key)
    text += 'X' * (rows*key-len(text))

    cipher = ""
    for col in range(key):
        for row in range(rows):
            cipher += text[row*key+col]
    return cipher

def decrypt(text, key):
    rows = len(text)//key
    result = ""
    for row in range(rows):
        for col in range(key):
            result += text[col*rows+row]
    return result.rstrip('X')

text = input("Enter Text: ")
key = int(input("Enter Key: "))

cipher = encrypt(text, key)
print("Encrypted:", cipher)
print("Decrypted:", decrypt(cipher, key))


3rd 
from PIL import Image

img = Image.open("cover.png").convert("RGB")
pixels = img.load()

msg = input("Enter Secret Message: ") + "####"
binary = ''.join(format(ord(c), '08b') for c in msg)

i = 0
for y in range(img.height):
    for x in range(img.width):
        p = list(pixels[x, y])
        for n in range(3):
            if i < len(binary):
                p[n] = (p[n] & 254) | int(binary[i])
                i += 1
        pixels[x, y] = tuple(p)
        if i == len(binary):
            break
    if i == len(binary):
        break

if i < len(binary):
    raise ValueError("Image is too small for this message.")

img.save("stego.png")
print("Message Hidden Successfully!")

img = Image.open("stego.png").convert("RGB")
binary = ""

for p in img.getdata():
    for v in p:
        binary += str(v & 1)

msg = ""
for i in range(0, len(binary), 8):
    msg += chr(int(binary[i:i+8], 2))
    if msg.endswith("####"):
        break

print("Hidden Message:", msg[:-4])



4th 

def gcd(a, b):
    while b:
        a, b = b, a % b
    return a

def inverse(a, m):
    for x in range(1, m):
        if (a*x) % m == 1:
            return x
    return None

a = int(input("Enter First Number: "))
b = int(input("Enter Second Number: "))
print("GCD:", gcd(a, b))

a = int(input("Enter Number: "))
m = int(input("Enter Modulus: "))

print("Modular Inverse:", inverse(a, m))


6th 
from Crypto.Cipher import DES

key = b"12345678"

cipher = DES.new(key, DES.MODE_ECB)

text = input("Enter text to encrypt: ")

# DES requires data in blocks of 8 bytes
data = text.encode()
padding = 8 - (len(data) % 8)
data += bytes([padding]) * padding

encrypted = cipher.encrypt(data)

print("Encrypted text:", encrypted.hex())


7th
cbc







ecd

from Crypto.Cipher import AES
from Crypto.Util.Padding import pad, unpad

key = b'1234567890abcdef'
text = input("Enter Text: ")

cipher = AES.new(key, AES.MODE_ECB)
encrypted = cipher.encrypt(pad(text.encode(), 16))

print("Encrypted:", encrypted.hex())

cipher = AES.new(key, AES.MODE_ECB)
decrypted = unpad(cipher.decrypt(encrypted), 16)

print("Decrypted:", decrypted.decode())


