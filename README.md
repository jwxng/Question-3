title_list = [ ' 3', ' 4', ' 5', ' 6', ' 7', ' 8', ' 9', '10', '11', '12', '13', '14', '15', '16', '17', '18']
user_list =  [ ' 0', ' 0', ' 0', ' 0', ' 0', ' 0', ' 0', ' 0', ' 0', ' 0', ' 0', ' 0', ' 0', ' 0', ' 0', ' 0']
comp_list =  [" ", " ", " ", " ", " ", " ", " ", "  ", "  ", "  ", "  ", "  ", "   ", "  ", "  ", "  "]
import random 
comp_loop = True
comp_table = []
perm_count = 0


def generate_nums():
    num_1 = random.randint(1, 6)
    num_2 = random.randint(1, 6)
    num_3 = random.randint(1, 6)
    num_4 = random.randint(1, 6)
    num_5 = random.randint(1, 6)
    return num_1, num_2, num_3, num_4, num_5

# only give the user 3 - 4 chances to enter a new number, and tell them
# if it's already there and they have limited chances
def user_turn(num):
    num_1 = num[0]
    num_2 = num[1]
    num_3 = num[2]
    num_4 = num[3]
    num_5 = num[4]

    chosen_dice = []
    variable = []
    turns = 0
    boolean = True
    for x in range (0, 3):
        while True:
            for y in range (3, 0, -1):
                while turns < 3:
                    print("This is turn number", turns, "(you get 3 turns in total)")
                    print("You have", y, "chance(s)left.")
                    choice = input("Enter which dice you want to use (enter  3 numbers \n\
        between 1 and 5")
                    try:
                        choice = int(choice)
                        if choice > 0 and choice < 6:
                           
                            if choice == 1 and 1 not in variable:
                                chosen_dice.append(num_1)
                                variable.append(1)
                                break
                           
                            elif choice == 2 and 2 not in variable:
                                chosen_dice.append(num_2)
                                variable.append(2)
                                break
                               
                            elif choice == 3 and 3 not in variable:
                                chosen_dice.append(num_3)
                                variable.append(3)
                                break

                            elif choice == 4 and 4 not in variable:
                                chosen_dice.append(num_4)
                                variable.append(4)
                                break

                            elif choice == 5 and 5 not in variable:
                                chosen_dice.append(num_5)
                                variable.append(5)
                                break
                            print(chosen_dice)
                               
                        else:
                            print("Enter a positive integer below 6!")
                    except:
                        print("Enter a number!")
           
            while turns < 3:
                print("enter while block", turns, chosen_dice)
                total = sum(chosen_dice)
                print("total is", total)
                pos = (total - 3)
                # boolean flag no
                no = False
                if ' X' == user_list [pos]:
                    # print the total and the value coming out of the user list position
                    print("total and position value", total, user_list [pos])
                    while True:
                        ans = input("That number has already been crossed out! \n\
    would you like to try again? (Yes or No):")
                        if ans == 'Yes':
                            chosen_dice = []
                            variable = []
                            turns += 1
                            if turns < 3:
                                break
                            else:
                                print("You have had 3 turns already!")
                                Boolean = False
                                no = True
                                break
                       
                        elif ans == 'No':
                            no = True
                            break
                        else:
                            print("Invalid answer! Please try again!")

                else:
                    return total, pos
               

                if no == True:
                    break
                elif no == False:
                    break

            if no == True:
                break
        if no == True:
            break


# Computer Turn Functions        
def computer_num():
    n1, n2, n3, n4, n5 = generate_nums()
    n_list = [n1, n2, n3, n4, n5]

    return n_list


def computer_rand(l):
    loop2 = True
    loop3 = True
    
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
    c = c1+c2+c3
    
    print(c1, "+", c2, "+", c3, "=", c)
    return c


def computer_tracker(n, table, count):
    if n not in table:
        table.append(n)
        in_comp = False
        count = 0
    else:
        in_comp = True
        count += 1

    table.sort()

    if count > 100:
        in_comp = True
        print("No permutation found.")
        count = 0

    return table, in_comp, count


#Main Program
#Player Turn
while True:
    num = generate_nums()
    print(num)
    # returning the final value of each cycle to the main program
    final_value = user_turn(num)
    # checks if the final_value is not none
   
    if final_value != None:
        pos_value = final_value[1]
        print("at end of pgm", final_value[0])
        # storing the final value of each cycle in the list
        del(user_list[pos_value])
        user_list.insert(pos_value, ' X')
        print(title_list)
        print(user_list, " user_list at end")
       
        if ' 0' not in user_list:
            print("You Win!")        
            break

#Computer Turn
comp_list = computer_num()
print("Computer's numbers:", comp_list)

while comp_loop:
    c = computer_rand(comp_list)
    comp_table, comp_loop, perm_count = \
    computer_tracker(c, comp_table, perm_count)

print("Current computer standings:", comp_table)

