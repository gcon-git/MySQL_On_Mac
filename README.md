## About this project

This project provides the steps necessary to install and use MySQL 8.0 on a personal computer using MacOS 10.15. 

I had to review/research several YouTube videos, StackOverflow posts, blog posts and other resources online to find the necessary requirements & steps to setup MySQL 8.0 on my own computer. 

I wanted to capture & share the steps that I used in one location to help others get started and potentially avoid the same degree of confusion I initially encountered.

This README file provides the references that were most helpful to me while trying to capture the steps that I used for the installation and initial set up. The *Configuring_MySQL_To_Use_Local_Files.md* file contains additional references used to help capture the steps I took to configure MySQL to allow for local data import/export operations.

## General

One should be able to download, install, and setup MySQL using only the provided steps. However, the referenced videos can provide a visual walk through for you to familiarize yourself with the steps and associated screen actions, etc. It may be helpful to have the steps provided in this repository handy to refer to while watching the videos.

## References

The following are the principle references that provide most, if not all, of the steps needed to install the software needed. 

* YouTube video (20 min : 11 sec):  "How To Install MySQL on Mac OS X", by ProgrammingKnowledge, dated Aug 8, 2017 at https://www.youtube.com/watch?v=UcpHkYfWarM
* YouTube video (6 min : 20 sec): "How to install mysql and workbench on Mac", by Tina, dated Apr 30, 2017 at https://www.youtube.com/watch?v=-TSFLhlGY1k
* YouTube video (12 min : 16 sec): "MacOSX Install MySQL and Workbench", by idtprof, dated Sep 17, 2018 at https://www.youtube.com/watch?v=zbK8cNS_cg0
* 2.4. Installing MySQL on macOS, *MySQL 8.0 Reference Manual*, https://dev.mysql.com/doc/refman/8.0/en/osx-installation.html

Not all of the videos used the current Mac OSx (Catalina 10.15.4) to demonstrate the steps for installation and/or setup. As such, there was some slight variation that I experienced when installing and setting up MySQL Community Server on my own computer. I've tried to capture the relevant steps that I used to install and set up MySQL for use on my own Mac.

## Why this project / my requirements

* Keep/Use MySQL Workbench
    + faster speeds
    + native features
    + more/full feature set
    + open-source - available for free
* Ability to use MySQL on my local machine
    + web access not required once installed
    + can research and experiment with integrating with other software already installed on my computer (ex. R, Python, VSCode, etc.)
    + can download datasets from multiple sources (i.e., Kaggle.com, webscrape, etc.) and import them into MySQL for further practice

## Background

I needed a way to practice writing & using SQL at home to keep my skills fresh and/or learn more about using SQL. I used MySQL Workbench in grad school and our professor(s) provided the information to connect to a server and the respective database we used for class/homework. However, after finishing grad school, I no longer had access to the server and/or databases. Therefore, I needed to find a way to connect MySQL Workbench to my local machine.

I didn't have a server and don't really know anything about them other than what they generally are. Since I didn't have a server, I tried a couple of alternate ways to practice using SQL/MySQL. Here are some of the things I tried (and used):
    
* *sqldf* package in R/RStudio 
    + works but it's slower than using an "organic" SQL platform if data is loaded into memory
    + does work well if connected to a SQL database 
    + large and/or multiple data sets can be problematic because of R's memory management
    + requires other package dependencies
    + required extra effort on my end to format queries in a more readable way
* Mode studio (found here:  https://mode.com/compare-plans/)
    + free account available 
    + has good learning resources
    + I wanted something local-based and not web-based

## Lesson(s) Learned

To use MySQL locally on your home computer/laptop requires two downloads/installations:

* MySQL Community Server
* MySQL Workbench

## Software Utilized / Installed 

* Mac OSx Catalina v10.15.4
* MySQL v8.0.19