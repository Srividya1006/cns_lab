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
