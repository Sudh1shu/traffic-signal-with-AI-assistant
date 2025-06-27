
# traffic-signal-with-AI-assistant
import time
import pygame
import pyttsx3

class TrafficSignal:
    def __init__(self):
        self.state = 'RED'
        self.green_duration = 30  
        self.yellow_duration = 5  
        self.red_duration = 30   
        
        
        self.engine = pyttsx3.init()
        
        
        pygame.init()
        self.screen = pygame.display.set_mode((300, 500))
        pygame.display.set_caption("Traffic Signal")

    def speak(self, message):
        self.engine.say(message)
        self.engine.runAndWait()

    def draw_signal(self):
        self.screen.fill((0, 0, 0))

        
        red_color = (255, 0, 0) if self.state == 'RED' else (100, 0, 0)
        pygame.draw.circle(self.screen, red_color, (150, 100), 50)

        
        yellow_color = (255, 255, 0) if self.state == 'YELLOW' else (100, 100, 0)
        pygame.draw.circle(self.screen, yellow_color, (150, 250), 50)

        
        green_color = (0, 255, 0) if self.state == 'GREEN' else (0, 100, 0)
        pygame.draw.circle(self.screen, green_color, (150, 400), 50)

        pygame.display.flip()

    def change_signal(self):
        if self.state == 'RED':
            self.speak("Signal is Red. Please wait.")
            self.draw_signal()
            time.sleep(self.red_duration)
            self.state = 'GREEN'
        elif self.state == 'GREEN':
            self.speak("Signal is Green. You may cross the road.")
            self.draw_signal()
            time.sleep(self.green_duration)
            self.state = 'YELLOW'
        elif self.state == 'YELLOW':
            self.speak("Signal is Yellow. Prepare to stop.")
            self.draw_signal()
            time.sleep(self.yellow_duration)
            self.state = 'RED'

    def run(self):
        running = True
        while running:
            for event in pygame.event.get():
                if event.type == pygame.QUIT:
                    running = False
            self.change_signal()

        pygame.quit()

if __name__ == "__main__":
    signal = TrafficSignal()
    signal.run()
