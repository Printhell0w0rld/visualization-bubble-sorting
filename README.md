# visualization-bubble-sorting
visualization bubble sorting
```Python 
import pygame,sys
import time
import random

FPS=60
WIDTH=700
HEIGHT=500
arr=[]
judge=0

pygame.init()
pygame.display.set_caption('Sorting')# name of the window
screen=pygame.display.set_mode([WIDTH,HEIGHT])
clock=pygame.time.Clock()


font_name=pygame.font.match_font('arial')
def draw_text(surf,text,size,x,y):
    font=pygame.font.Font(font_name,size)
    text_surface=font.render(text,True,[255,255,255])
    text_rect=text_surface.get_rect()
    text_rect.centerx=x
    text_rect.top=y
    surf.blit(text_surface,text_rect)

def draw_init():
    screen.fill((0,0,0))
    draw_text(screen,'Click any bottom to start',50,WIDTH//2,HEIGHT//3+20)
    pygame.display.update()
    waiting=True
    while waiting:
        clock.tick(FPS)
        for event in pygame.event.get():
            if event.type==pygame.QUIT:
                sys.exit()
            elif event.type==pygame.KEYDOWN:
                waiting=False

for i in range(1,201):
    arr+=[i]
random.shuffle(arr)
ans=sorted(arr)


show_init=True
while True:
    if show_init:
        draw_init()
        show_init=False
    clock.tick(600)
    for event in pygame.event.get():
        if event.type==pygame.QUIT:
            sys.exit()

    screen.fill((0,0,0))
    w=2
    for i in range(200):
        pygame.draw.rect(screen,[255,255,255],[50+i*(w+1),300-arr[i],w,arr[i]],0)
    for i in range (199):
        for j in range(199-i):
            if judge==1:
                break
            if (arr[j] > arr[j+1]):
                arr[j], arr[j+1]= arr[j+1],arr[j]
                judge=1
        if judge==1:
            judge=0
            break
    if ans==arr:
        draw_text(screen,'Finish',50,350,400)
    pygame.display.update()

```
