# Question 3
# Sum it Up

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
 
def computer():
 loop2 = True
 loop3 = True

 n1, n2, n3, n4, n5 = random()
 l = [n1, n2, n3, n4, n5]
    
 r1 = random.randint(0, 4)
  while loop2:
   r2 = random.randint(0, 4)
    if r2 != r1:
     loop2 = False
  while loop3:
   r3 = random.randint(0, 4)
    if r3 != r2 and r3 != r1:
     loop3 = False

  c1 = l[r1]
  c2 = l[r2]
  c3 = l[r3]
    
  return c1, c2, c3

c1, c2, c3 = computer()
