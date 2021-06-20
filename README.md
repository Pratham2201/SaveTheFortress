# Save The Fortress
Tower Defense Game

Aim –  

The aim of this project is to design a tower defense game of genre with a blend of endless runner. The game will be built on unreal engine with the assets library from unreal marketplace and mixamo imported character and meshes.

Abstract –  

The game will be in Tower Defense genre. Tower defense (TD) is a subgenre of strategy games where the goal is to defend a player's territories or possessions by obstructing the enemy attackers or by stopping enemies from reaching the exits, usually achieved by placing defensive structures on or along their path of attack. This typically means building a variety of different structures that serve to automatically block, impede, attack or destroy enemies. Tower defense is seen as a subgenre of real-time strategy video games, due to its real-time origins. It will also contain endless wave of enemies spawning from a portal. The number of waves faced will be the score of an individual. Strategic choice and positioning of defensive elements is an essential strategy of the genre.

Introduction –  

The game is about a defense system of kingdom preventing the invaders of from kingdom to enter the gates of fortress. The player commands the defense system by setting it up across the kingdom such that is destroys the enemy waves before the enemies breach the gate of fortress. Once the enemies reach the gates of fortress, the will reach for gold and take the amount of it possible according to the rank of enemy soldier. The players goal is to prevent enemies from looting the entire kingdom treasury for as many as waves as possible. The number of enemy waves face will determine the score achieved by the player. <br>
The player is provided with blueprint of various defense artilleries in the kingdom and player can built those in the provided spots across the kingdom map. Each type of defense artillery has different ability. These artilleries can be placed near each other to see the combined effect. The towers that are built require some resources whose cost will be deducted from the treasury. You can even sell the towers once their use is fulfilled. These towers’ different attributes like damage, range and speed of fire can be upgraded. You can view each tower’s details like their attributes, update status and sell value by clicking on them. The enemy comes in waves which are set at an interval of 40 seconds. In case, the wave is defeated early, the timer can be reset to 0 for next wave. The enemies arrive through a portal near the kingdom and moves towards the gates of fortress in the specified path. There are different tiers of enemies based on their strengths. Killing an enemy gives reward based on the tier or rank of enemy. The enemy health gets upgraded every time a wave is defeated.<br>
The game is provided a fantasy theme to display an era of olden times. The player gets to experience the different arrival of enemy waves by trumpet sound just like it was during wars.<br>

Asset used in Game –  

•	Starter Content –> In-built in the engine – Can be added by option.<br>
•	Mixamo Characters and Animation -> https://www.mixamo.com/#/?page=1&type=Character<br>
•	Anim Starter Pack ->  https://www.unrealengine.com/marketplace/en-US/product/animation-starter-pack<br>
•	Infinity Blade Medieval Dungeon -> https://www.unrealengine.com/marketplace/en-US/assets?count=20&keywords=infinity%20blade&sortBy=relevancy&sortDir=DESC&start=0<br>
•	Infinity Balde Effects ->  https://www.unrealengine.com/marketplace/en-US/product/infinity-blade-effects#:~:text=v%3DVMbPHuU1KRs-,Infinity%20Blade%3A%20Effects%20includes%20visual%20effects%20ranging%20from%20fire%20and,Unreal%20Engine%20community%20for%20free!

Design Procedure ->  

The design in divided into following major classes –  

Fort_Player Controller –   

A PlayerController is the interface between the Pawn and the human player controlling it. The PlayerController essentially represents the human player's will. All the controls go through PlayerController. Fort_PlayerController is the child class of PlayerController that will be used in this game by default.<br><br>
Fort_PlayerController contains following functionality and variables -<br>
•	money available for the player<br>
•	Boolean for checking Placement Mode status.<br>
•	The reference of placeable actor while Placement Mode is enabled<br>
•	Actor type for which placeable actor will be spawned<br>
•	Current Tower clicked<br>
•	High score Saved Value slot<br>
•	Reference for Spawn Point of enemies<br><br>
Functions –<br>
•	SetPlacementModeEnabled – To enable placement mode when clicked on icon from the HUD.<br>
•	UpdatePlacement –To update the location of placeable actor when in placement mode by using line trace.<br>
•	SpawnBuilding – To spawn building on click in the level while in placement mode.<br>
•	SetupSpawnTower – To setup the transform of placed tower when click on placement grid.

Fort_CameraControl –  

The Pawn class is the base class of all Actors that can be controlled by players or AI. A Pawn is the physical representation of a player or AI entity within the world.  Fort_CameraControl is the child class of Pawn which will be used in this project.<br><br>
The Fort_CamerControl Contains following functionality and variables –<br>
•	Camera forward, backward, right and left movement keys<br>
•	Camera rotation at current position along X axis and also along Y axis<br>
•	Camera zoom in and zoom out keys<br>
•	Minimum and maximum angle constraint while rotating along X and Y<br>
•	Refersh Key – Right Click<br><br>
Functions –<br>
•	UpdateMovementSpeed – To move on keys pressed using every tick second and multiplying by speed to get distance offset.<br>
•	CameraPitchChange – To change the zoom settings on keys pressed by increasing the spring arm length<br>

