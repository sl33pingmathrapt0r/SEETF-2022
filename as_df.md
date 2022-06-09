# "as" "df"  
Challenge Description: Why use a python interpreter when there are online ones?  
Challenge Author: The Mythologist  
NetCat: nc fun.chall.seetf.sg 50002

In this challenge, we want to retrieve the flag from the online interpreter provided.  
Upon entering the NetCat command into cmd.exe, the following screen appears:  

![Screenshot%202022-06-09%20.png](attachment:Screenshot%202022-06-09%20.png)

Notice: **THERE ARE BLACKLISTS**. This is a jail-break challenge.  
Since this is a PWN challenge, we want to retrieve the flag from the root directory provided over the network. We may first attempt using "os", or define some function to navigate the directories, or just test out a 'for' loop to explore what commands have been blacklisted. 

![Screenshot%202022-06-09%20170801.png](attachment:Screenshot%202022-06-09%20170801.png)

![Screenshot%202022-06-09%20170821.png](attachment:Screenshot%202022-06-09%20170821.png)

We can thus infer that a bad input returns "Your input sucks :(" but *allows you to continue using the interpreter*, but an input with **blacklisted keywords** kicks you out. We can guess that there is a data structure in the program storing the set of keywords. To find it, we use ```globals()``` to view all information stored in the program.  
```globals()``` returns a dictionary, with keys of variable names, or function names etc, and their values. 

![Screenshot%202022-06-09%20171550.png](attachment:Screenshot%202022-06-09%20171550.png)

Clearly, there exists a tuple ```blacklist```. Cross-checking with the tested input above verifies that keywords are checked against this tuple, such as 'os' and ' '.  
Since the interpreter **must** check each input against ```blacklist```, we can assume removing ```blacklist``` from the ```globals()``` dictionary may cause the program to crash. Instead, we shall re-assign ```blacklist``` to an empty tuple.  

From there, we can execute the basic ```os```  methods to find the file in the root directory containing the flag. 

![Screenshot%202022-06-09%20172633.png](attachment:Screenshot%202022-06-09%20172633.png)

We now open the file and retrieve the flag :D

![Screenshot%202022-06-09%20172940.png](attachment:Screenshot%202022-06-09%20172940.png)
