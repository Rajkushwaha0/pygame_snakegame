# pygame_snakegame
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
exit_game = False
game_over = False
snake_x = 45
snake_y = 55
vx = 0
vy = 0
score=0
foodx = random.randint(20, screen_width/2)
foody = random.randint(20, screen_height/2)
v=5
size = 20
fps = 60

clock = pygame.time.Clock()
font = pygame.font.SysFont(None, 55)

def text(text, color, x, y):
    screen_text = font.render(text, True, color)
    gameWindow.blit(screen_text, [x,y])
    

# Game Loop
while not exit_game:
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
    snake_x = snake_x + vx
    snake_y = snake_y + vy
    if abs(snake_x-foodx)<9 and abs(snake_y - foody)<9:
        score+=1
        print("Score:",score*10)
        
        foodx = random.randint(20, screen_width/2)
        foody = random.randint(20, screen_height/2)

    gameWindow.fill(aqua)
    text("Score: " + str(score * 10), r,4, 4)
    pygame.draw.rect(gameWindow, red, [foodx, foody, size, size])
    pygame.draw.rect(gameWindow, black, [snake_x, snake_y, size, size])
    pygame.display.update()
    clock.tick(fps)

pygame.quit()
quit()
