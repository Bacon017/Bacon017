import pygame
import random

# Initialize pygame
pygame.init()

# Screen dimensions
WIDTH, HEIGHT = 800, 600
screen = pygame.display.set_mode((WIDTH, HEIGHT))
pygame.display.set_caption("Mini Battle Royale")

# Colors
WHITE = (255, 255, 255)
RED = (255, 0, 0)

# Player settings
player_size = 50
player_pos = [WIDTH // 2, HEIGHT // 2]
player_speed = 10

# Enemy settings
enemy_size = 50
enemy_pos = [random.randint(0, WIDTH-enemy_size), 0]
enemy_speed = 5

# Clock to control frame rate
clock = pygame.time.Clock()

# Game loop
running = True
while running:
    screen.fill(WHITE)

    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            running = False

    # Get key presses
    keys = pygame.key.get_pressed()

    # Player movement
    if keys[pygame.K_LEFT] and player_pos[0] > 0:
        player_pos[0] -= player_speed
    if keys[pygame.K_RIGHT] and player_pos[0] < WIDTH - player_size:
        player_pos[0] += player_speed
    if keys[pygame.K_UP] and player_pos[1] > 0:
        player_pos[1] -= player_speed
    if keys[pygame.K_DOWN] and player_pos[1] < HEIGHT - player_size:
        player_pos[1] += player_speed

    # Update enemy position
    enemy_pos[1] += enemy_speed
    if enemy_pos[1] > HEIGHT:
        enemy_pos = [random.randint(0, WIDTH-enemy_size), 0]

    # Draw player
    pygame.draw.rect(screen, RED, (player_pos[0], player_pos[1], player_size, player_size))

    # Draw enemy
    pygame.draw.rect(screen, RED, (enemy_pos[0], enemy_pos[1], enemy_size, enemy_size))

    pygame.display.update()

    clock.tick(30)

pygame.quit()

