Since I worked alone, I was responsible for the full implementation of the game. This included the endless runner mechanics, player movement, spawning systems, pickups, enemies, UI, audio, and the final arcade controls. Instead of listing every small object I added, this reflection focuses on the main systems I implemented and the technical decisions behind them.
One of the first things I implemented was the endless runner loop. Instead of moving the player constantly forward, I kept the player mostly in place and moved the world to the left. This made the camera simpler and worked well for the arcade format.
The GroundMovement script moves ground pieces left at a fixed speed. When a ground piece reaches a certain X position, the GroundSpawner moves it back to the front. This creates the illusion of infinite ground:
 if (transform.position.x < -23f) 
        {
            ScoreManager.instance.AddScore(10);
            transform.position = new Vector3(23f, transform.position.y, 0f);
        }
The value “23” comes from the approximate length of the ground section in tiles. It was just a number I chose after testing what felt long enough.
For the player, I implemented a ground check using Raycast. The raycast checks whether the player is touching the ground (via the Layer), and the jump counter makes sure the player can only jump twice before landing again. Because of this some bushes and the platforms also have the layer “Ground” so that, when the player lands there, their jumps reset.
isGrounded = Physics2D.Raycast(transform.position, Vector2.down, rayLength, groundLayer);
A major part of my implementation was the spawning. At first, obstacles, platforms, pickups, and enemies had separate spawner scripts. Later, I combined them into a single SpawnManager.
The biggest technical challenge was an overlapping spawn bug. I first thought the issue was caused by the spawn logic, so I tried everything. Eventually, I discovered that the problem was inside the prefabs: some sprites were child objects with different local X. This meant the prefab root was spawning in the correct place, but the sprite itself appeared shifted.
This taught me that debugging in Unity is checking even what you think “oh, no, I am sure thats fine”.
I also implemented the chocolate system. The ChocolateManager controls the chocolate percentage, increases it when pickups are collected, drains it over time, and checks whether the value is above 50%. The ChocolateBarUI script reads this value and updates the visual bar on screen.
Later, I connected this to the attack system. The PlayerAttack checks with the ChocolateManager whether the player has enough chocolate to attack. If they do, it spawns a chocolate ball and subtracts the attack cost. The ChocoAttack script controls the ball movement, lifetime, and collision behaviour.
Another important contribution was the UI and arcade input. The game includes a main menu, tutorial, pause menu, game over screen, chocolate bar, and score display. Since the game had to run on the arcade, the UI could not depend on mouse clicks.

To solve this, I changed the menus to use selected buttons. The player can move between buttons using arrow keys on PC or the joystick on the arcade machine, and select options using the green button. I also mapped gameplay actions to arcade buttons, such that:
| Action | PC | Arcade | Arcade Player |
|---|---|---|---|
| Navigate through menu buttons | Arrow up/down/left/right | Joystick | Joystick |
| Select a button | Enter | Button 0 | Green Button |
| Open pause menu | Escape | Button 3 | Yellow Button |
| Close pause menu | Escape | Button 3 | Yellow Button |
| Jump | Space | Button 0 | Green Button |
| Attack | F | Button 1 | Red Button |
| Close tutorial | Arrow up + Enter / Escape | Button 3 | Yellow Button |

Lastly, I added an AudioManager that plays sound effects for actions such as jumping, attacking, and game events. I also added background music and visual UI assets to make the game feel more complete. These parts were not the most technically difficult, but they made a big difference to how finished the game felt.
If I had more time, I would improve the difficulty progression by making the game speed up over time, add a leaderboard for the score, and polish the tutorial so the controls are clearer. I would also make the input handling more robust, because during arcade testing I noticed that pressing several buttons at once can sometimes cause small bugs.
