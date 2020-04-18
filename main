import pygame, random
from itertools import count
import matplotlib.pyplot as plt
from matplotlib.animation import FuncAnimation
# Define some colors
BLACK = (0, 0, 0)
WHITE = (255, 255, 255)
GREEN = (0, 128, 0)
RED = (255, 0, 0)
VIOLET = (143, 0, 255)
#for matplotlib graph
iterazione = 0
x_vals = [0]
y_vals = [0]
plt.style.use('fivethirtyeight')
start = 0
# This sets the WIDTH and HEIGHT of each grid location
WIDTH = 8
HEIGHT = 8
gridSize = 100
# This sets the margin between each cell
MARGIN = 2
screenL = 1000
# Create a 2 dimensional array. A two dimensional
# array is simply a list of lists.
grid = []
deaths = 0
for row in range(gridSize):
    grid.append([])
    for column in range(gridSize):
        grid[row].append(0)  # Append a cell


def thereisinfectnear(row, column):
    global grid
    numClose = 0
    if row -1>0:
        if grid[row-1][column] == 2:
            numClose += 1
    if row + 1 < gridSize:
        if grid[row + 1][column] == 2:
            numClose += 1
    if row - 1 > 0 and column - 1 > 0:
        if grid[row - 1][column-1] == 2:
            numClose += 1
    if row + 1 < gridSize and column - 1 > 0:
        if grid[row + 1][column-1] == 2:
            numClose += 1
    if column - 1 > 0:
        if grid[row][column-1] == 2:
            numClose += 1
    if column + 1 < gridSize:
        if grid[row][column + 1] == 2:
            numClose += 1
    if row - 1 > 0 and column + 1 < gridSize:
        if grid[row - 1][column + 1] == 2:
            numClose += 1
    if row + 1 < gridSize and column + 1 < gridSize:
        if grid[row + 1][column + 1] == 2:
            numClose += 1
    return numClose

def thereisInfectedSick(row, column):
    global grid
    numClose = 0
    if row -1>0:
        if grid[row-1][column] == 4:
            numClose += 1
    if row + 1 < gridSize:
        if grid[row + 1][column] == 4:
            numClose += 1
    if row - 1 > 0 and column - 1 > 0:
        if grid[row - 1][column-1] == 4:
            numClose += 1
    if row + 1 < gridSize and column - 1 > 0:
        if grid[row + 1][column-1] == 4:
            numClose += 1
    if column - 1 > 0:
        if grid[row][column-1] == 4:
            numClose += 1
    if column + 1 < gridSize:
        if grid[row][column + 1] == 4:
            numClose += 1
    if row - 1 > 0 and column + 1 < gridSize:
        if grid[row - 1][column + 1] == 4:
            numClose += 1
    if row + 1 < gridSize and column + 1 < gridSize:
        if grid[row + 1][column + 1] == 4:
            numClose += 1
    return numClose
# Initialize pygame
pygame.init()

# Set the HEIGHT and WIDTH of the screen
WINDOW_SIZE = [screenL, screenL]
screen = pygame.display.set_mode(WINDOW_SIZE)

# Set title of screen
pygame.display.set_caption("COVID-19 KINDA SIMULATOR")

def animate(iterazione, totali_contagiati):
    x_vals.append(iterazione)
    y_vals.append(rapporto_sani_contagiati)

# Loop until the user clicks the close button.
done = False