Click (Component) –  

To store the mesh i.e. tower on click in the ‘Static Mesh’ array. This component helps in changing the material when on clicked and on hover.
There is also a similar component for the placement tiles.

Placeable (Component) –  

To update the material of the tower when in placement mode. The tower is shown in red color when in ‘Not Valid’ spot and in green color when in ‘Valid’ spot while in placement mode.

Fort_Game Mode –  

Even the most open-ended game has an underpinning of rules, and these rules make up a Game Mode. 
It contains all the standard classes that are required will be used by the game like default Pawn, HUD class, playercontroller class, GameBaseState class and spectator class.

Enemy –  

The enemy is the class for the enemies spawned through the portal i.e. spawn point.<br><br> The enemy class contains the following functionality and attributes -<br>
•	the direction in which the enemy is moving and facing. Therefore, the offset will be added in that direction.<br>
•	The speed of moving i.e. adding offset when enemy is alive<br>
•	The health of enemy<br>
•	The reward the player will get on killing the enemy<br>
•	The original speed of enemy to restore from when the speed is slowed down by the ice tower.<br><br>
Function -<br>
•	The Hit effect of bullet.<br>
•	Regular Enemy, Boss Enemy and Fast Enemy are child class of the Enemy.<br>

Defense Tower –  

It is a parent class for other tower classes similar to enemy class. It cannot be spawned as it is marked abstract. This class is functionality is used by the children when they are spawned by the player using HUD.<br><br> The DefenseTower class contains the following attributes and functionality –<br>
•	Damage caused by bullet<br>
•	List of enemies overlapped the collision sphere<br>
•	The tower type enum<br>
•	Cost of building the tower<br>
•	Speed of the bullet spawned<br>
•	Range for the detection of the enemies<br>
•	The HUD picture for the tower<br>
•	The material for the mesh of the tower<br>
•	Upgrade Damage, Speed and Range cost<br>
•	Boolean to check Upgrade Damage, Speed and Range is done or not<br>
•	Description of the tower<br><br>
Functionality –<br>
•	AttackEnemy – To spawn bullet and assign the speed, damage and enemy to the bullet<br><br>
Basic Tower, Ice Tower, Fire Tower and Wealth tower are the child classes for DefenseTower with different attributes.

Bullet –<br><br>
This class contains the property of the bullets. The class is design to create a bullet mesh with attributes attached to it so that it can define itself in the world when spawned.<br><br> The Bullet class contains the following attributes and functionality –<br>
•	Speed of the bullet<br>
•	Damage of the bullet<br>
•	Last location the enemy it was following in case the enemy dies before getting hit by the current bullet.<br>
•	Material of the bullet which will be similar to the material of the tower from which it was spawned.<br>
•	It also contains the enemy it is currently overlapping before getting destroyed. This helps to trigger the particle effect in the enemy that was hit.<br><br>
Functionality –<br>
•	PlayImpactAnim – This function will play the particle effect or hit effect when the bullet collides with the enemy. The animation presented will depend on the material of the bullet.

Spawn Point – <br><br>
Spawn point class contains the portal through which the enemies are spawned in the level. There will only be a single instance present in the level of this class.<br><br> The Spawn point class contains the following attributes and functionality –<br>
•	It contains the a wave array to store the number of enemies spawned in each wave<br>
•	Contains the wave current wave number<br>
•	Contains a Boolean to check where the enemy can be spawned or not<br>
•	Stores the number of spawned enemies in a single wave<br>
•	Stores the class of which the enemy will be spawned in the wave<br>
•	Store the time gap between two consecutive wave<br>
•	Stores the timer till the next wave to come<br>
•	Stores the Health increase factor by which the health will be increased after a wave completes.

Placement Tile –<br><br>
It is a small class that contains tower the mesh for the placement tile along with the Onclick component. It also has a boolean variable to know the status whether the placement tile is empty or not.

HUD class and Widget –<br><br>
This class Is responsible for storing the HUD widgets like the buttons to spawn the towers, current amount of money, number of waves faced, timer till the next wave. The widget class contains all the layout and the functionality of OnClick Events while the HUD class links the Widget class to the viewport.

