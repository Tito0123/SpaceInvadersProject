







### Welcome to the SpaceInvaders wiki!

    Team Members: Brice Minix; Tito Oyewole
    
# Overview

This project is a version of the Nokia space invaders with the following features:
1. Joystick/IMU: used to browse through the game menu and control the ship. Clicking the joystick also changes the color of the player.
2. Pushbutton: used to select an option on the menu screen and shoot sprites at the rows of enemies.
3. Speakers: plays music that is in sync with the game (some examples include: victory/losing sound, game menu sound, sprite fired sound e.t.c)
4. Levels: In the first level, the player has three lives; in the second level, the player has two lives, and in the third level, the player   has one life.
5. LED lighting effect: These effects are triggered once the game starts (i.e., at the game menu screen), when the player fires a shot, during a victory e.t.c  
6. Barriers: four barriers shields the player from the enemy missiles. These barriers break down once they have been hit by a missile or by the player.
7. Best Time: This version of space invaders also keeps track of the best time i.e., the fastest time in which the game is completed.
8. Potentiometer: Used to control the volume of the speaker.

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

# Demo Program

# Demo Video 



Whenever you commit to this repository, GitHub Pages will run [Jekyll](https://jekyllrb.com/) to rebuild the pages in your site, from the content in your Markdown files.

### Markdown

Markdown is a lightweight and easy-to-use syntax for styling your writing. It includes conventions for

```markdown
Syntax highlighted code block

# Header 1
## Header 2
### Header 3

- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text

[video](https://www.youtube.com/watch?v=UjkHr5F6Njw) and ![Image](src)
```

For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/Tito0123/Space_invadersbyTitoandBrice/settings/pages). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://docs.github.com/categories/github-pages-basics/) or [contact support](https://support.github.com/contact) and we’ll help you sort it out.
