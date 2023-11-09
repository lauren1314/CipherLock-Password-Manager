# CipherLock-Password-Manager
This projects aims to allow users to be able to safely input and retrieve their different online account and passwords through the system once it has been registered and saved into the database. The system is created using Tkinter which is a GUI Library that allows me to add in widgets such as buttons, text boxes which users can interact with. The code also uses libraries such as secrets and strings to asssit me in generating values and letters (passcode generation). 

# A3 CipherLock Password Manager 14251476.py
This is the code for my Python System which i have created. This needs to be opened/run ussing Python IDLE

# tkin.py
After running it, i have used libraries such as Tkinter, Secrets and String which should be downloaded within the Python Library System already.
Just incase if it hasnt been downloaded, this is the code

pip install secrets

pip install strings

pip install tk

Please make sure they're at the newest version by typing in:
pip v

# user_data.txt
This is the user_data file which i added into the python code, so that when users register their account and password it gets saved into this file. 

# SOURCE CODE USED

**- ADMIN LOGIN PAGE- **
SOURCE CODE 
  
def login():  
    username = input("Enter your username: ")  
    password = input("Enter your password: ")  
  
    if username in users and users[username] == password:  
        print("Login successful!")  
    else:  
        print("Invalid username or password. Please try again.")  
  
login()  
Reference-  Jauswal,S. (n.d.). Login Module in Python. JavaTpoint. https://www.javatpoint.com/login-module-in-python

**- Encryption and Decryption of Cipher- **
Soruce code 

def encrypt(word):
    encrypted = ''
    for char in word:
        if char in crypt:
            encrypted += crypt[char]
        else:
            encrypted += char
    return encrypted
Reference- Quercus. (2023). Encrypt/Decrypt code snippet. [Source Code]. Python Community Forum. https://discuss.python.org/t/encrypt-decrypt-with-custom-dictionary/23574

**- Generate password -**
Source code 

import secrets
import string
secure_str = ''.join((secrets.choice(string.ascii_letters) for i in range(8)))
print(secure_str)
password = ''.join((secrets.choice(string.ascii_letters + string.digits + string.punctuation) for i in range(8)))
print(password)

Reference- Hule, A. (2022). Generate Random Strings and Passwords in Python. [Soruce Code]. PYnative Python Programming. https://pynative.com/python-generate-random-string/

