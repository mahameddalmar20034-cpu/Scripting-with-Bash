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


Exit codes
Knowing how to use exit codes correctly is a critical part of handling scripts. "?$" is used to to see the exit code of the last command executed.A non zero exit code means it was unsuccesful and vice versa.Here -v is used to search for a variable in this case a command.-F can be used to search for a file. An example is as follows:

command -v git 2>/dev/null
if [[?$ -ne 0 ]]; then
echo "Git is not istalled. Please install Git."
exit 1
else
echo "Git is installed."
fi



Set -e 
What this command does is end the script as soon as there is a non zero exit code  following a failed command.It prevents the rest of the script from being executed.This is essential as it proctects the system and allows for easy debugging.However sometimes there is a non zero exit code but we still want the rest of the script to execeute so it isnt always necessary.An example of this:


set -e
echo "Before the script"
Nonexistantcommand
echo "After the script"

 Set -u
 This ends the script at the undefined variable.Hence this can be used to identify a variable that is undefined.This is useful for preventing running into potential issues due to missing data.Overall its useful for reliability and easy debugging.An example is as follows:

set -u
x=5
y=10
z=$(( x + y + w))
echo "z=$z"

Set -x
This is useful for tracing the flow of the script.It prints each command before executing aswell as expanding variables.This is practical for debugging and when handling sensitive code to allow you to spot errors and retrace your steps.An example is as follows:


set -x
echo "This is the start of the script."
X=5
Y=7
Z=$((X+Y))
echo "The value of Z is:$Z"
set +x
echo "This is the end of the script bye."

Set -eux 
All three can be combined to make debugging much easier and handling the scripts safer preventing the propagation of error.However this should only be done meticulously considering the specific requirements and context of the script.

Additional Set commands

There are more set commands like set -o nounset which behaves identical to set -u as well as set -o errexit which behaves identical to set -e.A new example is set -o pipefail how it works is that it ends the scrip where the pipefails the exit code of the pipe is whatever the last command is.Sometimes in a pipe if the second command runs no matter if the first one still doesnt the exit code is 0.However the command set -o pipefail prevents this with the pipe ending with the first fail.This allows for safer and more reliable scripts.

set -o pipefail
cat nonexiste | grep "something"
echo "exit code: $?"



Change Path permanently

You can write your own commands and execute them from anywhere.By adding your command to the $PATH shell.By adding your directory containing the file to your script using echo "export PATH=$PATH:~/Thescripts" >> ~/.zshrc followed by source.zshrc.This can be used to further enhances work efficency and bolstering productivity.



Reading Enviroment Variables/Standard Enviromental Variables
Enviromental variables are stored settings within the operating that provide the shell key information to the shell and programs.By looking at them it provide valuable insights for example the system and user .It can be used within the bash script to store and retrieve important information within the bash script.You can also  assign  local variables to make it more readable.Here are some examples:

my_user=$USER
my_os=$OSTYPE
my_home=$HOME

echo "Home is $my_home"
echo "User is $my_user"
echo "OS is $my_os"

echo "Username: $LOGNAME"
echo "Current Directory: $PWD"
echo "Shell: $SHELL"

echo "Executable Paths:$PATH"
echo "Default Language:$LANG"

Reading Files
While loops and redirection can be used to read the contents of a file line by line.This can also be done using the cat command and then piping it to generate each line one by one.This is a vital skill.Here are some examples:


#!/bin/bash
read_file() {
    local file_path=$1
    while ifs= read -r line; do
    echo "$line"
    done < "$file_path"
}
read_file "if.sh"



process_file() {
    local file_path="$1"
    cat "$file_path" | while IFS= read -r line; do
    #processing line 
    echo "Processing line: $line"
    done

}
process_file "if.sh"


Writing Files
Redirection (>) can be used to create a new file or overwrite the contents of a file.Appending (>>) allows you to add without overwriting content to a already existing file.Here is an example:

#!/bin/bash
write_file() {
    local file_path="$1"
    local data="$2"
    echo "$data" >> "$file_path"
}
write_file "if.sh" "Hey!"

File Checksums
A checksum is the files unique fingerprint.You can different alogrithims such as md5sum and sha256sum to check the checksum of a file.You can compare checksums to test the integrity and authenticity of a file.Here are some examples:


calculate_md5sum() {
    local file_path="$1"
    md5sum "$file_path"
}
calculate_md5sum "if.sh"


calculate_sha256sum() {
    local file_path="$1"
    sha256sum "$file_path"
}
calculate_sha256sum "if.sh

compare_checksum() {
    local file_path1="$1"
    local file_path2="$2"
    checksum1=$(md5sum "$file_path1" | awk '{print $1}')
    checksum2=$(md5sum "$file_path2" | awk '{print $1}')
    if [[ "$checksum1" == "$checksum2" ]]; then
    echo "The files match.They are identical."
    else 
    echo "The files do not match.They are different."
    fi
    
}
compare_checksum "if.sh" "if.sh"




Bash Battle Arena

Level 1
mkdir Arena
touch warrior.txt mage.txt archer.txt

Level 2
vi level2.sh
#!/bin/bash
count=1
while [ $count -le 10 ];do
        echo "Count: $count"
        ((count++))
done

Level 3
# Since this script was made within Arena the location of hero in terms of directory wasnt needed
vi level3.sh
#!/bin/bash
file_path="$hero.txt"
if [[ -f "$file_path" ]]; then
        echo "Hero found!"
else
        echo "Hero missing!"
fi

Level 4 
# when making the directory the location of the backup directory was needed for some reason "~" wasnt allowed so had to place $HOME there not sure why.?.However the *.txt was already in Arena (so not needed) but where it was moved to needed to have its location.(Basically foreign to the directory your in needs its exact location.

vi level4.sh
#!/bin/bash
mkdir "$HOME/Backup"
mv *.txt ~/Backup/

Level 5

vi level5.sh

#!/bin/bash
mkdir $HOME/Battlefield
touch $HOME/Battlefield/knight.txt $HOME/Battlefield/sorcerer.txt $HOME/Battlefield/rogue.txt
file_path="$HOME/Battlefield/knight.txt"
if [[ -f "$file_path" ]] ;then
        echo "Knight exists"
        mkdir $HOME/Archive
        mv $HOME/Battlefield/knight.txt  $HOME/Archive
        echo "Knight has been moved"
        else
                echo"Huh?"
                fi

echo "Content of Battlefield:"
ls "$HOME/Battlefield"
echo "Contents of Archive:"
ls "$HOME/Archive"

























 






















