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
perimeter=$((2 * (length * width)))
echo "The area is $area"
echo "The perimeter is $perimeter"
./script.sh 2 5 


If statements
If statements allow you to make decisions by executing different code blocks depending on the condition met.This is carried out using comparison operators such as ge (greater than or equal to) and gt (greater than) or logical operators like && (and) and || (or).
An example is as follows
name="Mahamed"
grade=85
if [ "$name" == Mahamed ] && [ $grade -ge 75 ]  ;then
echo "Hello Mahamed you have passed"
fi
Another example 
grade=85
if [ $grade -gt 70 ]  && [ $grade -lt 90 ]; then
echo "You are getting there keep going"
fi

else and elif
If the conditions fails then else and elif clauses allow for alternatives paths to be executed.That add a layer of depth and versatility.
for example :
grade=1
if [ $grade -ge 90 ];then
echo "Allahumbarak Akhi you smashed it"
elif [ $grade -ge 75 ];then
echo "You smashed it Akhi your getting closer"
elif [ $grade -lt 75 ];then
echo "Keep trying Akhi you will get there InshaAllah"
fi


Nested if statements
They allow for the evaluation of multiple conditions and execution of different code blocks.They allow for handling of complex deicision making scenarios.Further adding a layer of depth and versatility.
age=20
grade=80
if [ $age -ge 18 ]; then
echo "You are eligibile based on age."
if [ $grade -ge 70 ]; then 
echo "You have also qualified based on grade."
echo "You have qualified for the scholarship."
else 
echo "You have not qualified based on grade."
fi
else
echo " You are too young and hence uneligible."
fi


While loops
Can be used for automating tasks and iterating over data.This is done by continuiously executing  a block of code until the conditions are no longer met.
Some examples:
count=4
while [ $count -lt 10 ]; do
echo "Count:$count"
((count++))

fruits=("apple" "banana" "cherry")
index=0
while [ $index -lt ${#fruits[@]} ]; do
echo "Fruit: ${fruits[$index]}"
((index++))
done


For loops
They allow you to iterate over sequence or a range of values.Allows you to execute the code block for each iteration.They are used for arrays ,lists of values and ranges. 
Some examples:
fruits=("Banana" "Blueberry" "Cherry")
for fruits in "${fruits[@]}" ; do
echo "Fruits:$fruits"
done



for number in $(seq 4 9)
do
echo "Number:$number"
done


for (( i=1 ; i<=10 ; i++ )) ; do
echo "Number: $i"
done

Break and continue
Break statement exits the inner most loop its placed in.The continue statement skips the rest of the current iteration for the loop and skips to the next iteration.Both break and continue are useful for finetuning for and while loops.
Here are some examples:

for (( i=1 ; i<=10 ; i++ )) ; do
if [ $i -eq 5 ] ; then
continue
fi
echo "Number:$i"
done

count=2
while true
do
echo "Count:$count"
((count++))
if [ $count -eq 4 ] ;then
break
fi
done

count=2
while [ $count -le 5 ]
do
if [ $count -eq 3 ]
then
((count++))
continue
fi
echo "Count:$count"
((count++))
done



Basics of functions
A function is a reusable block of code inside a script that you can call like a command.You can also pass paramters(arguments) to refine the level of detail.
Here are some examples:

hello_world() {
    echo "Hello, World!"
    }
hello_world



greet_person() {
    local name="$1"
    echo "Hello, $name!"
    }
greet_person "Mahamed"

Positional/Special Parameters
Special parameters are useful for providing additional information about a script.
An example:

print_args() {
    echo "Name of script: "$0""
    echo "Number of arguments(paramters): "$#""
    echo "First parameter:"$1""
    echo "Second parameter: "$2""
    echo "All parameters: "$@""

}

print_args "Boy" "Man" "Alien"


User inputs
An example of an User input is read name.This is an interactive as well as useful way for providing information where the parameter has not been provided.They can be combined with parameters to offer flexibility in how inputs are accepted.
Some example of this:
greet() {
    echo "What is your name?"
    read name
    echo "Hello,$name!"
}

greet

greet() {
    local name
    if [ $# -eq 0 ] ;then
    echo "What is your name?"
    read name 
    
    else
    name="$1"
    echo "Hello, $name!"
    fi
    echo "Hello, $name!"
 }

greet "Dalmar"



Handling bad data
Coniditional statements can be used to validate user inputs to gurantee the criteria is met.Exit codes can be optimised to provide feedback to the user whether a code has been exectued succesfully or not.Also input santization can be carried out using paramater expansion and patent subsitution to clean and transform user inputs to meet the required format.Here are some examples below:

validate_age() {
local age=$1
    if [[ ! $age =~ ^[0-9]+$ ]] ;then
    echo "invalid age: $age is not a valid number"
    return 1
    fi
   if ((age < 18));then
   echo "Sorry you must be at least 18 years old."
   return 1
   fi
   echo "Congrats at $age your eligible to vote!"
   return 0
}

validate_age "17"

sanatize_string(){
local input="$1" 
local sanatized_input=${input//[^a-zA-Z0-9]/}
echo "$sanatized_input"

}

echo "Please enter a username:"
read input_username
sanatized_username=$(sanatize_string "$input_username")
echo "Sanitized username: $sanatized_username"


Piping
Piping allows you to pass the output of a command as the input of the other command.Allows the execution of advanced data operation ands store the results in variables.It can be combined with other commands or functions  for more complex data manipulation pipelines. Here are some examples:

get_filecount() {
    local directory=$1
    local file_count
    file_count=$(ls $directory | wc -l)
    echo "The number of files in $directory is $file_count"

}
 get_filecount "./"


 search_logs() {
    local search_term="$1"
    grep "$search_term" Arena | awk '{ print $2 }'
}

search_logs "error"


Introduction to error handling
Error handling is useful for preventing crashes whilst giving you feedback.It makes your scripts reliable,safer and easier to use.Here is an example:

num1=17
num2=0
if [ $num2 -eq 0 ]; then
echo "Error:Division by is zero is not possible."
exit 1
fi
result=$((num1 / num2))

echo "The result is: $result"





















