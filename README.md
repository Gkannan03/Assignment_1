# Assignment_1

PROBLEM
To create Registration and Login system using Python, file handling


Step:1     Registration 
Conditions to create Username:
1. Email/username should have "@" and followed by ".", Eg:  sherlock@gmail.com
2. There should not be any "." immediate next to "@"  Eg: @gmail.com
3. It should not start with special characters and numbers  Eg: 123#@gmail.com

*****
    def User_name(Username):
        U_name='Pass'
        y = list(map(str, Username))
        if y[0].isalpha():
            if '@' in y and '.' in y:
                if (y[y.index('@') + 1]) != '.':
                    if ' ' not in y:
                        U_name = 'Pass'
                    else:
                        U_name = 'Fail'
                        print('space character not allowed, Try again')
                else:
                    U_name = 'Fail'
                    print('\'@\' should not followed by \'.\', Try again')
            else:
                U_name = 'Fail'
                print('. and @ character missing, Try again')
        else:
            U_name = 'Fail'
            print('should not start with special characters and numbers, Try again')

          # reading username in file if exists of not, if same username exist in file, request the user for different username

        if U_name == 'Pass':
            file = open('Login_database.txt', 'r+')
            for rd in file:
                if Username in rd:
                    print('Username already exists, Try another username')
                    file.close()
                    break
            else:
                return U_name
            
  *****

Conditions to create Password:
1. Length should be 5 < password length > 16
2. Must have minimum one special character
3. Must have minimum one one digit
4. Must have minimum one uppercase
5. Must have minimum one lowercase character


*****
    def Pass_word(Password):
        Spl_character = ['#', '@', '_', '-', '!', '$', '%', '&', '*', '(', ')', '<', '>', '?', '/', '|', '}', '{', ':', '[', ']', '^']
        Password_test = 'Pass'

        if len(Password) >= 5 and len(Password) <= 16:
            for i in Password:
                if i.isupper() == True:
                    break
            else:
                Password_test = 'Fail'
                print('Password must contain atleast one upper character')

            for j in Password:
                if j.islower() == True:
                    break
            else:
                Password_test = 'Fail'
                print('Password must contain atleast one lower character')

            for k in Password:
                if k.isdigit() == True:
                    break
            else:
                Password_test = 'Fail'
                print('Password must contain atleast one number character')

            for l in Password:
                if l in Spl_character:
                    break
            else:
                Password_test = 'Fail'
                print('Password must contain atleast one special character')

            for m in Password:
                if m != ' ':
                    continue
                else:
                    Password_test = 'Fail'
                    print('Password should not contain space character')
                    break

        else:
            Password_test = 'Fail'
            print('Password Length should between 5 to 16')
        if Password_test == 'Pass':
            return Password_test
        else:
            print ('Try again')

  *****

Step:2      Storing Username and Password in a text file
1. Once the username and password are validated, store that data in a file

*****
# Registering Username and Password into the file

    def Register():
        file1 = open('Login_database.txt', 'a')
        file1.write(x)                         # x is the Username
        file1.write(',')
        file1.write(y)                         # y is the Password
        file1.write(',')
        file1.write(se1)                       # se1 is the security qn 1 answer
        file1.write(',')
        file1.write(se2)                       # se2 is the security qn 2 answer
        file1.write('\n')
        file1.close()
        return ('Registered succesfully')

    *****


    print('Enter 1 for Login, Enter 2 for Register')
    x=int(input('Enter the number Login\ Register: '))

    #Registration
    if x == 2:
        # Creating a text file to store the data
        import os.path
        if os.path.exists('Login_database.txt'):
            pass
        else:
            f = open('Login_database.txt', 'x')
            f.close()

        #Getting username input
        x=input('Enter Username: ')
        User_id=User_name(x)
        if User_id=='Pass':
            print('Username OK')

        if User_id == 'Pass':
            #Getting Password input
            y=input('Enter Password: ')
            P_w=Pass_word(y)
            if P_w=='Pass':
                print('Password OK')

        if User_id == 'Pass' and P_w == 'Pass':
            # Security question used for retrieving password
            se1 = input('What is your favourite color? ')
            se2 = input('What is your place of birth? ')
            Reg = Register()
            print(Reg)


Step: 3
1. Login, check whether his/her credentials exist in the file or not based on the user input. If it doesn’t exist then ask them to go for Registration
2. If they have chosen forget password you should be able to retrieve their original password based on their username provided in the user input
or else you can ask them to provide a new password
3. If nothing matches in your file you should ask them to Registration

*****
    #Login
    if x==1:
        Username = input('Enter Username: ')
        Password = input('Enter Password: ')
        file= open('Login_database.txt', 'r+')
        m=0
        n=0

        # Reading the Login database file for username and password
        for p in file:
            q=p.replace("\n",'')
            r=q.split(',')
            for s in r:
                if s==Username:
                    m = m+1
                    break
            for t in r:
                if t==Password:
                    n = n+1
                    break
        file.close()
        if m>0 and n>0:
            print('Logged in Successfully')
        if m==0:
            print('Not Registered yet, Please Register')
        if m>0 and n==0:
            print('Enter 1 for Forgot password, Enter 2 for Retrieving old password')


            y=int(input())

            # Forgot password- New password creation block

            if y==1:
                U_name1=input('Enter Username: ')
                if U_name1==Username:
                    y= input('Enter a password: ')
                    P_w=Pass_word(y)
                    with open('Login_database.txt', 'r+') as file1:
                        lines=file1.readlines()
                        for ap in lines:
                            if Username in ap:
                                id=lines.index(ap)
                                print(id)
                                list_items=ap.split(',')
                                print(list_items)
                                list_items[1]=y
                                new_pass=(list_items[0] + ',' + list_items[1] + ',' + list_items[2] + ',' + list_items[3])
                                print(ap)
                    lines[id]=new_pass
                    print(lines)
                    with open('Login_database.txt', 'w') as file2:
                        file2.writelines(lines)
                        print('Password changed successfully')
                else:
                    print('Username wrong, Enter correctly')
            # Old password retrieval block
            elif y==2:
                U_name1 = input('Enter Username: ')
                if U_name1==Username:
                    se1 = input('What is your favourite color? ')
                    se2 = input('What is your place of birth? ')
                    with open('Login_database.txt', 'r+') as file1:
                        lines=file1.readlines()
                        for p in lines:
                            if Username in p:
                                ap=p.replace('\n','')
                                list_item=ap.split(',')
                                if list_item[0]==Username:
                                    if list_item[2]==se1:
                                        if list_item[3]==se2:
                                            print('Password is: ', list_item[1])
                                        else:
                                            print('Wrong Answer, Try forget password')
                                    else:
                                        print('Wrong Answer, Try forget password')
                                else:
                                    print('Wrong Answer, Try for new password')
                else:
                    print('Username wrong, Enter correctly')
 
 *****




