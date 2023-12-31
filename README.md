# CipherLock-Password-Manager
This projects aims to allow users to be able to safely input and retrieve their different online account and passwords through the system once it has been registered and saved into the database. The system is created using Tkinter which is a GUI Library that allows me to add in widgets such as buttons, text boxes which users can interact with. The code also uses libraries such as secrets and strings to asssit me in generating values and letters (passcode generation). The system has 4 main functions:

- Register account and password details
The user can enter their online account and passwords into the entry box and save it into a user database. The password saved gets encrypted so that even if someone gets access to the save data they are unable to see the original password. this creates double security for the user. The database automatically creates a file into the users dekstop, so there is no need for the user to create a file themselves. Users can also edit the database by removing their saved data if they do wish to update their account details. 

- Password strength checker
When users type in their password, the system automatically runs the password through a password strength test out of /5. The password strength tests where the password has
1 upper case, lower case, special character, number and over 8 characters. This is made to provide guidance for the user

- Password Generator
If user needs assistance in generating a strong password they are able to use the Generate Password function. THe password generator makes sure that their is 8+ characters and has one upper case, lower case, number and special character inside it.

- Password Retrieval
if the user forgets their password or wants to check what password they saved for their account, they are able to retrieve it by entering their registered account username into the entry boxx at the top and press the retrieve registered password button. The encrypted password will then be decrpyted from the database and shown at the botton of the window in red bold letters.


# A3 CipherLock Password Manager 14251476.py
This is the code for my Python System which i have created. This needs to be opened/run using Python IDLE

# tkin.py
After running it, i have used libraries such as Tkinter, Secrets and String which should be downloaded within the Python Library System already.
Just incase if it hasnt been downloaded, this is the code

    pip install secrets
 
    pip install string
 
    pip install tk 


Please make sure they're at the newest version by typing in:
pip v

# user_data.txt
This is the user_data file which i added into the python code, so that when users register their account and password it gets saved into this file. 

# SOURCE CODES

These are the source code that i used and altered to create my code.


**- Generate password -**

Source code 

    import secrets 

    import string

      secure_str = ''.join((secrets.choice(string.ascii_letters) for i in range(8)))

      print(secure_str)

      password = ''.join((secrets.choice(string.ascii_letters + string.digits + string.punctuation) for i in range(8)))

      print(password)

Reference- Hule, A. (2022). Generate Random Strings and Passwords in Python. (Version 3.12.0). [Soruce Code]. PYnative Python Programming. https://pynative.com/python-generate-random-string/

My altered code

    def generate_random_password():
    uppercase_letters = string.ascii_uppercase
    lowercase_letters = string.ascii_lowercase
    special_characters = "!@#$%^&*?"
    digits = string.digits
    

    while True:
        password = ''.join(secrets.choice(uppercase_letters) for _ in range(1))
        password += ''.join(secrets.choice(lowercase_letters) for _ in range(1))
        password += ''.join(secrets.choice(special_characters) for _ in range(1))
        password += ''.join(secrets.choice(digits) for _ in range(1))
        password += ''.join(secrets.choice(uppercase_letters + lowercase_letters + special_characters + digits) for _ in range(6))

        if calculate_password_strength(password) == 5:
            return password
            
**- ADMIN LOGIN PAGE -**
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


My altered code

    def check_admin_credentials():

    entered_username = admin_username_entry.get() 
    
    entered_password = admin_password_entry.get()
    
    admin_username = "lauren222"
    
    admin_password = "lauren223"

    if entered_username == admin_username and entered_password == admin_password:
        admin_login_window.destroy()
         
    else:
       admin_feedback_label.config(text="Invalid admin credentials. Please try again with correct details.")



