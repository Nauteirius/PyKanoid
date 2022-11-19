import pygame, sys
from paddle import Paddle
from ball import Ball
from brick import Brick

#biblioteka pygame
#sterowanie
#klasy
#warunki
#
#13
#8
#9
#

#globalCegly = 20
class Game(object):
    def __init__(self):#dokumentacja, glowne klasy za co odpowiadaja
        #Config
        self.tps_max = 60.0 #liczba FPS
        self.res=1280,720

        #1280,720
        #Initialisation
        pygame.init()
        self.screen=pygame.display.set_mode((self.res))
        self.tps_delta=0.0
        self.tps_clock = pygame.time.Clock()

        self.player = Paddle(self)
        self.destroyer = Ball(self)
        
        self.listBrick=[]
        for i1 in range(1,6):
            for i2 in range (0,4):
                self.listBrick.append(Brick(self,self.res[0]*i1/6, 20+100*i2, 4 - i2)) #wygenerowanie 20 cegiel



        self.cegly = 20

        self.NotEnd = 1
        self.win=0

        while True:

            # Handle Events
            for event in pygame.event.get():
                if event.type == pygame.QUIT:
                    sys.exit(0)
                elif event.type == pygame.KEYDOWN and event.key == pygame.K_ESCAPE:
                    self.box.x += 100

            # Ticking
            self.tps_delta += self.tps_clock.tick() / 1000.0
            while (self.tps_delta > 1/self.tps_max) and self.NotEnd:
                self.tick()
                self.tps_delta -= 1/self.tps_max
                

            #Drawing
            self.screen.fill((0, 0, 0))
            self.draw()
      
        
            if not (self.NotEnd):
                if(self.win == 1):
                    font = pygame.font.Font('freesansbold.ttf', 32)
                    text = font.render('Wygrana', True, (255,255,255))
                    textRect = text.get_rect()
                    #screen.blit(text, (10,10)
                    #textRect.center = (20 // 2, 20 // 2)
                    self.screen.blit(text, textRect)
                    pygame.display.update()
                else:
                    font = pygame.font.Font('freesansbold.ttf', 32)
                    text = font.render('Przegrana', True, (255,255,255))
                    textRect = text.get_rect()
                    #screen.blit(text, (10,10)
                    #textRect.center = (20 // 2, 20 // 2)
                    self.screen.blit(text, textRect)
                    pygame.display.update()
            pygame.display.flip()        

    def tick(self):
        if len(self.listBrick)==0:
            self.NotEnd = 0
            self.win = 1
           

        #if(self.listBrick[0].tick() == True):
       #     self.listBrist.pop(0)
        

        ToRemove=[]
        for item in self.listBrick:
            if item.tick(self.destroyer):
                ToRemove.append (item)

        for item in ToRemove:
            self.listBrick.remove(item)

        self.player.tick()
        if (self.destroyer.tick(self.player)): #,self.bricks
            self.NotEnd=0
            self.win = 0
        # Input

    def draw(self): #,
        for tem in self.listBrick:
            tem.draw()
        self.player.draw()
        self.destroyer.draw()
        for item in self.listBrick:
            item.draw()

#print(pygame.__version__)

if __name__== "__main__":
    Game()

