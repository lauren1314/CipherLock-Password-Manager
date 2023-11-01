# CipherLock-Password-Manager
This projects aims to allow users to be able to safely input and retrieve their different online account and passwords through the system once it has been registered and saves into the database


import tkinter as tk #THIS IS FOR THE GUI LIB
import secrets #USED FOR CRYPTOGRAPHY DOUBLE SAFETY
import string 


#FIRST LOGIN PAGE SET LOGIN 
def check_admin_credentials():
#GUI 
    entered_username = admin_username_entry.get() 
    entered_password = admin_password_entry.get()
    
#SET LOGIN CREDENTIALS
    admin_username = "lauren222"
    admin_password = "lauren223"

#WHEN USER LOGINS IN WITH CORRECT DETIALS THE LOGIN PAGE WILL DISSAPEAR

    if entered_username == admin_username and entered_password == admin_password:
        admin_login_window.destroy()
        
#IF LOGIN DETIALS NOT CORRECT (FEEDBACK)    
    else:
       admin_feedback_label.config(text="Invalid admin credentials. Please try again with correct details.")




#USER LOGINREGISTRATION PAGE


def show_user_registration_login_window():
    user_registration_login_window = tk.Toplevel()
    user_registration_login_window.title("User Registration and Login")
    
#GUI
admin_login_window = tk.Tk()
admin_login_window.title("Admin Login")

#WIDGETS-
#LABEL- A widget used to display text on the screen
#ENTRY- A text entry widget that allows only a single line of text
#BUTTON- 
admin_username_label = tk.Label(admin_login_window, text="Admin Username:")
admin_username_entry = tk.Entry(admin_login_window)
admin_password_label = tk.Label(admin_login_window, text="Admin Password:")
admin_password_entry = tk.Entry(admin_login_window, show="*")
admin_login_button = tk.Button(admin_login_window, text="Login", command=check_admin_credentials)
admin_feedback_label = tk.Label(admin_login_window, text="")

#PACK() Helps to organise widgets
#padx, pady -- the number of pixels surrounding the widget to create a padding between other widgets, for horizontal or vertical padding.

admin_username_label.pack(padx=10, pady=5)
admin_username_entry.pack(padx=10, pady=5)
admin_password_label.pack(padx=10, pady=5)
admin_password_entry.pack(padx=10, pady=5)
admin_login_button.pack(padx=10, pady=5)
admin_feedback_label.pack(padx=10, pady=5)

admin_login_window.mainloop()










#own cipher

encrypt_cipher = 'ajsbktcludmvenwfoxgpyhqzir!@#$./&*?9753108642ZQHYPGXOFWNEVMDULCTRBSJARI'
decrypt_cipher = 'ABCDEFGHIJKLMNOPQRSTUVWXYZ1234567890!@#$./&*?abcdefghijklmnopqrstuvwxyz'

#this status shows that not logged in

admin_logged_in = False

#custom because it is my own cipher
#allows both ways for encrypting and decrypting
#index find the matching specififc letter within cipher

def custom_cipher_encrypt(text):
    encrypted_text = ''
    for char in text:
        if char in decrypt_cipher:
            index = decrypt_cipher.index(char)
            encrypted_text += encrypt_cipher[index]
        else:
            encrypted_text += char
    return encrypted_text

def custom_cipher_decrypt(text):
    decrypted_text = ''
    for char in text:
        if char in encrypt_cipher:
            index = encrypt_cipher.index(char)
            decrypted_text += decrypt_cipher[index]
        else:
            decrypted_text += char
    return decrypted_text










#password generator section
#has specifications which matches the strength check

def generate_random_password():
    uppercase_letters = string.ascii_uppercase
    lowercase_letters = string.ascii_lowercase
    special_characters = "!@#$%^&*?"
    digits = string.digits
    
#adds one point everytime it meet criteria, once it adds up to 5, password will be generated
    while True:
        password = ''.join(secrets.choice(uppercase_letters) for _ in range(1))
        password += ''.join(secrets.choice(lowercase_letters) for _ in range(1))
        password += ''.join(secrets.choice(special_characters) for _ in range(1))
        password += ''.join(secrets.choice(digits) for _ in range(1))
        password += ''.join(secrets.choice(uppercase_letters + lowercase_letters + special_characters + digits) for _ in range(6))

        if calculate_password_strength(password) == 5:
            return password
        
# this is a strength checker for registered password, password must pass strength test before user registers

def calculate_password_strength(password):
    uppercase_letters = set(string.ascii_uppercase)
    lowercase_letters = set(string.ascii_lowercase)
    special_characters = set("!@#$%^&*?")
    digits = set(string.digits)

    strength_score = 0
