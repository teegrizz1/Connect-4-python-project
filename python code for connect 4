import random
import statistics
import termcolor as t
import time
mode1 = ("red")
mode2 = ("blue")
blueWins = 0
redWins = 0

# Initialize variables for the coordinate with the maximum count
coordinateCount=[]
from firebase import firebase

"""myDBConn = firebase.FirebaseApplication(
    "https://magic-7f4e2-default-rtdb.firebaseio.com/", None)

myGetResults = myDBConn.get('/gameStats',None)

for keyID in myGetResults:
    print(myGetResults)
    blueWinsActual = myGetResults['blueWins']
    redWinsActual = myGetResults['redWins']
blueWins = blueWinsActual
redWins = redWinsActual
print("#",blueWinsActual)
print("#",redWinsActual)
print(blueWins)
print(redWins)"""

#t.c, this allows me to add colors to certains parts of my code.
t.cprint("Welcome to Connect Four", 'blue')
t.cprint("-----------------------", 'red')

#Gameboard
def printGameBoard():
    t.cprint("\n     A    B    C    D    E    F    G  ", 'blue', end="")
    for x in range(rows):
        print("\n   +----+----+----+----+----+----+----+")
        print(x, " | ", end="")
        for y in range(cols):
            if (gameBoard[x][y] == "⚪"):
                print("", end="")
                t.cprint(gameBoard[x][y], 'red', end=" | ")
            elif (gameBoard[x][y] == "⚫"):
                print("", end="")
                t.cprint(gameBoard[x][y], 'blue', end=" | ")
            else:
                print("", gameBoard[x][y], end="  | ")
    print("\n   +----+----+----+----+----+----+----+")


def modifyArray(spacePicked, turn):
    gameBoard[spacePicked[0]][spacePicked[1]] = turn


def checkForWinner(chip):
    global blueWins
    global redWins
    ### Check horizontal spaces
    for y in range(rows):
        for x in range(cols - 4):
            if (gameBoard[x][y] == chip and gameBoard[x + 1][y] == chip
                    and gameBoard[x + 2][y] and gameBoard[x + 3][y]) == chip:

                return True

def checkForWinner(chip):
    global blueWins
    global redWins
    for y in range(rows):
        for x in range(cols - 4):
            if (gameBoard[x][y] == chip and gameBoard[x + 1][y] == chip
                    and gameBoard[x + 2][y] == chip and gameBoard[x + 3][y] == chip):
                return True

    for x in range(rows):
        for y in range(cols - 3):
            if (gameBoard[x][y] == chip and gameBoard[x][y + 1] == chip
                    and gameBoard[x][y + 2] == chip and gameBoard[x][y + 3] == chip):
                return True

    for x in range(rows - 3):
        for y in range(3, cols):
            if (gameBoard[x][y] == chip and gameBoard[x + 1][y - 1] == chip
                    and gameBoard[x + 2][y - 2] == chip and gameBoard[x + 3][y - 3] == chip):
                return True

    for x in range(rows - 3):
        for y in range(cols - 3):
            if (gameBoard[x][y] == chip and gameBoard[x + 1][y + 1] == chip
                    and gameBoard[x + 2][y + 2] == chip and gameBoard[x + 3][y + 3] == chip):
                return True

    return False



#Coordinate code
def coordinateParser(inputString):
    coordinate = [None] * 2
    if (inputString[0] == "A".upper()):
        coordinate[1] = 0
    elif (inputString[0] == "B"):
        coordinate[1] = 1
    elif (inputString[0] == "C"):
        coordinate[1] = 2
    elif (inputString[0] == "D"):
        coordinate[1] = 3
    elif (inputString[0] == "E"):
        coordinate[1] = 4
    elif (inputString[0] == "F"):
        coordinate[1] = 5
    elif (inputString[0] == "G"):
        coordinate[1] = 6
    else:
        print("Invalid try again")
    coordinate[0] = int(inputString[1])
    return coordinate


def isSpaceAvailable(intendedCoordinate):
    if (gameBoard[intendedCoordinate[0]][intendedCoordinate[1]] == "⚫"):
        return False
    elif (gameBoard[intendedCoordinate[0]][intendedCoordinate[1]] == "⚪"):
        return False
    else:
        return True


#Gravity checker
def gravityChecker(intendedCoordinate):
    ### Calculate space below
    spaceBelow = [None] * 2
    spaceBelow[0] = intendedCoordinate[0] + 1
    spaceBelow[1] = intendedCoordinate[1]
    ### Is the coordinate at ground level
    if (spaceBelow[0] == 6):
        return True
### Check if there's a token below
    if (isSpaceAvailable(spaceBelow) == False):
        return True
    return False


#Gameboard
possibleLetters = [
    "A",
    "B",
    "C",
    "D",
    "E",
    "F",
    "G",
]
gameBoard = [["", "", "", "", "", "", ""], ["", "", "", "", "", "", ""],
             ["", "", "", "", "", "", ""], ["", "", "", "", "", "", ""],
             ["", "", "", "", "", "", ""], ["", "", "", "", "", "", ""]]

