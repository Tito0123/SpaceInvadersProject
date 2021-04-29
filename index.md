

### Welcome to the SpaceInvaders wiki!

    Team Members: Brice Minix; Tito Oyewole
    
# Overview

This project is a version of the well-known retro arcade game, Space Invaders, that was developed by Tomohiro Nishikado for Taito in 1978. We thought that it would be interesting to produce this game with the ARM Mbed and the I/O hardware that is available in the ECE 4180 kits and in the ECE 4180 lab. We searched the Mbed wiki pages and found that Michael Son had already implemented a basic version of Mbed Space Invaders. Instead of simply building a new version of Space Invaders for the Mbed from scratch, we decided to adapt and improve upon Michel Son's Mbed Space Invaders. Michael Son's Mbed Space Invaders lacks the documentation necessary to reproduce the audio files that were initially required for his version of the game to run, and his version is somewhat buggy with frequent crashing and freezing. He neglected to use the "volatile" keyword that is used by the Mbed cloud compiler for mutual exclusion with global variables, and he often uses the wait() function (that locks up the processor) when the Thread::wait() function (that allows other threads to run while one thread waits) should have been used. Michael Son's version also uses basic squares (drawn with uLCD.filled_rectangle()) for the player and enemies instead of sprites, and his game menu has only one option (to start the game) and does not allow for cursor movement. The score in his version is calculated such that any winner of the game would have the same score; the score is based only on the number of enemies defeated. His game also lacks the barriers that the player could hide behind in the original game (until the player's or enemies' missiles destroyed them). The controls for Michel Son's version consist of only a pushbutton and a somewhat uncomfortable 5-way tactile switch (navigation switch) that allowed for only one speed of movement to the left or right. However, his game does offer a good foundation for the basic mechanics of the Space Invaders game. Michael Son’s Space Invaders is the foundation upon which we built our game, and the features/changes we implemented to make our game unique are listed below along with some important explanations and instructions:


