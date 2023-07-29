#!/bin/bash

echo -e "Enter the name of the file : \c"
read file_name

if [ -d $file_name ]
then
  echo "$file_name found"

else
  echo "$file_name not found"
fi


#file_name will be any file name you put.
#-e means it leaves curser at the end of the sentence,


echo -e "Enter the name of the file : \c"
read file_name

if [ -d $file_name ]
then
  echo "$file_name found"
else
  echo "$file_name not found"
fi

#-------------------------
#count=10

#if [ $count -ne "9" ]
#then
  #echo "condition is true"
  #echo "You are very smart"

#else
 # echo "condition is false"
  #echo "You are still very smart"
#fi

#-------------------------
#name=$1
#compliment=$2

#user=$(whoami)
#date=$(date)
#whereami=$(pwd)


#echo "Good morning!"
#sleep 1
#echo "Your awesome!"
#sleep 1
#echo "You have the best $compliment I've ever seen $name!!"
#sleep 2

#echo "You are currently logged in as the $user and your current directory is $whereami on this $date"


#user_var means user variable. It allows you to use any username.
#you can type any username and will print out that username after entering.
#pass_var means password variable. It allows you to use any password.

#read -p 'username : ' user_var
#read -sp 'password : ' pass_var
#echo
#sleep 2
#echo "Welcome to the linux world $user_var"

#Example scripts:

#----------------------------

#echo "Enter names : "
#read name1 name2 name3

#echo "Welcome to the matrix $name1 , $name2 , $name3"

#----------------------------