rows = 6
cols = 7
#Game mode menu selection
t.cprint("1. Single Player", 'blue')
t.cprint("2. Multi Player", 'red')
t.cprint("3. simulation", 'green')
t.cprint("4. mystery mode", 'blue')
mode = int(input("Please select a mode"))

while mode >= 5:
    print("Error, please select valid input")
    print("1. Single Player")
    print("2. Multi Player")
    print("3. simulation")
    print("4.Mystery Mode")
    mode = int(input("please select a mode"))
t.cprint("Next Step", 'blue')
#Code for single player
if mode == 1:
    turnCounter = 0
    while True:
        valid = False
        printGameBoard()
        if turnCounter % 2 ==0:
            #players turn
            chip = "⚪"
            while valid == False:
                spacePicked = (input("\nChoose a space: ")).upper()
                print(spacePicked)
                coordinate = coordinateParser(spacePicked)
                if (isSpaceAvailable(coordinate) and gravityChecker(coordinate)):
                    modifyArray(coordinate, "⚪")
                    valid = True
                else:
                    print("Player Not a valid coordinate")


            turnCounter += 1
            winner = checkForWinner("⚪")
            if winner == True:
                print("*"*50,winner)
                print("\nGame over", chip, "wins! Thank you for playing :)")
                print("#", chip, "#")
                print("Red WON")
                redWins += 1
                printGameBoard()
                break
### It's the computers turn
        else:
            valid2 = False
            chip = "⚫"
            while valid2 == False:
                cpuChoice = [random.choice(possibleLetters),random.randint(0, 5)]
                print(cpuChoice)
                cpuCoordinate = coordinateParser(cpuChoice)
                if (isSpaceAvailable(cpuCoordinate) and gravityChecker(cpuCoordinate)):
                    modifyArray(cpuCoordinate, "⚫")
                    valid2 = True
                else:
                    print("Player Not a valid coordinate")
            turnCounter +=1
            winner = checkForWinner("⚫")
            if winner == True:
                print("*"*50,winner)
                print("\nGame over", chip, "wins! Thank you for playing :)")
                print("#", chip, "#")
                print("Blue WON")
                blueWins += 1
                printGameBoard()
                break
           
#Code for multiplayer
elif mode == 2:
    turnCounter = 0
    while True:
        valid = False
        printGameBoard()
        if turnCounter % 2 ==0:
            #players turn
            chip = "⚪"
            while valid == False:
                spacePicked = (input("\nChoose a space: ")).upper()
                print(spacePicked)
                coordinate = coordinateParser(spacePicked)
                if (isSpaceAvailable(coordinate) and gravityChecker(coordinate)):
                    modifyArray(coordinate, "⚪")
                    valid = True
                else:
                    print("Player Not a valid coordinate")


            turnCounter += 1
            winner = checkForWinner("⚪")
            if winner == True:
                print("*"*50,winner)
                print("\nGame over", chip, "wins! Thank you for playing :)")
                print("#", chip, "#")
                print("Red WON")
                redWins += 1
                printGameBoard()
                break
### It's the computers turn
        else:
            chip = "⚫"
            while valid == False:
                spacePicked = (input("\nChoose a space: ")).upper()
                print(spacePicked)
                coordinate = coordinateParser(spacePicked)
                if (isSpaceAvailable(coordinate) and gravityChecker(coordinate)):
                    modifyArray(coordinate, "⚫")
                    valid = True
                else:
                    print("Player Not a valid coordinate")


            turnCounter += 1
            winner = checkForWinner("⚫")
            if winner == True:
                print("*"*50,winner)
                print("\nGame over", chip, "wins! Thank you for playing :)")
                print("#", chip, "#")
                print("Blue WON")
                blueWins += 1
                printGameBoard()
                break

#code for simulation
elif mode == 3:
    #code for simulation

   #code for simulation

    redWins = 0
    blueWins = 0
    draws = 0

