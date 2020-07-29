## Steps to Configure MySQL 8.0 to Use Local Files

### References

1. *Setting secure_file_priv to local folder in MySQL 8.0 (Mac OSX)*, Minnow's answer dtd 01/25/2019, https://stackoverflow.com/questions/51996401/setting-secure-file-priv-to-local-folder-in-mysql-8-0-mac-osx

2. Installing and Using the MySQL Launch Daemon, *MySQL 8.0 Reference Manual*, 
   section - 2.4.3, https://dev.mysql.com/doc/refman/8.0/en/osx-installation-launchd.html

***
### General 

1. Loading data from a local file into a table using MySQL 8.0 is not as straightforward as it once was when using previous versions. To enable the ability to load data from local files, one must change the default settings for two variables in MySQL 8.0: the  `secure_file_priv` and the `local_infile` variables.

2. According to the MySQL 8.0 Reference manual:
   - `secure_file_priv` is a system variable that limits import & export operations to a specific directory (see section 2.10.1) However, it is not a dynamic variable (see chart on page 636), which means that it cannot be set at runtime.
   - `local_infile` is a dynamic variable. It is a system variable that allows or refuses to allow the use of `LOAD DATA LOCAL` statements (see page 223).

3. In MySQL 8.0, `local_infile` is disabled and `secure_file_priv` does not have a directory associated by default. 

4. To check your currect settings for both variables use the following MySQL statements:  
   `SHOW VARIABLES LIKE local infile;`

   `SHOW VARABLES LIKE secure_file_priv;`

*** 
### Assumptions

The following steps assume that you are the owner/administrator of both the machine that you are using and the MySQL server that you are working with, and that you have the requisite access rights to each of them.

***
### Steps to configure/set `secure_file_priv` variable

* Using Terminal, navigate to your installed MySQL files and view the contents


      >> cd /usr/local/mysql-8.0.19-macos10.15-x86_64/

      >> ls 

![](https://github.com/gcon-git/MySQL_On_Mac/blob/master/img_files/nav_to_directory.png?raw=true)

* Create a directory for local data files 

      >> mkdir [somedirectoryname]

   + This will be the directory where you will put the local data files that you wish to use for your MySQL session.

   + In the above screen shot, you'll see where I have already created a directory called *mylocaldata/*. 


* Open the com.oracle.oss.mysql.mysqld.plist file

      >> sudo nano /Library/LaunchDaemons/com.oracle.oss.mysql.mysqld.plist

![](https://github.com/gcon-git/MySQL_On_Mac/blob/master/img_files/open_plist.png?raw=true)

* In the .plist file, set the `secure_file_priv` variable to the directory that you created above to allow for local data import/export operations.

* Below you'll see an opened .plist file. At the bottom of the file, under the `<array>`section, you'll see the line where I set the `secure_file_priv` variable to the directory where I will place my local data files. Set the variable using your directory path accordingly and then save and close the file.

![](https://github.com/gcon-git/MySQL_On_Mac/blob/master/img_files/set_secure_file_priv_var.png?raw=true)

* If you have installed and set up your MySQL server and Workbench then you can check to ensure that your changes took effect.

![](https://github.com/gcon-git/MySQL_On_Mac/blob/master/img_files/check_secure_file_priv_var.png?raw=true)

***
### Steps to configure/set `local_infile` variable

* Setting the `local_infile` variable is a little easier. Using MySQL Workbench, you can simply enter the following statement in a query window:

      >> SET GLOBAL local_infile=1;

* To ensure that I didn't have to re-enter the above command in a future session, I persisted the variable setting. 

   + As your MySQL server administrator, under the "Administration" tab click "Status and System Variables".

   + In the right/main window, click the "System Variables" tab.

   + Under the "Category" (left) column, click "Other".

   + On the right side window, scroll down until you find "local_infile" and click the box next to it. 

![](https://github.com/gcon-git/MySQL_On_Mac/blob/master/img_files/persist_local_infile_var.png?raw=true)

* Finally, again using MySQL Workbench, you can check that your change(s) took effect

![](https://github.com/gcon-git/MySQL_On_Mac/blob/master/img_files/check_local_infile_var.png?raw=true)

***
### Notes

1. Terminal and Finder can both be used to navigate to and/or create the requisite directory. 

2. The LaunchDaemons .plist file for MySQL 8.0 should be located in your /Library/LaunchDaemons/ directory.  

3. When setting the `secure_file_priv` variable, I was unable to designate a directory in my Documents folder on my machine. Even though I entered the path correctly, MySQL did not recognize that particular directory for `LOAD LOCAL DATA` operations. My theory is that the target directory was "outside" of the MySQL server environment. However, when I created a data-related directory in the /usr/local/mysql/ directory everything now works as intended.  

4. Many other blog posts, stackoverflow posts, etc make reference to configuration file called my.cnf. This file does not exist when installing MySQL 8.0 on macOS. The majority of websites that I reviewed in researching how to enable local data file use indicated that the my.cnf file discussions only pertained to Windows users. None of the material discussed for configuring a my.cnf file proved helpful when working with a macOS.