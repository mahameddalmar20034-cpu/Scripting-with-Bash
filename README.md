# Scripting-with-Bash


Shebang Line
Every Bash script should begin with a shebang line #!/bin/bash . This tells the operator which program should interpret the script.


Comments
Comments can be used to explain the function of a script.They are created by placing a # at the start.You can also create a multiline comment by placing a : ' and then after your intended number of lines closing it with a ' . This is useful for clarity and understanding for when collaborating with other people or even revisiting the script.


Running a script from anywhere
You can run a script from anywhere by placing it in the shell $PATH.This is the shell where the system gathers its script from.By placing the script inside a directory in the shell you can simply run it by stating the name.Remember to use the sudo command.
For e.g. : sudo mv greet.sh /usr/local/bin/greet. The  file name was changed for simplicity as that is the command name.

Variables
Variables allow you to store data such as strings, numbers and arrays.They are essential in creating dynamic scripts.This is achieved by using an = sign e.g. greeting="Hello World".To access the value of this variable you append it with a dollar sign this would look like echo $greeting.
e.g count=42 by using no " system identifies it as a number not a string
echo $count
another e.g fruits=("apple", "banana", orange")
echo $fruits
You can also use variable interpolation for e.g. name="Ahmed" 
echo "Hello , $name"


Parameters
Parameters or arugments are used as inputs in the command line.They are accessed through $1 and $2 based on their position .They enable versatility and foster interactiveness. 
for e.g.  echo "Parameter 1 :$1"
 echo "Parameter 2: $2"
echo "Parameter 3: $3"
echo "All Parameters: @"

Arithmetic Expansion
Scripts can be used to carry out arithmetic expansion.This facilities mathematical calculations as well as a level of dynamic scripting.
length=5
width=3
area=$((length * width))
echo "The area is $area"

Arithmetic Expansion with parameters
This adds a layer of interactivity by adding arguments that can be used in the arithmetic process.
length=$1
width=$2
area=$((length * width))
echo "The area is $area"
./script.sh 2 5 





