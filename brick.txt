import pygame
import ball
from pygame.math import Vector2

class Brick(object):
    #self.pos2 = Vector2(100,100)

    def __init__(self, game, X, Y, Z):
        #self.brick = brick
        self.game=game
        self.height = 20
        self.width = 60
        self.pos2 = Vector2(X,Y) 
        self.hp = Z


    #def Destroy(self):
    #    self.kill()

    def tick(self, ball):
        
        if self.pos2.y-20 < ball.pos.y and self.pos2.y + self.height> ball.pos.y and self.pos2.x < ball.pos.x+10 and self.pos2.x + self.width > ball.pos.x:  #kolizja piłki i cegły
            ball.bounce_y()
            #print("kolizja")
            self.hp = self.hp - 1
            if self.hp == 0:
                return True
            else: 
                return False
             #ball.bounce_y()
             #self.Destroy()
    #     print(paddle.pos1.y)
    #     #sprite
    #     #
    #     # if self.pos.y.colliderect(prostokąt)
    #     if self.pos.y <0 or self.pos.y > (self.size[1]-self.height):
    #         self.bounce_y()
    #     print(self.pos.y)



    def draw(self):
    #Draw
        if self.hp == 1:
            color = (255, 0, 0)
        elif self.hp == 2:
            color = (255,255,0)
        elif self.hp == 3:
            color = (0,255,0)
        else:
            color = (0,0,255)

        goal = pygame.Rect(self.pos2.x, self.pos2.y, self.width, self.height)
        pygame.draw.rect(self.game.screen, color, goal)



