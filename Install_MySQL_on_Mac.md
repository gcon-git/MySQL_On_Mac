## Steps to Install and Use MySQL Locally on Mac 

 
 ### 1. Download MySQL Community Server

 * https://dev.mysql.com/downloads/mysql

 ### 2. Install MySQL Community Server

 * Open the .dmg package file and install MySQL Community Server using the installation wizard.
 * When prompted - enter a password of your choice for the root user of the MySQL Community Server.
    + IMPORTANT!! - Be sure to keep this password and/or store it in your key chain. 
 * Once the installation wizard is complete, check that the server is installed and running on your computer.
    + Go to "System Preferences"
    + Look for "MySQL" with the logo (mine was at the bottom of the System Preferences window) and click it.
    + You should see active and installed instances. If the server is running there will be a green dot next to the active and installed instances.
    + If the server is not running you can click the button to start it. If you have to start the server you will likely be asked to provide a password. That password will most likely be the root user password you created during the installation process. 

### 3. Configure the server to run on the command line in terminal on your computer

* Open terminal
* Type `nano .bash_profile` to open your .bash_profile file
* Move the cursor to the bottom of your .bash_profile file and enter `export PATH=${PATH}:/usr/local/mysql/bin`
    + This exports your MySQL path so that your computer can find where requisite MySQL files are located.
    + WARNING: I do not recommend making any other changes or alterations to your .bash_profile file. Doing so could have negative impacts on other software operations.
* Save and close your .bash_profile file.
* At the terminal prompt, get the new changes in your .bash_profile to take effect by entering `source .bash_profile` 

### 4. Check that MySQL is running correctly and you can use MySQL on the command line
* Type `mysql -u root -p` to start MySQL
    + Enter the root password that you created during installation of MySQL Community Server above
    + If it's installed correctly and your server is working then you should get a MySQL welcome message and prompt that looks like `mysql>`
    + You can check to see what default databases are loaded by entering `show databases;` at the mysql prompt. 
* Exit/quit out of MySQL
    + At the mysql prompt enter `quit;` or `exit`

### 5. Download MySQL Workbench

* https://dev.mysql.com/downloads/workbench/

### 6. Install MySQL Workbench

* Open the .dmg package file and install MySQL Workbench using the installation wizard.
* To install MySQL Workbench, you should be able to simply drag the MySQL icon into the Applications folder icon.
* If prompted, you may have to enter your computer's password for the installation to begin.

### 7. Check that MySQL Workbench installed correctly

* Go to your Applications folder, find MySQLWorkbench, and launch the program.
* Once open, you should see a connection to your local instance. If not, you will need to create a connection.

***

## Miscellaneous

* To change the root password in MySQL from the terminal:
    + Start mysql by typing `mysql -u root -p`
    + Enter your MySQL root user password when prompted
    + At the mysql prompt type `ALTER USER 'root'@'localhost' IDENTIFIED BY '<newpassword>';`
* Add new user(s) / accounts in MySQL Workbench through your root user connection
    + NOTE 1: I added an account for training purposes so as not to affect my root user account.
    + NOTE 2: If you create an account to use for training, projects, etc., you will have to create a new connection for each of those new user(s)/account(s)
    + Go to --> 'Administration' tab,  and click 'Users & Priveleges'
    + Click 'Add Account'
    + Under the 'Login' tab of the new account:
        + Authentication type --> caching_sha2_password
        + Limit to Hosts Maching --> localhost
        + Password --> you can give your new account its own password
        + Confirm password --> retype the same password 
    + Under 'Administrative Roles' tab of the new account:
        + select the roles you want to limit for that user/account 

***

## Troubleshooting 

* If you are having trouble getting MySQL to work on your terminal (Step #4 above) after making the addition to your .bash_profile, try doing the following:
    + Enter `sudo ln -s /usr/local/mysql/bin/mysql/bin/mysql /usr/local/bin`   
        + If/when prompted, enter the password for your computer
        + This creates a symbolic link between the two directories 
* Check the comments section of the videos listed as references. Many commenters provided troubleshooting solutions to problems that others had during installation and set up.