1. Joystick/IMU Controls: Micheal Son's game uses a somewhat uncomfortable navigation switch (5-way tactile switch) to browse through the game menu and move the ship (the player) to the left and right. This navigation switch allows for only one speed of movement to the left and right (less fluid control). Our version of the game uses both a SparkFun thumb joystick and a SparkFun 9 Degrees of Freedom IMU (LSM9DS1) (uses the accelerometer via tilting) for smoother movement and a more comfortable feel. The speed of movement depends on how much the joystick is pushed and/or how much the board is tilted. Clicking the joystick also changes the color of the player (the ship); this essentially adds a basic "skin" feature. The player can choose to be green, blue, pink, purple, or yellow by repeatedly clicking the joystick. To more easily allow the player to choose their color, we require that the joystick's button be released and pushed again for each change in color. The link to the joystick library used can be found in the References/Citation Section; this library offers useful functions that can be used to offer a lot of flexibility with using the joystick.
2. Pushbutton: Both versions of the game use a pushbutton to select an option on the menu screen (different levels/difficulties) and shoot missiles at the rows of enemies.
3. Speakers: Our version of the game utilizes a speaker and a class D audio amplifier to play sounds that are in sync with the different game states (e.g., victory music (with a win), gameover music, game menu music, missile fired sound (when the player fires a missile), and an explosion sound (when the player gets hit with an enemy missile and loses a life)). This sound effects are implemented with the waveplayer library and are played from a separate thread (from the main thread). Although Michael Son's game originally had music and sound effects, he did not make these sound files available to the users; he also did not have victory music that plays when the player wins. The links to the source sound files we used are in the References/Citation section. These sound files can be edited with Audacity to decrease their frequencies to 16-44.1 kHz to export them as 16-bit wave files (as we did). Finally, It is also important to note that while recreating our version, the sound files (.wave files) need to be saved in a folder called "wavfiles," which should be stored on the SD card.
4. Barriers: To make our game more complex, we added barriers that can be used to shield the player. These barriers will break down when they are hit by the enemy or player missiles. (When missiles hit the barrier, they are destroyed, and a chunk of the green barrier pixels becomes black. Missiles can pass through these gaps). This feature was not originally included in Micheal Son's game at all.
5. Levels: Our game has three levels that correspond to 3 different difficulties. All 3 levels are added as options in the menu, and the cursor can be moved to each of these options by tilting the board (with the IMU accelerometer) or by moving the joystick. The level is selected by pushing the pushbutton. The game becomes more difficult as the player proceeds to the next level (LEVEL 1 = easy, LEVEL 2 = medium, LEVEL 3 = hard). As the difficulty increases, the number of barriers present in the game reduces, the enemies' missiles are shot at an increased speed, and the number of lives reduces. In LEVEL 1, the player has 3 lives, the enemies' missiles move slowly, and there are 4 barriers. In LEVEL 2, the player has 2 lives, the enemies' missiles move faster, and there are 2 barriers. In LEVEL 3, the player has only 1 life, the enemies' missiles move very fast, and there is only 1 barrier. On the other hand, Michel Son's game had only one basic level without any of the features mentioned above; his version had only one menu option.
6. RGB LED lighting effects: Similarly to the music and sound effects, RGB LED lighting effects correspond with different states of the game. These effects are triggered once the game starts (i.e., at the game menu screen), when the player is hit with a missile, when the player loses, and when the player wins. During the game menu, the RGB LED alternates between red, green, and blue as it brightens and dims with PWM to a maximum of half brightness (0.5). When the player is hit with a missile, the red LED flashes three times at half brightness (0.5 PWM). When the player loses, the red LED brightens and dims with PWM to a maximum of one-quarter brightness (0.25). When the player wins, the green LED brightens and dims with PWM to a maximum of one-quarter brighteness (0.25). The RGB LED lighting effects are implemented in a separate thread (from the main thread). Again, this is another feature that makes our version different from Michael Son's.
7. High Score: Since Michael Son's score calculation only took into account the number of enemies defeated, the high score was always the same for winning players, regardless of how fast the player finished the game. Our version uses a more realistic and complex method of computing the score. We achieved this by subtracting the time duration of the game from the product of the usual score calculation (that depends on the number of enemies defeated) (implemented in Michael Son's game) and the game level. The time duration since the game began is determined by starting a Timer when the game begins and stopping and resetting the timer when the game finishes. This method makes sure that the difficulty of the level and time duration are taken into account when determining the score (and allows for more unique scores among winners). The highest score is stored on the SD card. The highest score is read from the SD card and displayed at the bottom of the game menu. A "highscore.txt" file will need to be created and stored on the SD card to recreate this method; this file should be initialized by typing a 0, hitting the return key, and saving the file (the high score is initialized to 0).
8. Enemy/Player Sprite: Michael Son's game utilizes the rectangle member function (uLCD.filled_rectangle()) of the uLCD class to create the enemy and player sprites (simple squares). Our version implements more realistic-looking enemy and player sprites that closely resemble that of the original game created by Tomohiro Nishikado. We use the uLCD.BLIT() function to do this.
9. Temporary Change of Player's Color When Hit: When the player is hit with a missile, the player briefly flashes red (as the RGB LED flashes and the explosion/death sound effect is played) before the player is returned to their previously chosen color. 
10. Potentiometer: This is wired to the class D audio amplifier and can be turned to control the volume of the speaker (not present in Michael Son's version of the game).
11. Fixed Bugs: We reduced some of the buggy behavior present in Michael Son's Mbed Space Invaders by adding the "volatile" keyword to global variables. (This tells the Mbed cloud compiler to use mutual exclusion with global variables that may be shared among different threads orr used in interrupt service routines). We also use Thread::wait() instead of wait() so that other threads can run while one thread waits instead of simply locking up the processor.

Michael Son's Mbed Space Invaders inspired our version of the game. The link to his wiki page can be found in the References/Citation section.

# Components Used
1.  ARM Mbed (LPC1768)
2.  uLCD-144-G2 128 by 128 Smart Color LCD
3.  Pushbutton
4.  LSM9DS1 IMU (SparkFun 9 Degrees of Freedom IMU)
5.  RGB LED (with some 100 ohm resistors)
6.  Sparkfun Thumb Joystick
7.  MicroSD Card with microSD Transflash Breakout (from Sparkfun)
8.  Speaker
9.  Class D Audio Amplifier (from Sparkfun)
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
|p22         |        |                  |            |           | Green |    |         |      |             |
|p23         |        |                  |            |           | Blue  |    |         |      |             |
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
![image Schematic](https://github.com/Tito0123/SpaceInvadersProject/blob/master/schematics.png?raw=true)


# Setup

![image of space invaders Game Menu](https://github.com/Tito0123/SpaceInvadersProject/blob/master/IMG_5261.jpg?raw=true, "Game Menu")

![image of space invaders Game Screen](https://github.com/Tito0123/SpaceInvadersProject/blob/master/IMG_5268.jpg?raw=true,"Game Screen")

# Demo Video 
[![Alternate Text](https://github.com/Tito0123/Space_invadersbyTitoandBrice/blob/master/Screen%20Shot%202021-04-28%20at%204.27.09%20PM.png?raw=true)](https://www.youtube.com/watch?v=GOonE07fTdg "Place holder")

# Future Improvements
1. When we set out to recreate this game, we wanted to implement a two-player Space Invaders game using two mbeds, two screens, e.t.c. However, we quickly ran into some technical difficulties while attempting to form a means of communication between the two mbeds. We eventually figured it out, but time would not allow us to proceed on this path. Currently, the two mbeds can communicate with each other, and we have the primitives for this setup commented out in our code. In the future, we will move forward with our idea of two players competing to get the highest scores.
2. More work needs to be done to make both versions of the game less buggy.
3. We can further improve the animations of the game and the sound quality.
4. We can make more involved skins instead of simply changing the color of the player.

# References/Citation
[comicalgameoverEdit (gameover)](https://freesound.org/people/themusicalnomad/sounds/253886/) 

[bigExplosionEdit2 (death)](https://freesound.org/people/tcpp/sounds/77339/) 

[futureEdit2 (intro)](https://freesound.org/people/VABsounds/sounds/443865/) 

[laserEdit (missile)](https://freesound.org/people/nsstudios/sounds/321102/) 

[victoryEdit2 (win)](https://freesound.org/people/honeybone82/sounds/513253/)  

[Starter Code: Michael Son’s Mbed Space Invaders](https://os.mbed.com/users/michaeljson/notebook/mbed-space-invaders/) 

[SparkFun Analog Joystick](https://os.mbed.com/teams/a/code/SparkfunAnalogJoystick//file/2b40241a7675/SparkfunAnalogJoystick.cpp/) 

[Space Invaders Soundtrack Website](https://www.classicgaming.cc/classics/space-invaders/sounds)  
IT IS UNKNOWN IF THESE ARE SAFE. SOME REDDITORS HAVE STATED THAT THIS SITE IS NOT LEGIT, BUT SOME SAY THEY HAVE USED IT WITHOUT CONSEQUENCES YET.  

[Barrier inspiration](https://os.mbed.com/users/DNoved1/notebook/space-invaders-clone/) 

[Speaker Sound Control](https://os.mbed.com/users/4180_1/notebook/tpa2005d1-class-d-audio-amp/) 

 


