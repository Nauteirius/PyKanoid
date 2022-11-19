import pygame
import ball
from pygame.math import Vector2

class Paddle(object):
    def __init__(self, game):
        self.game=game
        self.ball = ball
        self.speed=1.2

        self.size = self.game.screen.get_size()

        self.pos1 = Vector2(self.size[0]/2,self.size[1]-22) #nie dziala
        self.vel = Vector2(0,0)
        self.acc = Vector2(0,0)

        self.width = 100
        self.height = 20

    def add_force(self,force):
        self.acc += force

    def tick(self):
        #Input
        pressed = pygame.key.get_pressed()
        if pressed[pygame.K_LSHIFT]:
            self.speedmax=self.speed * 2
        else: self.speedmax = self.speed

        if pressed[pygame.K_d] or pressed[pygame.K_RIGHT]:
            self.add_force(Vector2(self.speedmax,0))

        if pressed[pygame.K_a] or pressed[pygame.K_LEFT]:
            self.add_force(Vector2(-self.speedmax, 0))

        if self.pos1.x < 0:
            self.vel.x *=-1
            self.pos1.x += 5

        if self.pos1.x > (self.size[0]-self.width):
            self.vel.x *=-1
            self.pos1.x += -5
            #przy tzrymaniu klawisza shift i strzalki w prawo paletka czasami sie na ułamek sekundy buguje i ląduje częściowo poza ekranem
        else:

            #realistyczne sterowanie paletką, przy tzrymaciu przycisku SHift paletka porusza sie 2x szybciej
            #Phys
            self.vel *= 0.90
            self.vel += self.acc
            self.pos1 += self.vel
            self.acc *= 0

    def draw(self):

        #Draw
        box = pygame.Rect(self.pos1.x, self.pos1.y, self.width, self.height)
        pygame.draw.rect(self.game.screen, (0, 180, 255), box)
