In milestone 3, I focused mostly on the final touches, you know, the cherry on the cake. This was also when I could finally see the whole game coming together, which was very rewarding.
I started by finally adding the enemies. Because of my previous debugging, I had already combined all spawners into one SpawnManager script, which I actually liked, so I kept it. I added headers above each object section so it was easier to see which variables belonged to obstacles, platforms, chocolate, or enemies.
Once I added the enemies, nothing broke and almost nothing overlapped, which almost brought tears of joy. Then I balanced the spawn chances. After testing, I found the right balance. I also gave the enemies a small animation from BigManJD’s assets and added simple AI behaviour. If the player gets too close, the enemy gets annoyed, changes color slightly, and moves towards the player. Very rude of them, but also pretty cool.
I changed the chocolate bar so it starts at 70%. Before that, it was too hard to fill, and it felt like the bar barely changed no matter how much chocolate spawned (even when chance=96). Starting at 70% made the attack mechanic easier to reach and more fun.
After that, I made the game look nicer. I found a UI asset package by Devnik2D with pixel art elements that fit the game’s style. I replaced the basic buttons on the panels and added a visible pause button during gameplay, so the player knows the game can be paused.
Then I used Canva to make an image for the main menu and some tutorial images. I added the tutorial as a small carousel with arrow-style buttons from Devnik2D’s assets. The tutorial images do not loop, so at the end the player has to go backwards, but I do not think that is an issue.
At this point, I realised the character still could not attack. So I quickly made a brown chocolate ball in Piskel and created two scripts: PlayerAttack and ChocoAttack. PlayerAttack checks the ChocolateManager, throws the chocolate ball if there is enough chocolate, and drains the attack cost. ChocoAttack controls the ball’s speed, lifetime, and what it can destroy. As a small hidden detail, the attack can destroy both enemies and tree stumps, even though the tutorial only explains the enemies. I liked the idea of players discovering that later.
Afterwards, I added sound. I found an asset package by Leohpaz with sounds that matched the feeling I wanted. Some sounds technically did not match their original purpose, for example I used an “open menu” sound for jumping, but it worked well in my opinion. I created an AudioManager script and called the sounds from the relevant actions. Later, I added background music, Cat In A Box from NekoLegend’s assets, because it gave me Midnight Munchies vibes.
Lastly, I changed the controls so the game could be played on the arcade machine, such as:

| Action | PC | Arcade |
|---|---|---|
| Navigate through menu buttons | Arrow up/down/left/right | Joystick |
| Select a button | Enter | Button 0 |
| Open pause menu | Escape | Button 3 |
| Close pause menu | Escape | Button 3 |
| Jump | Space | Button 0 |
| Attack | F | Button 1 |
| Close tutorial | Arrow up + Enter / Escape | Button 3 |