How To Play ?<br><br>
•	Move the camera across the kingdom to look for various tower placing spots and incoming enemy wave. Rotate the camera to view the kingdom from different angle horizontally or vertically. Also, zoom in and zoom out your camera to get a closer look or to view the entire kingdom from a far angle.<br>
•	The player has to select a tower from a various types of towers present in HUD and place it in on one of the hexagonal tiles available i.e. which is not occupied.<br>
•	The tower can be built from the blueprint if there is enough money present in the treasury to endure the cost. If money is less than the cost of tower, error will be displayed on the screen. Build tower across the kingdom according to your strategy and earn rewards on defeating the enemy. The rewards goes into treasury.<br>
•	Click on specific tower to view its specification and its features.<br>
•	Upgrade your tower by selecting the tower you want to upgrade and clicking on desired attribute to be upgraded like damage caused, speed of fire and range of tower.<br>
•	Sell the specific tower by selecting it and clicking on sell button.<br>
•	Reset the enemy wave timer by clicking the ‘Reset Timer Key’.

Screen Snapshots of the game-
1.	It is the first level of the game or we can say the default level which is opened when the game is executed. It consists of two buttons-
a.	New Game – This button leads to next level which is our game.
b.	Exit – Click on this button exits the game.
![Screenshot_1](https://user-images.githubusercontent.com/55658008/122665536-6ea4f900-d1c5-11eb-9c77-1b30d16a6768.png)

2.	This is the main level of the game. The player starts to setup the defense system of the game with the initial money provided. If the player completes the defense setup before the timer runs out, the player can skip the timer by pressing ‘G’ key.
 ![Screenshot_2](https://user-images.githubusercontent.com/55658008/122665576-a90e9600-d1c5-11eb-8b71-f6306828b942.png)

3.	The player upgrades the tower by clicking on the specific upgrading attribute of that tower. The upgrade will reduce the cost of upgrading from the treasury
![Screenshot_3](https://user-images.githubusercontent.com/55658008/122665598-c2174700-d1c5-11eb-9db4-a92d39e6b1cf.png)
 
4.	This is the same level with the same HUD. When the enemies enter the gates of Fortress and empty the treasury, the game is over. This pauses the game displays your current score (which is the ‘Waves Faced’) along with the High score.
 ![Screenshot_4](https://user-images.githubusercontent.com/55658008/122665603-cc394580-d1c5-11eb-8000-ab4e9a02f0f6.png)


Key Controls –
Camera Movements –  

	W – Move Forward
	S – Move Backward
	D – Move Right
	A – Move Left
	Q – Rotate Camera leftwards
	E – Rotate Camera Rightwards
	R – Rotate Camera Upwards
	F – Rotate Camera Downwards
	Thumb Mouse Button 1 – Zoom Out
	Thumb Mouse Button 2 – Zoom In
	Left Click – Place Towers/Select Specific Tower/Upgrade or Sell Tower
	Right Click – Exit Placement Mode
	G – Reset Timer

Starting and Winning Position –<br><br>
Staring Position – Initial kingdom with no tower placed and 40 seconds until 
                              arrival of first wave<br>
Winning Position – When Treasury is empty and an enemy enters the gate of 
                                Fortress.

Conclusion –<br><br>
‘Save The Fortress’ is built using unreal engine using blueprint scripting. The game provides a suitable experience a fantasy themed war era. The game delivers a full experience of a standard war based, fantasy themed and strategy based game. The high score will be saved in the local memory which provide remote access to data anytime. The saved file will load the high score on that system every time. The game contains various assets for different kinds of enemies, defense towers, explosion and hit effects. At last, the game is a single player strategy game made using visual scripts.

Feature Work – <br><br>
The game contains many future development and improvement possibility. To start with graphics and animation, The overall layout of the game can be improved by adding various meshes to enhance the level map. The lightning can be improved to cast the shadows of flames and enemies on the ground and other objects. Most importantly, an upgrade in a tower can be shown by the change in the tower mesh showing the improved attribute. A cannon can be added to top of tower instead of the sphere which will also be upgradable. 
The canon will trace the enemy movement fire in the same way. The bullets can be provided with particle effects as well as a specified trajectory. The trajectory will be dependent on the type of artillery Ex – a mortar will fire upwards which will fall in enemies’ way and provide splash damage. <br>
On enemies’ side, the enemy can slowly grow their body parts showing increase in health. The ways can be upgraded with a new number a number of new enemy meshes with different attributes. The wave structure can be improved to allow a mixture of different level of enemies to enter in a single wave. Further, the score can pattern could be changed from high score like to mission. The player will be provided with a story and the number of defense levels can be increased.

References –<br><br>
•	https://www.reddit.com/r/gamedev/comments/b8vdre/starting_to_build_a_tower_defense_game_in_unreal/<br>
•	https://docs.unrealengine.com/4.26/enUS/Resources/SampleGames/StrategyGame/<br>
•	https://www.youtube.com/watch?v=ZrM_CfOy1sU&list=PLFYGCCDpMHmHJwhIRY6qNumAts--W8bTy&index=4&t=1352s<br>
•	https://www.youtube.com/watch?v=9f98-D9T0Nk&list=PLFYGCCDpMHmHJwhIRY6qNumAts--W8bTy&index=8<br>

