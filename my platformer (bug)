MAIN CODE:

#rysunek dinozaura:
#arks.itch.io/dino-characters
#twitter tworcy dinozaura: @ScissorMarks

from ogurek.engine import Animation
import pygame
import engine
def drawText(t,x,y):
    text = font.render(t, True, YELLOW, DARK_GREY)
    text_rectangle = text.get_rect()
    text_rectangle.topleft = (x,y)
    screen.blit(text, text_rectangle)
SCREEN_SIZE = (700,500)
DARK_GREY = (50,50,50)
DARK_BLUE = (48, 81, 227)
BLACK = (0,0,0)
YELLOW = (181, 181, 24)
game_state = 'w trakcie'
player_width = 45
player_height = 51
pygame.init()
screen = pygame.display.set_mode(SCREEN_SIZE)
pygame.display.set_caption("Platformówka")
clock = pygame.time.Clock()
font = pygame.font.Font(pygame.font.get_default_font(), 18)
player_image = pygame.image.load("ogurek/player_00.png")
player_x = 300
player_y = 0
player_speed = 0
player_acceleration = 0.2
player_direction = 'prawo'
player_state = 'bezczynny'
player_animations = (
    'bezczynny' : engine.Animation([
        pygame.image.load("ogurek/player_00.png"),
        pygame.image.load("ogurek/player_01.png"),
        pygame.image.load("ogurek/player_02.png"),
        pygame.image.load("ogurek/player_03.png"),
    ]),
    'chodzi' : engine.Animation([
        pygame.image.load("ogurek/player_04.png"),
        pygame.image.load("ogurek/player_05.png"),
        pygame.image.load("ogurek/player_06.png"),
        pygame.image.load("ogurek/player_07.png"),
        pygame.image.load("ogurek/player_08.png"),
        pygame.image.load("ogurek/player_09.png")
    ])
platforms1 = [
pygame.Rect(100,300,400,50),
pygame.Rect(100,250,50,50),
pygame.Rect(450,250,50,50)
]
platforms2 = [
pygame.Rect(100,300,400,48),
pygame.Rect(100,250,50,48),
pygame.Rect(450,250,50,48)
]
coin_image = pygame.image.load("ogurek\coin1.png")
coin_animation = engine.Animation([
pygame.image.load("ogurek\coin1.png"),
pygame.image.load("ogurek\coin2.png"),
pygame.image.load("ogurek\coin3.png"),
pygame.image.load("ogurek\coin4.png"),
pygame.image.load("ogurek\coin5.png"),
pygame.image.load("ogurek\coin6.png"),
pygame.image.load("ogurek\coin7.png"),
pygame.image.load("ogurek\coin8.png")
])
coins = [
    pygame.Rect(100,100,21,21),
    pygame.Rect(200,250,21,21)
]
enemy_image = pygame.image.load("ogurek\enemy.png")
enemies = [
    pygame.Rect(150,250,48,48)
]
lives = 3
heart_image = pygame.image.load("ogurek\heart.png")

score = 0
running = True
while running:
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            running = False
    if game_state == 'w trakcie':
        new_player_x = player_x
        new_player_y = player_y
        keys = pygame.key.get_pressed()
        if keys[pygame.K_a]:
            new_player_x -= 2
            player_direction = 'lewo'
            player_state = 'chodzi'
        if keys[pygame.K_d]:
            new_player_x += 2
            player_direction = 'prawo'
            player_state = 'chodzi'
        if not keys[pygame.K_a] and not keys[pygame.K_d]:
            player_state = 'bezczynny'
        if keys[pygame.K_SPACE] and player_on_ground:
            player_speed = -7
    if game_state == 'w trakcie':
        coin_animation.update()
        player_animations[player_state].update()
        new_player_rect = pygame.Rect(new_player_x,player_y,player_width,player_height)
        x_colission = False
        for p in platforms1 or platforms2:
            if p.colliderect(new_player_rect):
                x_colission = True
                break
        if x_colission == False:
            player_x = new_player_x 
        player_speed += player_acceleration
        new_player_y += player_speed
        new_player_rect = pygame.Rect(player_x, new_player_y,64,64)
        y_colission = False
        player_on_ground = False
        for p in platforms1 or platforms2:
            if p.colliderect(new_player_rect):
                y_colission = True
                player_speed = 0
                if p[1] > new_player_y:
                    player_y = p[1] - 64
                    player_on_ground = True
                break
        if y_colission == False:
            player_y = new_player_y 
        player_rect = pygame.Rect(player_x,player_y,player_width, player_height)
        for e in enemies:
            if e.colliderect(player_rect):
                lives -= 1
                player_x = 300
                player_y = 0
                player_speed = 0
                if lives <= 0:
                    game_state = 'przegrana'
        for c in coins:
            if c.colliderect(player_rect):
                coins.remove(c)
                score += 1
                if score >= 2:
                    game_state = 'wygrana'
    screen.fill(DARK_GREY)
    for p in platforms1: 
        pygame.draw.rect(screen, (DARK_BLUE), p)
    for p in platforms2: 
        pygame.draw.rect(screen, (BLACK), p)
    for c in coins:
        coin_animation.draw(screen, c.x,c.y,False,False)
    for e in enemies:
        screen.blit(enemy_image, (e.x, e.y))
    if player_direction == 'prawo':
        #screen.blit(player_image, (player_x, player_y))
        player_animations[player_state].draw(screen,player_x,player_y,False,False)
    elif player_direction == 'lewo':
        screen.blit(pygame.transform.flip(player_image, True, False),(player_x, player_y))
        player_animations[player_state].draw(screen,player_x,player_y,True,False)
    screen.blit(coin_image, (20,3))
    drawText(': ' + str(score),50,10)
    for l in range(lives):
        screen.blit(heart_image, (550 + (l*50),0))
    if game_state == 'wygrana':
        drawText('Wygrałeś/aś',10,10)
    if game_state == 'przegrana':
        drawText('Przegrałeś/aś',10,10)
    pygame.display.flip()
    clock.tick(60)
pygame.quit()
