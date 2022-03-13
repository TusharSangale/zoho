Use Pycharm app to run game
code is
import pygame

# initialize
pygame.init()

WHITE = (255, 255, 255)
DARKBLUE = (36, 90, 190)
BLACK= (0, 0, 0)
GREEN1 = (0, 255, 0)

# bricks

bricks1 = [pygame.Rect(10 + i * 100, 60, 80, 30) for i in range(7)]
bricks2 = [pygame.Rect(10 + i * 100, 100, 80, 30) for i in range(7)]
bricks3 = [pygame.Rect(10 + i * 100, 140, 80, 30) for i in range(7)]
bricks4 = [pygame.Rect(10 + i * 100, 180, 80, 30) for i in range(7)]
bricks5 = [pygame.Rect(10 + i * 100, 220, 80, 30) for i in range(7)]
bricks6 = [pygame.Rect(10 + i * 100, 260, 80, 30) for i in range(7)]
bricks7 = [pygame.Rect(10 + i * 100, 300, 80, 30) for i in range(7)]

# brick draw on screen

def draw_brick(bricks):
    for i in bricks:
        pygame.draw.rect(screen, GREEN1, i)


score = 0

velocity = [1, 1]

size = (800, 800)

screen = pygame.display.set_mode(size)

pygame.display.set_caption("My Bricks Game")

paddle = pygame.Rect(100, 550, 200, 10)
ball = pygame.Rect(50, 250, 10, 10)

gameContinue = True

while gameContinue:
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            gameContinue = False

    screen.fill(DARKBLUE)

    pygame.draw.rect(screen, BLACK, paddle)

    font = pygame.font.Font(None, 34)

    text = font.render("SCORE " + str(score), 1, WHITE)

    screen.blit(text, (20, 10))

    # paddle move:
    if event.type == pygame.KEYDOWN:
        if event.key == pygame.K_RIGHT:
            if paddle.x < 740:
                paddle.x = paddle.x + 5

        if event.key == pygame.K_LEFT:
            if paddle.x > 0:
                paddle.x = paddle.x - 5

    # creating bricks
    draw_brick(bricks1)
    draw_brick(bricks2)
    draw_brick(bricks3)
    draw_brick(bricks4)
    draw_brick(bricks5)
    draw_brick(bricks6)
    draw_brick(bricks7)

    # ball movement
    ball.x = ball.x + velocity[0]
    ball.y = ball.y + velocity[1]

    if ball.x > 700 or ball.x < 0:
        velocity[0] = -velocity[0]

    if ball.y <= 7:
        velocity[1] = -velocity[1]

    if paddle.collidepoint(ball.x, ball.y):
        velocity[1] = -velocity[1]

    if ball.y >= 790:
        font = pygame.font.Font(None, 84)
        text = font.render("Game Over..!! ", 1, GREEN1)
        screen.blit(text, (150, 350))

        pygame.display.flip()

        pygame.time.wait(2000)

        break;
    pygame.draw.rect(screen, WHITE, ball)

    for i in bricks1:
        if i.collidepoint(ball.x, ball.y):
            bricks1.remove(i)
            velocity[0] = -velocity[0]
            velocity[1] = -velocity[1]
            score = score + 1

    for i in bricks2:
        if i.collidepoint(ball.x, ball.y):
            bricks2.remove(i)
            velocity[0] = -velocity[0]
            velocity[1] = -velocity[1]
            score = score + 1

    for i in bricks3:
        if i.collidepoint(ball.x, ball.y):
            bricks3.remove(i)
            velocity[0] = -velocity[0]
            velocity[1] = -velocity[1]
            score = score + 1

    for i in bricks4:
        if i.collidepoint(ball.x, ball.y):
            bricks4.remove(i)
            velocity[0] = -velocity[0]
            velocity[1] = -velocity[1]
            score = score + 1

    for i in bricks5:
        if i.collidepoint(ball.x, ball.y):
            bricks5.remove(i)
            velocity[0] = -velocity[0]
            velocity[1] = -velocity[1]
            score = score + 1

    for i in bricks6:
        if i.collidepoint(ball.x, ball.y):
            bricks6.remove(i)
            velocity[0] = -velocity[0]
            velocity[1] = -velocity[1]
            score = score + 1

    for i in bricks7:
        if i.collidepoint(ball.x, ball.y):
            bricks7.remove(i)
            velocity[0] = -velocity[0]
            velocity[1] = -velocity[1]
            score = score + 1

    if score == 49:
        font = pygame.font.Font(None, 84)
        text = font.render("Hurray..!!", 1, GREEN1)
        screen.blit(text, (150, 350))
        pygame.display.flip()

        pygame.time.wait(3000)
        break;

    pygame.time.wait(3)
    pygame.display.flip()

pygame.quit()
