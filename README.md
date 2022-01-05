"""before executing make a txt a file in same folder of name "raj" and write 30 or whatever value you want to initialize as high score"""
#by pygame
import pygame
import random
pygame.init()
# Colors
white = (255, 255, 255)
red = (255, 0, 0)
black = (0, 0, 0)
r=(255,235,205)
aqua=(0,255,255)

# Creating window
screen_width = 900
screen_height = 600
gameWindow = pygame.display.set_mode((screen_width, screen_height))

pygame.display.set_caption("My First Game")
pygame.display.update()

#variables


clock = pygame.time.Clock()
font = pygame.font.SysFont(None, 55)

def text(text, color, x, y):
    screen_text = font.render(text, True, color)
    gameWindow.blit(screen_text, [x,y])
def plot_snake(gameWindow, color, snk_list, snake_size):
    for x,y in snk_list:
        pygame.draw.rect(gameWindow, color, [x, y, snake_size, snake_size])
 
def welcome():
    exit_game = False
    while not exit_game:
        gameWindow.fill((255,182,193))
        text("Welcome to Snakes", black, 260, 250)
        text("Press Space Bar To Play", black, 232, 290)
        for event in pygame.event.get():
            if event.type == pygame.QUIT:
                exit_game = True
            if event.type == pygame.KEYDOWN:
                if event.key == pygame.K_SPACE:
                    gameloop()

        pygame.display.update()
        clock.tick(60) 

# Game Loop
def gameloop():
    exit_game = False
    game_over = False
    snake_x = 45
    snake_y = 55
    vx = 0
    vy = 0
    score=0
    with open("raj.txt","r") as f:
        raj=f.read()
    foodx = random.randint(20, screen_width/2)
    foody = random.randint(20, screen_height/2)
    v=5
    size = 20
    fps = 60
    list1 = []
    length = 1  

    while not exit_game:
        if game_over:
            with open("raj.txt","w") as f:
                f.write(str(raj))
            
            gameWindow.fill(white)
            text("Game Over! Press Enter To Continue", red, 100, 250)

            for event in pygame.event.get():
                if event.type == pygame.QUIT:
                    exit_game = True

                if event.type == pygame.KEYDOWN:
                    if event.key == pygame.K_RETURN:
                        gameloop()
        else:
            for event in pygame.event.get():
                if event.type == pygame.QUIT:
                    exit_game = True
                if event.type == pygame.KEYDOWN:
                    if event.key == pygame.K_RIGHT:
                        vx = v
                        vy = 0
                    if event.key == pygame.K_LEFT:
                        vx= - v
                        vy = 0
                    if event.key == pygame.K_UP:
                        vy = - v
                        vx = 0
                    if event.key == pygame.K_DOWN:
                        vy = v
                        vx = 0
                    if event.key == pygame.K_z :
                        score+=10
                    
            snake_x = snake_x + vx
            snake_y = snake_y + vy
            if abs(snake_x-foodx)<10 and abs(snake_y - foody)<10:
                score+=10
                
                
                foodx = random.randint(20, screen_width/2)
                foody = random.randint(20, screen_height/2)
                length +=5
                if score>int(raj):
                    raj=score

            gameWindow.fill(aqua)
            text("Score: " + str(score)+" highscore:"+str(raj), r,4, 4)
            pygame.draw.rect(gameWindow, red, [foodx, foody, size, size])
            #pygame.draw.rect(gameWindow, black, [snake_x, snake_y, size, size])
            head = []
            head.append(snake_x)
            head.append(snake_y)
            list1.append(head)

            if len(list1)>length:
                del list1[0]
            if head in list1[:-1]:
                game_over = True
            if snake_x<0 or snake_x>screen_width or snake_y<0 or snake_y>screen_height:
                game_over = True

           
            plot_snake(gameWindow, black, list1, size)
        pygame.display.update()
        clock.tick(fps)

    pygame.quit()
    quit()
welcome()
#to win press z😂


