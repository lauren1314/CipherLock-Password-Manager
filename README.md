# CipherLock-Password-Manager
This projects aims to allow users to be able to safely input and retrieve their different online account and passwords through the system once it has been registered and saved into the database. The system is created using Tkinter which is a GUI Library that allows me to add in widgets such as buttons, text boxes which users can interact with. The code also uses libraries such as secrets and strings to asssit me in generating values and letters (passcode generation). 

The code first starts off with important the 3 libraries which i have mentioned above which are Tkinter, Secrets and Strings, these three components are key to creating this entire system and looks of the GUI. i made the system a small widget as i wanted the system to be something that is not too complicated and east to access and that it doesnt fill up the entire home screen. 

Next in the code is the checkin the admin credientials used to login for the user which i have alredy present in this system

admin_username = "lauren222"
admin_password = "lauren223"

The next line makes sure that what is entered in the text box matches the preset credentials and if it does match the user will be able to login and access the other functions of the system. If the credentials entered does not match the presets then it will show "Invalid admin credentials. Please try again with correct details.".

Once the user logs in they will see a new GUI pop up and this is where users are able to register their username and passwords. The GUI has text boxes which allow them to insert the details and have buttons such as "register data", "checked registered data", "generate password", "show generated password" and "check registered password for account". I will go into detail later on for each buttons function. 

now i am going to show you how to use this system and its functions:
The account username and password entry box is where the user enters their existing username/passwords which they have for their different online accounts eg. facebook, youtube or google account passwords. In this case i will register random details as an example 

lauren456
lauren1234

As you can see while i type in the password, there is a feedback lable below the entry box that starts to change, this feedback lable is to provide a  strength test to users for their password. the strength test is out of 5, and it is tested based on the complexity which i also created a preset for: 

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

it consists of having a password length more than 8 digits, having a upper and lower case, special characters and a nubmer. each prerequsitie adds one point. In this case my password only has a strength of 3/5 as i do not have a uppercase or special character. However this does not prevent users from registering their details, it is rather a guideline or recommendation to users. 

Once i input my details in, i press the register data button, which then automatically saves the details into a exisitng database file which i named "user_data". this data base updates everytime i register a new account/ information onto the system. The password that is entered is encrypted into the file using my own created cipher for safety and security. this means that when users go into the file, they can only see the encrypted version of the password and not the original password. it is worthy to note that users can edit/delete registered data through the file, this can be useful when they user had updated their password or account name. 

the next button below is the check registered data button, this button aims to retrieve the registered information within the "user_data" file and that users can double check whether they have already registered previously for this account. if they enter data that has been registered it will show 
"Username and Password Correct"
If it hasnt been registered or they enter the wrong details it will show "Invalid username or passwrod. Please try again"

the generate password button is created using the secrets and strings library, it is a function that generates a random password that meets specified criteria for length, uppercase letters, lowercase letters, special characters, and digits.similarly, once user recieves the generated password they are able to register it into the file database. 

As part of security, the passwrod entered into the entry box are all toggled so that it only shows "*", i put in the option for users to "show generated password" so that they are able to see the password generated. it can also be used to see the password they have entered, so that they can make sure they have entered it correctly. 

Finally, the users can retireve their password if they have forgotten it, this function is called "Check registered password for account", users type in the registered account in the top entry box and then they press the button and it will retireve the information by decrypting the password. the decrypted password will show above the show generated password button.



