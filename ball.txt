import pygame
import paddle
import brick
from pygame.math import Vector2
#from paddle import Paddle
class Ball(object):

    def __init__(self, game):
        self.game=game
        self.paddle = paddle.Paddle
        self.size = self.game.screen.get_size()
        self.vx=-6
        self.vy=6
        self.width = 20
        self.height = 20
        self.pos = Vector2(self.size[0]/2,self.size[1]/2)
        self.vel = Vector2(self.vx,self.vy)
        #print(paddle.Paddle.pos1)

    def add_force(self,force):
        self.acc += force

    def bounce_x(self):
        self.vel[0] *= -1

    def bounce_y(self):
        self.vel[1] *= -1
    def tick(self, paddle):

        self.pos += self.vel

        if self.pos.x < 0 or self.pos.x > (self.size[0]-self.width):
            self.bounce_x()
        if self.pos.y > paddle.pos1.y-20 and self.pos.x> paddle.pos1.x and self.pos.x < paddle.pos1.x+ paddle.width:  #potrzebna funcja badająca zderzenie z paletką. osobno dla krawędzi paletki
            self.bounce_y()
        #print(paddle.pos1.y)
        #sprite
        #
        # if self.pos.y.colliderect(prostokąt)
        if self.pos.y <0:
            self.bounce_y()

        if self.pos.y > (self.size[1]-self.height):    
            return True
            
        else:
            return False
        print(self.pos.y)

    def draw(self):

        #Draw
        box = pygame.Rect(self.pos.x, self.pos.y, self.width, self.height)
        pygame.draw.rect(self.game.screen, (180, 180, 255), box)

