# Question 3

# This is a test

import random

def dice_num():
 while True:
  num = input("Enter a number between 6 and 10:")
  try:
   num = int(num)
   if num > 5 and num < 11:
    break
            
   else:
    print("Enter an integer between 6 and 10!")
  except:
   print("Enter a number!")

 
