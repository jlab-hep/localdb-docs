Login DB system before the scan (You can do it once when you start the machine.)
```
$ cd Yarr/src

#######################
#  in the first time  #
#######################
$ source dbLogin.sh <account_name>     # set your account name
User Config file is not exist: /home/kubota/.yarr/kubota_user.json
 
Enter your name (<first name>_<last name>) or 'exit' ... 
<FirstName>_<LastName>     # ex. John_Doe
 
Enter your institution (ABC_Laboratory) or 'exit' ... 
<ABC_Laboratory>
 
Do you want to set identification key? [y/n]
n     # answer 'y' if you want to set identification keyword to distinguish between multiple users with same name in the same machine
 
Logged in User Information
  Account: <account_name>
  Name: <FirstName>_<LastName>
  Institution: <ABC_Laboratory>
  Identity: default
 
Are you sure that's correct? [y/n]
y     # you can login DB system as your account and register your information into local DB
 
Database: Login user: 
	account: <account_name>

Database: Register user's information: 
	user name : <FirstName>_<LastName>
	institution : <ABC_Laboratory>
	user identity : default

Create User Config file: ${HOME}/.yarr/<account_name>_user.json 

###########################
#  after the second time  #
###########################
$ source dbLogin.sh <account_name>     # set your account name
User Config file is exist: ${HOME}/.yarr/<account_name>_user.json
 
Logged in User Information
  Account: <account_name>
  Name: <FirstName>_<LastName>
  Institution: <ABC_Laboratory>
  Identity: default
 
Are you sure that's correct? [y/n]
y
 
Database: Login user: 
	account: <account_name>

Database: Register user's information: 
	user name : <FirstName>_<LastName>
	institution : <ABC_Laboratory>
	user identity : default

Database: Already exist, exit.
 
Create User Config file: ${HOME}/.yarr/<account_name>_user.json 
```