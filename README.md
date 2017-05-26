# BikeMessenger By Sanjeev Sharma
                  
# Description of app:
BikeMessenger is a simple 2d side scroller. The game features a simple navigation scheme, press and hold on screen to move the player up, release to bring the player down. In the player’s path are few different objects of interest:
- Regular Packages (in the form of a black and white boxes)
- Red Packages (in the form of boxes with a red bow on top)
- Taxis
- Nails

The point scheme is simple, collect the packages to help your player make more money as a bike messenger. Below is the points breakdown:
- Regular Packages = $10.00
- Red Packages = $20.00

So why are the red packages worth more than the regular packages? Because they move faster across the screen.
But what would be a game without things trying to kill you? To solve this dilemma, there are the vicious nails and insane taxi drivers in your player’s path to riches (can you feel my excitement). Avoid at all cost. May the force be with you.
Also, there are some sound effects and a simple high score display that shows at the game over sequence.

# Installation: 
The game is not yet available on the Play Store, as there is much I would like to eventually add. For now:  
The .apk (app-debug.apk) can be found in the following path: BikeMessenger\app\build\outputs\apk
1. Drag and drop app-debug.apk onto your device
2. Be sure your device setting allows apps to be installed from unknown sources
3. Find .apk file on device using a file browser
4. Tap to install 
*You can also email me at sanjeev.sharma90@myhunter.cuny.edu if you want the apk to be sent to your phone through email.

# Description of Code design:
There are three Activities in this application:
1. MainActivity: Where all of the actual gameplay logic is implemented
2. MenuActivity: The main menu Activity. Very simple, starts the MainActivity
3. ResultActivity: This activity handles he logic behind displaying the result of the last game played.

>MainActivity

As stated earlier, this is where the actual logic behind the gameplay is implemented. There are 4 main things taking place here:

1. Position
  - We start the position of the messenger in the middle of the screen and the potential points and enemies off screen.
  - We change the position of the player along the Y axis and the non-player objects along the x-axis.
  - Position is especially important in keeping all objects on display. This can be seen in changePos() where the player is kept from     falling off of frame using the objects Y coordinate.

2. Movement
  - Implemented in the changePos() class.
  - Implementation of the movement of each of the non-player objects is more or less the same. The exceptions being the speed of movement across the screen of each object.
  - The use of Math.random() is leveraged multiplied by the height of the game frame – the height of each object.
  Math.random() is used to randomize the Y axis on which the objects appear and the second half of the equation
  is to insure that the objects always appear on some Y in the frame and not outside of it.
  - In the case of the player object, we vary on the Y axis instead of the X. This is because we want to move the
  messenger up and down the screen, not across it. The touch input is handled by motionEvent.getAction() in the
  onTouch event. Move_check (Boolean) is used to check if the screen is receiving input or not. Simply put, if a
  finger is on the screen, move_check is true and messenger goes up on the screen. If it is false, meaning not touch
  input is being received, the messenger goes down the screen.
  
3. Speed
  - Through this project, I learned how much of a deviation in game speed can occur across different screen sizes
  and resolutions. My initial idea was to set hard coordinate update numbers for each of the objects, but I realized
  it would make for a different experience on different devices.
  - After doing some research, I found it is much better to set speed but referring to the width and height of the
  actual screen. This was done by capturing the size of x and y in integer variables and dividing that by some
  number to achieve the speed you are looking for.
  
4. Hit detection
  - Hit detection is handles by finding the midpoint of the non player objects first, and then seeing if the center of
  the objects makes contact with the biker. This is done through an if statement and Boolean algebra. Upon
  hitting, the various non player objects their own set of code. The user of a timer is implemented to aid in
  stopping and starting the game.

>MenuActivity

  This activity was made to be used for the main menu of the game. The XML portion handles displaying the simple rules of the
  game while the java file handles the play button. This button starts the MainActivity.

>ResultActivity

  This activity is started when the player either registers a hit with a nail or a taxi. It displays the Game Over textview and shows
  what the players score was for the game. There is also a high score tracker. It compares the current game score of the player
  with the the previously saved high score. If the current score is higher, it updates the score to the current score. If it is less, the
  high score stays the same.

>Sounds (class)

  This was not included above because it is only a java class. This class handles the 3 basic sounds in this game. The sound played
  when collecting any of the packages, and the 2 different sounds played for the nail and taxi object. This is done using a
  SoundPool and the calling playSound functions in the hitterOrQuitter portion of the main activity.