**- Password Strength Test -**

    def checkPassword(password):

    upperChars, lowerChars, specialChars, digits, length = 0, 0, 0, 0, 0
    
    length = len(password)

    if (length < 6):
        print("Password must be at least 6 characters long!\n")
    else:
        for i in range(0, length):
            if (password[i].isupper()):
                upperChars += 1
            elif (password[i].islower()):
                lowerChars += 1
            elif (password[i].isdigit()):
                digits += 1
            else:
                specialChars += 1

    if (upperChars != 0 and lowerChars != 0 and digits != 0 and specialChars != 0):
        if (length >= 10):
            print("The strength of password is strong.\n")
        else:
            print("The strength of password is medium.\n")
    else:
        if (upperChars == 0):
            print("Password must contain at least one uppercase character!\n")
        if (lowerChars == 0):
            print("Password must contain at least one lowercase character!\n")
        if (specialChars == 0):
            print("Password must contain at least one special character!\n")
        if (digits == 0):
            print("Password must contain at least one digit!\n") 
            password = input("Please enter password: ") checkPassword(password)

Reference - (2023). Python Code Example: check password strength. [Source Code]. CodeVisionz. https://codevisionz.com/lessons/python-check-password-strength/

My Altered code

    def calculate_password_strength(password):
    uppercase_letters = set(string.ascii_uppercase)
    lowercase_letters = set(string.ascii_lowercase)
    special_characters = set("!@#$%^&*?")
    digits = set(string.digits)

    strength_score = 0

    if len(password) >= 8:
        strength_score += 1
        
    if any(c in uppercase_letters for c in password):
        strength_score += 1

    if any(c in lowercase_letters for c in password):
        strength_score += 1

    if any(c in special_characters for c in password):
        strength_score += 1

    if any(c in digits for c in password):
        strength_score += 1

    return strength_score

**- Encryption and Decryption of Cipher -**

Source code 

    def encrypt(word):
   
    encrypted = ''
    
    for char in word:
        
        if char in crypt:
            
            encrypted += crypt[char]
       
        else:
           
            encrypted += char
    
    return encrypted
    
Reference- Quercus. (2023). Encrypt/Decrypt code snippet. [Source Code]. Python Community Forum. https://discuss.python.org/t/encrypt-decrypt-with-custom-dictionary/23574

My altered code


    def custom_cipher_encrypt(text):
    encrypted_text = ''
    for char in text:
        if char in decrypt_cipher:
            index = decrypt_cipher.index(char)
            encrypted_text += encrypt_cipher[index]
        else:
            encrypted_text += char
    return encrypted_text
    
**- Saving and Reading Files -**

This is the webstie where i found out how to save and read files using the Strip and Split Lines. 

Kutaj, P. (2021). Strip And Split Read Lines In Python To Parse Config Files Effectively [Source Code]. Medium. https://pavolkutaj.medium.com/strip-and-split-read-lines-in-python-to-parse-config-files-effectivelly-df903966ecd4

**-Tkinter-**

This is the webstie where i learnt how to use Tkinter to create my GUI

Python. (2023). tkinter — Python interface to Tcl/Tk. (Version 3.12.0) [Source Code]. Python. https://docs.python.org/3/library/tkinter.html

# Referencences

CodeVisionz (2023). Python Code Example: check password strength. [Source Code]. CodeVisionz. https://codevisionz.com/lessons/python-check-password-strength/

Hule, A. (2022). Generate Random Strings and Passwords in Python. (Version 3.12.0). [Soruce Code]. PYnative Python Programming. https://pynative.com/python-generate-random-string/

Jauswal,S. (n.d.). Login Module in Python. JavaTpoint. https://www.javatpoint.com/login-module-in-python

Kutaj, P. (2021). Strip And Split Read Lines In Python To Parse Config Files Effectively [Source Code]. Medium. https://pavolkutaj.medium.com/strip-and-split-read-lines-in-python-to-parse-config-files-effectivelly-df903966ecd4


Quercus. (2023). Encrypt/Decrypt code snippet. [Source Code]. Python Community Forum. https://discuss.python.org/t/encrypt-decrypt-with-custom-dictionary/23574

Python. (2023). tkinter — Python interface to Tcl/Tk. (Version 3.12.0) [Source Code]. Python. https://docs.python.org/3/library/tkinter.html