# -------- Main Program Loop -----------
while not done:
    #clock.tick(60)
    #--------USER INPUT----------
    pressed = False
    for event in pygame.event.get():  # User did something
        if event.type == pygame.QUIT:  # If user clicked close
            done = True  # Flag that we are done so we exit this loop
            print(f"Celle Totali = {quanteCelle}")
        elif pygame.mouse.get_pressed()[0]: #SPAWN NOT INFFECT
            # User clicks the mouse. Get the position
            pos = pygame.mouse.get_pos()
            # Change the x/y screen coordinates to grid coordinates
            column = pos[0] // (WIDTH + MARGIN)
            row = pos[1] // (HEIGHT + MARGIN)
            # Set that location to one
            grid[row][column] = 1
        elif pygame.mouse.get_pressed()[1]: #SPAWN WALL
            # User clicks the mouse. Get the position
            pos = pygame.mouse.get_pos()
            # Change the x/y screen coordinates to grid coordinates
            column = pos[0] // (WIDTH + MARGIN)
            row = pos[1] // (HEIGHT + MARGIN)
            # Set that location to one
            grid[row][column] = 3
        if event.type == pygame.MOUSEBUTTONDOWN:
            if event.button == 2:
                if grid[row][column] == 3:
                    grid[row][column] = 0
        elif pygame.mouse.get_pressed()[2]: #SPAWN INFECT
            # User clicks the mouse. Get the position
            pos = pygame.mouse.get_pos()
            # Change the x/y screen coordinates to grid coordinates
            column = pos[0] // (WIDTH + MARGIN)
            row = pos[1] // (HEIGHT + MARGIN)
            # Set that location to one
            grid[row][column] = 2
        #GET PLOT FROM NOW
        if event.type == pygame.KEYUP:
            start += 1


    # Set the screen background
    screen.fill(BLACK)
    color = WHITE
    bin = [-1, 1] #choose between these for random direction
    numAttorno = 0

    #----------------CHECK NEW STATE----------------
    for row in range(gridSize):
        for column in range(gridSize):
            alfa = 6
            infAttorno = thereisinfectnear(row, column)
            sickattorno = thereisInfectedSick(row, column)
            guarisci_o_peggiori = 0
            if grid[row][column] == 2:#IF INFECTED YOU COULD GET SICK OR HEALTHY
                guarisci_o_peggiori = random.randint(1,1000)
                if guarisci_o_peggiori < 900:#YOU STAY INFECTED
                    grid[row][column] = 2
                elif 900<=guarisci_o_peggiori<=990: #guarisci_o_peggiori == range(80,90):#YOU MAY STAY INFECTED
                    grid[row][column] = 4
                elif 990<guarisci_o_peggiori<=1000:
                    grid[row][column] = 1

            elif grid[row][column] == 4:#IF SICK SEE IF YOU GET BETTER OR NOT
                guarisci_o_peggiori = random.randint(1, 1000)
                if guarisci_o_peggiori < 900:
                    grid[row][column] = 4
                elif 900<=guarisci_o_peggiori<=920:
                    deaths += 1
                    grid[row][column] = 0
                else:
                    grid[row][column] = 1

            elif grid[row][column] == 1 and infAttorno >= 1: #IF HEALTHY BUT INFECTED AROUND GET INFECTED
                grid[row][column] = 2
            elif grid[row][column] == 1 and sickattorno >= 1: #IF HEALTHY BUT SICK AROUND GET INFECTED
                grid[row][column] = 2

            if grid[row][column] == 1:#MOVEMENT FOR HEALTHY
                tentativo = 0
                y = 0
                x = 0
                posY = 0
                posX = 0
                while alfa != 0 and tentativo < 10:
                    while posX <= 0 or posX >= gridSize or posY <= 0 or posY >= gridSize:
                        y = random.choice(bin)
                        x = random.choice(bin)
                        posY = row + y
                        posX = column + x
                    alfa = grid[posY][posX]
                    tentativo += 1
                if tentativo >= 10:
                    grid[row][column] = 1
                else:
                    grid[row][column] = 0
                    grid[posY][posX] = 1

            elif grid[row][column] == 2:#MOVEMENT FOR INFECTED
                tentativo = 0
                y = 0
                x = 0
                posY = 0
                posX = 0
                while alfa != 0 and tentativo < 10:
                    while posX <= 0 or posX >= gridSize or posY <= 0 or posY >= gridSize: #Check its not going out of grid
                        y = random.choice(bin)
                        x = random.choice(bin)
                        posY = row + y
                        posX = column + x
                    alfa = grid[posY][posX]
                    tentativo += 1
                if tentativo >= 10:
                    grid[row][column] = 2
                else:
                    grid[row][column] = 0
                    grid[posY][posX] = 2

            elif grid[row][column] == 4:#MOVEMENT FOR SICK
                tentativo = 0
                y = 0
                x = 0
                posY = 0
                posX = 0
                while alfa != 0 and tentativo < 10:
                    while posX <= 0 or posX >= gridSize or posY <= 0 or posY >= gridSize:
                        y = random.choice(bin)
                        x = random.choice(bin)
                        posY = row + y
                        posX = column + x
                    alfa = grid[posY][posX]
                    tentativo += 1
                if tentativo >= 10:
                    grid[row][column] = 4
                else:
                    grid[row][column] = 0
                    grid[posY][posX] = 4

    quanteCelle = 0
    verdiCelle = 0
    rosseCelle = 0
    violaCelle = 0
    nereCelle = 0
    #------------------SCREEN UPDATE------------------
    for row in range(gridSize):
        for column in range(gridSize):
            if grid[row][column] != 0:
                quanteCelle += 1
            if grid[row][column] == 1:
                color = GREEN
                verdiCelle += 1
            elif grid[row][column] == 2:
                color = RED
                rosseCelle += 1
            elif grid[row][column] == 3:
                color = BLACK
                nereCelle += 1
            elif grid[row][column] == 4:
                color = VIOLET
                violaCelle += 1
            else:
                color = WHITE
            pygame.draw.rect(screen, color, [(MARGIN + WIDTH) * column + MARGIN, (MARGIN + HEIGHT) * row + MARGIN, WIDTH, HEIGHT])

    #print(f"Celle Totali = {quanteCelle}")
    #print(f"Verdi = {verdiCelle}")
    #print(f"Verdi = {rosseCelle}")

    rapporto_sani_contagiati = 0
    totali_contagiati = rosseCelle + violaCelle
    personeTotali = quanteCelle - nereCelle
    try:
        rapporto_sani_contagiati = totali_contagiati / personeTotali
    except:
        pass
    if start > 0:
        iterazione += 1
        animate(iterazione, totali_contagiati)
    pygame.display.update()
print(f"Deaths = {deaths}")
#This is done to draw plot
plt.plot(x_vals, y_vals)
plt.tight_layout()
plt.show()
pygame.quit()
