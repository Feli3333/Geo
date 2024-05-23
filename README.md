# Geo
Geo
import pygame
import random

# Initialisierung von Pygame
pygame.init()

# Bildschirmgröße
WIDTH, HEIGHT = 800, 600
screen = pygame.display.set_mode((WIDTH, HEIGHT))
pygame.display.set_caption("Geometrisches Spiel")

# Farben
WHITE = (255, 255, 255)
BLACK = (0, 0, 0)

# Spieler
player_size = 50
player_x = WIDTH // 2 - player_size // 2
player_y = HEIGHT - player_size
player_speed = 5

# Gegner
enemy_size = 50
enemy_x = random.randint(0, WIDTH - enemy_size)
enemy_y = -enemy_size
enemy_speed = 3

# Schleife für das Spiel
clock = pygame.time.Clock()
running = True

while running:
    # Ereignisse überprüfen
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            running = False

    # Spielerbewegung
    keys = pygame.key.get_pressed()
    if keys[pygame.K_LEFT] and player_x > 0:
        player_x -= player_speed
    if keys[pygame.K_RIGHT] and player_x < WIDTH - player_size:
        player_x += player_speed

    # Bewegung des Gegners
    enemy_y += enemy_speed
    if enemy_y > HEIGHT:
        enemy_x = random.randint(0, WIDTH - enemy_size)
        enemy_y = -enemy_size

    # Kollisionserkennung
    if player_x < enemy_x + enemy_size and player_x + player_size > enemy_x \
            and player_y < enemy_y + enemy_size and player_y + player_size > enemy_y:
        print("Kollision! Spiel vorbei.")
        running = False

    # Hintergrund zeichnen
    screen.fill(WHITE)

    # Spieler und Gegner zeichnen
    pygame.draw.rect(screen, BLACK, (player_x, player_y, player_size, player_size))
    pygame.draw.rect(screen, BLACK, (enemy_x, enemy_y, enemy_size, enemy_size))

    # Bildschirm aktualisieren
    pygame.display.flip()

    # Framerate festlegen
    clock.tick(60)

# Pygame beenden
pygame.quit()