#length
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

#the strength meter adds up everytime criteria has been met
def update_strength_indicator():
    password = password_entry.get()
    strength_score = calculate_password_strength(password)
    strength_label.config(text=f"Strength: {strength_score}/5")

#users username and password gets registered into system. password is encrypted using the cipher as well as secrets lib

def register_user():
    username = username_entry.get()
    password = password_entry.get()

    strength_score = calculate_password_strength(password)
    

    hashed_password = password
    encrypted_password = custom_cipher_encrypt(hashed_password)









    
#created a file that saves all of the registered information. Use a so that everytime a new password has been saved in gets added in.
    
    with open("user_data.txt", "a") as file:
        file.write(f"Username: {username}, Encrypted Password: {encrypted_password}\n")

    feedback_label.config(text="Username and Password registered successfully!")





    

#this specfic code makes sure that users can see the generated password

def toggle_password_visibility():
    if show_password_var.get():
        password_entry.config(show="")
    else:
        password_entry.config(show="*")

# this function allows uses to retrieve their stored password by typing in correct registered username. 
def check_stored_password():
    entered_username = username_entry.get()
    stored_password = None
    
#retrieved from this file
    with open("user_data.txt", "r") as file:
        lines = file.readlines()
        for line in lines:
            stored_username, password = line.strip().split(", ")
            stored_username = stored_username.split(": ")[1]
            password = password.split(": ")[1]
            password = password.replace("Encrypted Password: ", "")
            decrypted_password = custom_cipher_decrypt(password)
            if entered_username == stored_username:
                stored_password = decrypted_password
                break

    if stored_password is not None:
        feedback_label.config(text=f"Stored Password: {stored_password}")
    else:
        feedback_label.config(text="Username or Password has not been registered or incorrect")



#this section if for user login
        
def login_user():
    username = username_entry.get()
    entered_password = password_entry.get()

    with open("user_data.txt", "r") as file:
        lines = file.readlines()
        for line in lines:
            stored_username, stored_password = line.strip().split(", ")
            stored_username = stored_username.split(": ")[1]
            stored_password = stored_password.split(": ")[1]
            stored_password = stored_password.replace("Encrypted Password: ", "")
            decrypted_password = custom_cipher_decrypt(stored_password)
            if username == stored_username and entered_password == decrypted_password:
                feedback_label.config(text="Username and Password correct!")
                return
        feedback_label.config(text="Invalid username or password. Please try again.")

        

# this provides option for users to generate password making sure it fits criteria also allows users to see the generated password in normal letters 

def generate_password():
    generated_password = generate_random_password()
    password_entry.delete(0, tk.END)
    password_entry.insert(0, generated_password)

window = tk.Tk()
window.title("User Registration")

username_label = tk.Label(window, text="Account Username:")
username_entry = tk.Entry(window)
password_label = tk.Label(window, text="Account Password:")
password_entry = tk.Entry(window, show="*")
password_strength_label = tk.Label(window, text="Password Strength:")
strength_label = tk.Label(window, text="Strength: 0/5")
register_button = tk.Button(window, text="Register Data", command=register_user)
login_button = tk.Button(window, text="Check Registered Data", command=login_user)
generate_password_button = tk.Button(window, text="Generate Password", command=generate_password)
feedback_label = tk.Label(window, text="")


username_label.grid(row=0, column=0, padx=10, pady=5, sticky="e")
username_entry.grid(row=0, column=1, padx=10, pady=5)
password_label.grid(row=1, column=0, padx=10, pady=5, sticky="e")
password_entry.grid(row=1, column=1, padx=10, pady=5)
password_strength_label.grid(row=2, column=0, padx=10, pady=5, sticky="e")
strength_label.grid(row=2, column=1, padx=10, pady=5)
generate_password_button.grid(row=6, column=0, columnspan=2, pady=5)
register_button.grid(row=3, column=0, columnspan=2, pady=10)
login_button.grid(row=5, column=0, columnspan=2, pady=5)
feedback_label.grid(row=7, column=0, columnspan=2)

password_entry.bind("<KeyRelease>", lambda event: update_strength_indicator())

show_password_var = tk.BooleanVar()
show_password_checkbox = tk.Checkbutton(window, text="Show Generated Password", variable=show_password_var, command=toggle_password_visibility)
show_password_checkbox.grid(row=8, column=0, columnspan=2, pady=5)

check_password_button = tk.Button(window, text="Check Registered Password for Account", command=check_stored_password)
check_password_button.grid(row=9, column=0, columnspan=2, pady=5)



window.mainloop()