for i in range(10):
    turnCounter = 0
    draw = False
    while True:
        valid = False
        printGameBoard()
        if turnCounter % 2 ==0:
            valid = False
            chip = "⚪"
            while valid == False:
                cpuChoice = (random.choice(possibleLetters),random.randint(0, 5))
                coordinateCount.append(cpuChoice)
                #print(cpuChoice)
                cpuCoordinate = coordinateParser(cpuChoice)
                if (isSpaceAvailable(cpuCoordinate) and gravityChecker(cpuCoordinate)):
                    modifyArray(cpuCoordinate, "⚪")
                    valid = True
                #else:
                    #print("Player Not a valid coordinate")
            turnCounter +=1
            winner = checkForWinner("⚪")
            if winner == True:
                print("*"*50,winner)
                print("\nGame over", chip, "wins! Thank you for playing :)")
                print("#", chip, "#")
                print("Blue WON")
                blueWins += 1
                printGameBoard()
                break
        ### It's the computers turn
        else:
            valid2 = False
            chip = "⚫"
            while valid2 == False:
                cpuChoice = [random.choice(possibleLetters),random.randint(0, 5)]
                #print(cpuChoice)
                cpuCoordinate = coordinateParser(cpuChoice)
                if (isSpaceAvailable(cpuCoordinate) and gravityChecker(cpuCoordinate)):
                    modifyArray(cpuCoordinate, "⚫")
                    valid2 = True
                #else:
                    #print("Player Not a valid coordinate")
            turnCounter +=1
            winner = checkForWinner("⚫")
            if winner == True:
                print("*"*50,winner)
                print("\nGame over", chip, "wins! Thank you for playing :)")
                print("#", chip, "#")
                print("Red WON")
                redWins += 1
                printGameBoard()
                break
        if turnCounter == 42: # all spaces have been filled and nobody has won
            print("*"*50)
            print("\nGame over! It's a DRAW! Thank you for playing :)")
            draws += 1
            printGameBoard()
            draw = True
            break

    if draw == False and redWins >= blueWins:
        print("Simulation ", i+1, ": Red is the winner")
    elif draw == False and redWins < blueWins:
        print("Simulation ", i+1, ": Blue is the winner")
    else:
        print("Simulation ", i+1, ": It's a draw")


if redWins >= blueWins and redWins >= draws:
    print ("modal winner :", mode1)
elif blueWins >= redWins and blueWins >= draws:
    print ("modal winner :", mode2)
else:
    print ("modal winner : Draw")  
#print(coordinateCount)
print(coordinateCount)
modalCoordinate = statistics.mode(coordinateCount)
 
# Iterate through the dictionary and find the coordinate with the maximum count

# Print the coordinate with the maximum count
print("Coordinate picked the most:",modalCoordinate)

  

#Hypothesis what if there was a bigger game board would that change the modal winner
#Gameboard
  
if mode == 4:
  
    
  

  def printGameboard():
    t.cprint("\n     A    B    C    D    E    F    G    H    I  ", 'blue', end="")
    for x in range(rows):
        print("\n   +----+----+----+----+----+----+----+----+----+")
        print(x, " | ", end="")
        for y in range(cols):
            if (gameboard[x][y] == "⚪"):
                print("", end="")
                t.cprint(gameboard[x][y], 'red', end=" | ")
            elif (gameBoard[x][y] == "⚫"):
                print("", end="")
                t.cprint(gameboard[x][y], 'blue', end=" | ")
            else:
                print("", gameboard[x][y], end="  | ")
    print("\n   +----+----+----+----+----+----+----+----+----+")

  rows = 8
  cols = 9

  turnCounter = 0
  while True:
    
    valid = False
    printGameboard()
    if turnCounter % 2 ==0:
      valid = False
      chip = "⚪"
      while valid == False:
        cpuChoice = [random.choice(possibleLetters),random.randint(0, 5)]
        #print(cpuChoice)
        cpuCoordinate = coordinateParser(cpuChoice)
      if (isSpaceAvailable(cpuCoordinate) and gravityChecker(cpuCoordinate)):
            modifyArray(cpuCoordinate, "⚪")
            valid = True
        #else:
            #print("Player Not a valid coordinate")
            turnCounter +=1
            winner = checkForWinner("⚪")
            if winner == True:
              print("*"*50,winner)
              print("\nGame over", chip, "wins! Thank you for playing :)")
              print("#", chip, "#")
              print("Red WON")
              blueWins += 1
              printGameboard()
              break
### It's the computers turn
            else:
              valid2 = False
              chip = "⚫"
              while valid2 == False:
                  cpuChoice = [random.choice(possibleLetters),random.randint(0, 5)]
                #print(cpuChoice)
                  cpuCoordinate = coordinateParser(cpuChoice)
                  if (isSpaceAvailable(cpuCoordinate) and gravityChecker(cpuCoordinate)):
                    modifyArray(cpuCoordinate, "⚫")
                    valid2 = True
                #else:
                    #print("Player Not a valid coordinate")
            turnCounter +=1
            winner = checkForWinner("⚫")
            if winner == True:
                print("*"*50,winner)
                print("\nGame over", chip, "wins! Thank you for playing :)")
                print("#", chip, "#")
                print("Blue WON")
                redWins += 1
                printGameboard()
                break




data = {"redWins": redWins, "blueWins": blueWins}
print(data)
myDBConn.put("/", "gameStats", data)
print("All Done")
print(winner)

import matplotlib.pyplot as plt
winStats = [redWins, blueWins]
names = ["Red", "blue"]
plt.bar(names, winStats)
plt.title("winners statistics")
plt.xlabel("Color")
plt.ylabel("amount of wins")
plt.show
