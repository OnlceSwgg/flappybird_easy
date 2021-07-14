import pygame
import os #this will help me to find the path of the images of our game
pygame.font.init() # initialize the pygame font library
pygame.mixer.init() # initialize the music pygame library

# first of all you need to make the main surface "the window"


WIDTH, HEIGHT = 900, 500
WIN = pygame.display.set_mode((WIDTH, HEIGHT)) # The window display, the surface display in tuples
pygame.display.set_caption("First Game!") # this is the title of the page


BLACK = (0, 0, 0)
WHITE = (255, 255, 255)
RED = (255, 0, 0)
YELLOW = (255, 255, 0)
# --- our health font
HEALTH_FONT = pygame.font.SysFont('comicsans', 40)
WINNER_FONT = pygame.font.SysFont('comicsans', 100)
# -----
# -------- add a song on our game
BULLET_HIT_SOUND = pygame.mixer.Sound(os.path.join('Assets', 'Grenade+1.mp3'))# the song when a chracter is hit by a bullet
BULLET_FIRE_SOUND = pygame.mixer.Sound(os.path.join('Assets', 'GUN+Silencer.mp3'))# the song when a chracter is hit by a bullet
# ------
FPS = 60 # this will the FPS of our game specifically of our backgournd, so it's constant. and it's on the clock variable
SPACESHIP_WIDTH, SPACESHIP_HEIGHT = 55, 40
VELOCITY = 5
BULLETS_VELOCITY = 7 # the velocity of the bullets
MAX_BULLETS = 3
#----- event to remove the bullet when is collided to the other rentangle repersnti our character
YELLOW_HIT = pygame.USEREVENT + 1  # number of the custom user events
RED_HIT = pygame.USEREVENT + 2  # number of the custom user events
# ------------------ creating a border that divides the 2 characters
BORDER = pygame.Rect(WIDTH//2-5, 0, 10, HEIGHT) # the position and the widht and the height, but the rectangle will not be in th exact middle coz of the width

# --------------------------------let's make two players, so first of all we need to display two players ecc...:
YELLOW_SPACESHIP_IMAGE = pygame.image.load(os.path.join('Assets', 'spaceship_yellow.png')) # importing the image of the yellow spaceschip
YELLOW_SPACESHIP = pygame.transform.rotate(pygame.transform.scale(YELLOW_SPACESHIP_IMAGE, (SPACESHIP_WIDTH, SPACESHIP_HEIGHT)), 90)# resizing and rotate the image of the Yellow spaceship, so it's a little bit smaller and its rotated good
RED_SPACESHIP_IMAGE = pygame.image.load(os.path.join('Assets', 'spaceship_red.png')) # importing the image of the red spaceschip
RED_SPACESHIP = pygame.transform.rotate(pygame.transform.scale(RED_SPACESHIP_IMAGE, (SPACESHIP_WIDTH, SPACESHIP_HEIGHT)), 270)# resizing and rotate the image of the Yellow spaceship, so it's a little bit smaller and its rotated good
#  -------------------------------
# ------------- add an image background
SPACE = pygame.transform.scale(pygame.image.load(os.path.join('Assets', 'space.png')), (WIDTH, HEIGHT))

# -------------------------------- let's make a loop so we have a pop up on the screen

def draw_window(red, yellow, red_bullets, yellow_bullets, red_health, yellow_health): # let's take as an argument whatever i want to draw
    WIN.blit(SPACE, (0, 0))  # blit the screen of a image . on pygame is on RGB color. but will not fill the display YET
    pygame.draw.rect(WIN, BLACK,
                     BORDER)  # making the rectangle/border. WIN (will draw it on the windows), BLACK (the color), BORDER (will print the border variable)
    # displaying the health
    red_health_text = HEALTH_FONT.render("Health: " + str(red_health), 1, WHITE)
    yellow_health_text = HEALTH_FONT.render("Health: " + str(yellow_health), 1, WHITE)
    WIN.blit(red_health_text, (
    WIDTH - red_health_text.get_width() - 10, 10))  # it's on the edge and 10 pixels from x and 10 pixels from y'
    WIN.blit(yellow_health_text, (10, 10))  # it on the start of the window
    # ------------------ continiung to our draw window. the spaceships
    WIN.blit(YELLOW_SPACESHIP, (yellow.x,
                                yellow.y))  # displaying the spaceships on our display in a position where the human change(using blit to draw a surface onto the screen)
    WIN.blit(RED_SPACESHIP, (red.x,
                             red.y))  # displaying the spaceships on our display in a position where the human change(using blit to draw a surface onto the screen)
    # --------------------------- let's draw the bullets so it wil show up
    for bullet in red_bullets:
        pygame.draw.rect(WIN, RED, bullet)
    for bullet in yellow_bullets:
        pygame.draw.rect(WIN, YELLOW, bullet)

    # ------------------
    pygame.display.update()  # this will update the color background. and so it's OKAY

    # -----------
    # ---------------------------------- moving our yellow character when we put the WASD
def yellow_handle_movement(keys_pressed, yellow):
    if keys_pressed[pygame.K_a] and yellow.x - VELOCITY > 0:  # LEFT and check if pressing the key will pass the border
        yellow.x -= VELOCITY
    if keys_pressed[pygame.K_d] and yellow.x + VELOCITY + yellow.width < BORDER.x:  # RIGHT and check if pressing the key will pass the border. adding + yello.width because "il punto di origine" is on the top left corner and the body/width of the spacehsip can be on the border but not the "il punto di origine"
        yellow.x += VELOCITY
    if keys_pressed[pygame.K_w] and yellow.y - VELOCITY > 0:  # UP and check if pressing the key will pass the border.
        yellow.y -= VELOCITY
    if keys_pressed[pygame.K_s] and yellow.y + VELOCITY + yellow.height < HEIGHT - 15:  # DOWN and check if pressing the key will pass the border. adding + yello.height because "il punto di origine" is on the top left corner and the body/height of the spacehsip can be on the border but not the "il punto di origine"
        yellow.y += VELOCITY

    # -----------
    # ---------------------------------- moving our red character when we put the arrows keys
def red_handle_movement(keys_pressed, red):
    if keys_pressed[pygame.K_LEFT] and red.x - VELOCITY > BORDER.x + BORDER.width:  # LEFT and check if pressing the key will pass the border:  # LEFT
        red.x -= VELOCITY
    if keys_pressed[pygame.K_RIGHT] and red.x + VELOCITY + red.width < WIDTH:  # RIGHT and check if pressing the key will pass the border. adding + yello.width because "il punto di origine" is on the top left corner and the body/width of the spacehsip can be on the border but not the "il punto di origine":  # RIGHT
        red.x += VELOCITY
    if keys_pressed[pygame.K_UP] and red.y - VELOCITY > 0:  # UP and check if pressing the key will pass the border.:  # UP
        red.y -= VELOCITY
    if keys_pressed[pygame.K_DOWN] and red.y + VELOCITY + red.height < HEIGHT -15:  # DOWN and check if pressing the key will pass the border. adding + yello.height because "il punto di origine" is on the top left corner and the body/height of the spacehsip can be on the border but not the "il punto di origine":  # DOWN
        red.y += VELOCITY
# -----------------------
# --------------- moving, and handle the collison of the bullets and handle removing bullets when they get off of the screen or collide

def handle_bullets(yellow_bullets, red_bullets, yellow, red):
    for bullet in yellow_bullets:
        bullet.x += BULLETS_VELOCITY # it's moving from the left to the right so use +=
        if red.colliderect(bullet): # the .colliderect will check if the rectangle representing our red character has collided with the rectangle representing our bullet
            pygame.event.post(pygame.event.Event(RED_HIT)) # this will know if the bullet hit the red character
            yellow_bullets.remove(bullet) # this will remove the bullet, but we need to tell to our program that the bulled ha been remove. go find the code on somewhere to the code
        elif bullet.x > WIDTH:
            yellow_bullets.remove(bullet)


    for bullet in red_bullets:
        bullet.x -= BULLETS_VELOCITY # it's moving from the right to the left so use -=
        if yellow.colliderect(bullet): # the .colliderect will check if the rectangle representing our yellow character has collided with the rectangle representing our bullet
            pygame.event.post(pygame.event.Event(YELLOW_HIT)) # this will know if the bullet hit the yellow character
            red_bullets.remove(bullet) # this will remove the bullet, but we need to tell to our program that the bulled ha been remove. go find the code on somewhere to the code, "it's above"
        elif bullet.x < 0:
            red_bullets.remove(bullet)

def draw_winner(text):
    draw_text = WINNER_FONT.render(text, 1, WHITE)
    WIN.blit(draw_text, (WIDTH/2 - draw_text.get_width()/2, HEIGHT/2 - draw_text.get_width()/2))
    pygame.display.update()
    pygame.time.delay(5000) # pause so after the winner text, it will restart the game

def main(): # a function that is called main and handle all the main game loop in pygame (collision, checking the score and stuff like that
    # ------- here we will change the x and y of our players, so the human can change them and control them
    red = pygame.Rect(700, 300, SPACESHIP_WIDTH, SPACESHIP_HEIGHT) # creating a rectange of our character, the beginning
    yellow = pygame.Rect(100, 300, SPACESHIP_WIDTH, SPACESHIP_HEIGHT) # creating a rectange of our character, the beginning

    # -----------
    # ------------------------------------ bullets from player
    red_bullets = [] # list empty of red bullets
    yellow_bullets = [] # list empty of yellow bullets
    # adding the health
    red_health = 10
    yellow_health = 10

    # -----------
    clock = pygame.time.Clock() # this will control the speed of our WHILE LOOP
    run = True # let's make a while loop. this while loop is the main game loop. it will be an infinitive loop
    while run:
        clock.tick(FPS) # this will control the speed of our WHILE LOOP
        for event in pygame.event.get(): # this will get a list of all the different events we're looping through them, and we can check what these events were and based on what they were,we can do something different
            if event.type == pygame.QUIT: # the first event is the user quid window
                run = False # this will end the while loop, with the game
                pygame.quit() # this is for quit the program
        # ------------------------------------ bullets from player
            if event.type == pygame.KEYDOWN: # making a limited number of bullets
                if event.key == pygame.K_LCTRL and len(yellow_bullets) < MAX_BULLETS:
                    bullet = pygame.Rect(yellow.x + yellow.width, yellow.y + yellow.height//2 - 2, 10, 5)
                    yellow_bullets.append(bullet)
                    ### ---- sound when fire the yellow bullet:
                    BULLET_FIRE_SOUND.play()

                if event.key == pygame.K_RCTRL and len(red_bullets) < MAX_BULLETS:
                    bullet = pygame.Rect(red.x, red.y + red.height//2 - 2, 10, 5)
                    red_bullets.append(bullet)
                    ### ---- sound when FIRE the red bullet:
                    BULLET_FIRE_SOUND.play()

            # what happen when a bullet hit. check the events
            if event.type == RED_HIT:
                red_health -= 1
                ### ---- sound when HIT the red bullet:
                BULLET_HIT_SOUND.play()

            if event.type == YELLOW_HIT:
                yellow_health -= 1
                ### ---- sound when HIT the yellow bullet:
                BULLET_HIT_SOUND.play()
        # checkin when a player has 0 health, the other player won
        winner_text = ""
        if red_health <= 0:
            winner_text = "Yellow wins!"
        if yellow_health <= 0:
            winner_text = "Red wins!"

        if winner_text != "":
            draw_winner(winner_text)
            break


        keys_pressed = pygame.key.get_pressed()
        yellow_handle_movement(keys_pressed, yellow)
        red_handle_movement(keys_pressed, red)
# ------------------------------------ moving the bullets and check if they hit any of the character
        handle_bullets(yellow_bullets, red_bullets, yellow, red)



        draw_window(red, yellow, red_bullets, yellow_bullets, red_health, yellow_health)  # let's call the function of the fill screen, so it's more organized

    #pygame.quit() # this will quit the game. # comment otherwise main is not working
    main() # this will recall the function, so will restart the game
if __name__ == '__main__':
    main()
