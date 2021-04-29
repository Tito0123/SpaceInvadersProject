

### Welcome to the SpaceInvaders wiki!

    Team Members: Brice Minix; Tito Oyewole
    
# Overview

1. Joystick/IMU: Micheal Son's game uses a navigation switch to browse through the game menu and control the ship. Our version of the game uses both a joystick and an IMU for smoother movement and a more comfortable feel. Clicking the joystick also changes the color of the player. The link to the joystick can be found in the References/Citation Section.
2. Pushbutton: Both versions of the game use a pushbutton to select an option on the menu screen and shoot missiles at the rows of enemies.
3. Speakers: Our version of the game utilizes a speaker and a class D amplifier to play sounds that are in sync with the game (e.g., victory/losing sound, game menu sound, missile fired sound, e.t.c). This feature is not present in Micheal Son's game. The links to the sounds we used are in the References/Citation section. Finally, It is also important to note that while recreating our version, the sound files (.wave files) need to be saved in a folder called "wavfiles," which should be stored on the SD card.
4. Barriers: To make our game more complex, we added barriers to shield the player. These barriers will break down when they are hit by the enemy or player missiles. This feature was not originally included in Micheal Son's game.
5. Levels: Our game has three levels. The game becomes more difficult as the player proceeds to the next level. The number of barriers present in the game reduces, the missiles are shot at an increased speed, and the number of lives reduces. On the other hand, Michel Son's game had one level without any of the features mentioned above. 
6. LED lighting effect: These effects are triggered once the game starts (i.e., at the game menu screen), when the player fires a shot, during a victory e.t.c. Again, this is another feature that makes our version different from Michael Son's.
7. High Score: Since Michael Son's game had one level, the high score was always the same, regardless of how fast the player finished the game. Our version uses a more realistic and complex method of computing the score. We achieved this by subtracting the time duration of the game from the product of the usual score calculation (implemented in Michael Son's game)and the game level. This method makes sure that the difficulty of the level and time duration are taken into account when determining the score. A "highscore.txt" file will need to be created and stored on the SD card to recreate this method.
8. Enemy/Player Sprite: Michael Son's game utilizes the rectangle member function of the uLCD class to create the enemy and player sprites. Our version implements a more realistic-looking enemy and player sprite that closely resembles that of the original game created by Tomohiro Nishikado. 
9. Potentiometer: This is used to control the volume of the speaker.

Michael Son's Mbed Space Invaders inspired our version of the game. The link to his wiki page can be found in the References/Citation section.
# Components Used
1.  mbed
2.  uLCD
3.  Pushbutton
4.  LSM9DS1 IMU
5.  RGBLED
6.  Joystick
7.  SDCard
8.  Speaker
9.  Class D audio amp
10. Potentiometer

# Wiring

|mbed        |Speaker |Class D audio amp |uLCD header |Pushbutton |RGBLED |IMU |Joystick |SDCard|Potentiometer|
|------------|--------|------------------|------------|-----------|-------|----|---------|------|-------------|
|GND         |        | pwr -            |     GND    |  -        |GND    |GND |GND      |GND   |             |       
|Vout(3.3V)  |        | pwr +            |            |           |       |VDD |  VCC    |VCC   |             |
|p18         |        | in +             |            |           |       |    |         |      |             |
|            | +      | out +            |            |           |       |    |         |      |             |      
|            | -      | out -            |            |           |       |    |         |      |             |                                                         
|VU = 5V     |        |                  |5V(External)|           |       |    |         |      |             |
|TX = p28    |        |                  |    RX      |           |       |    |         |      |             |                       
|RX = p27    |        |                  |    TX      |           |       |    |         |      |             |
|p29         |        |                  |    Reset   |           |       |    |         |      |             |
|p20         |        |                  |            | +         |       |    |         |      |             |       
|p21         |        |                  |            |           |  Red  |    |         |      |             |
|p22         |        |                  |            |           |  Blue |    |         |      |             |
|p23         |        |                  |            |           | Green |    |         |      |             |
|p9          |        |                  |            |           |       |SDA |         |      |             |
|p10         |        |                  |            |           |       |SCL |         |      |             |
|p15         |        |                  |            |           |       |    |VERT     |      |             |
|p16         |        |                  |            |           |       |    |HORZ     |      |             |
|p17         |        |                  |            |           |       |    | SEL     |      |             |
|p8          |        |                  |            |           |       |    |         | CS   |             |
|p5          |        |                  |            |           |       |    |         | DI   |             |
|p7          |        |                  |            |           |       |    |         |SCK   |             |
|p6          |        |                  |            |           |       |    |         | DO   |             |
|            |        |                  |            |           |       |    |         | CD   |             |
|            |        |  Volume (Top)    |            |           |       |    |         |      | Top         |
|            |        |  Volume (Middle) |            |           |       |    |         |      | Middle      |
|            |        |  Volume (Bottom) |            |           |       |    |         |      | Bottom      |

# Schematic

# Setup
![image of space invaders setup](https://github.com/Tito0123/Space_invadersbyTitoandBrice/blob/master/IMG_5252.jpg?raw=true "setup")

# Demo Video 
[![Alternate Text](https://github.com/Tito0123/Space_invadersbyTitoandBrice/blob/master/Screen%20Shot%202021-04-28%20at%204.27.09%20PM.png?raw=true)](https://www.youtube.com/watch?v=GOonE07fTdg "Place holder")

#Future Improvements
1. When we set out to recreate this game, we wanted to implement a two-player Space Invaders game using two mbeds, two screens, e.t.c. However, we quickly ran into some technical difficulties while attempting to form a means of communication between the two mbeds. We eventually figured it out, but time would not allow us to proceed on this path. Currently, the two mbeds can communicate with each other, and we have the primitives for this setup commented out in our code. In the future, we will move forward with our idea of two players competing to get the highest scores.
2. More work needs to be done to make both versions of the game less buggy.
3. We can further improve the animations of the game and the sound quality.

# References/Citation
[comicalgameoverEdit (gameover)](https://freesound.org/people/themusicalnomad/sounds/253886/) 

[bigExplosionEdit2 (death)](https://freesound.org/people/tcpp/sounds/77339/) 

[futureEdit2 (intro)](https://freesound.org/people/VABsounds/sounds/443865/) 

[laserEdit (missile)](https://freesound.org/people/nsstudios/sounds/321102/) 

[victoryEdit2 (win)](https://freesound.org/people/honeybone82/sounds/513253/)  

[Starter Code: Michael Son’s Mbed Space Invaders](https://os.mbed.com/users/michaeljson/notebook/mbed-space-invaders/) 

[SparkFun Analog Joystick](https://os.mbed.com/teams/a/code/SparkfunAnalogJoystick//file/2b40241a7675/SparkfunAnalogJoystick.cpp/) 

[Space Invaders Soundtrack Website](https://www.classicgaming.cc/classics/space-invaders/sounds)  
IT IS UNKNOWN THAT THESE ARE SAFE. SOME REDDITORS HAVE STATED THAT THIS SITE IS NOT LEGIT, BUT SOME SAY THEY HAVE USED IT WITHOUT CONSEQUENCES YET.  

[Used for barrier inspiration](https://os.mbed.com/users/DNoved1/notebook/space-invaders-clone/) 

[Speaker Sound Control](https://os.mbed.com/users/4180_1/notebook/tpa2005d1-class-d-audio-amp/) 

 



