# Collect and Avoid

Game where player moves around an arena, collects items for points, avoids an enemy that patrols and chases, and wins or loses.

## How to run the packaged build

## Version

Unreal Engine 5.8.4

## Settings

Everything done on "Epic" Viewport scalability group.

## Controls
W -- Movement Forward\
A -- Movement Left\
S -- Movement Backward\
D -- Movement Right\
Left Shift -- Sprint\
Space -- Jump. You can also press space 2 times to double jump
Escape -- To pause the game.

## How Git is used

For storing .uasset and .umap the Git LFS is used.

## Useful abbreviations in names of objects

L\_ = Level  
BP\_ = Blueprint  
M\_ = Material  
T\_ = Texture  
SM\_ = Static Model  
SK\_ = Skeleton Model  
IA\_ = Input Action  
IMC\_ = Input Mapping Context

## The structure of the folders is the following

Content/CollectAndAvoid  
From CollectAndAvoid there are folders Blueprints (there is Widgets folder as well), Materials, Meshes, Maps, UI, Input_Action, Sounds, Enumeration, Images

## Blueprints, their description and their functions

(Added during Part 1)
BP_Hero. The main character that can move, jump, has camera that follows him. During completion of task, has sprint logic implemented and add input mapping implemented. Also it's class that has pause logic for WBP_Pause widget.\
BP_Gamemode. The place that controls what Controller class to use (in this case it's BP_ThirdPersonPlayerController, free asset from Unreal Engine), default pawn class (In our case it's BP_Hero). Basically it's where rules are being set\
Has function to AddScore (that adds score and check whether score is equal to target score and if that's the case, prints string that I won and makes enumeration equal to "Won"). Has variables Score and TargetScore, Game_State_Enumeration.

(Added during Part 2)
BP_Coin. Has sphere collision component and static mesh. It has only collection logic implemented, where you check whether BP_Hero collided with sphere collision component, then it would add points (by BP_GameMode AddScore function) and destroy the coin.

(Added during Part 3)
BP_Enemy. Checks collision (I added separately sphere collision component named LoseRadius because I had problems with checking overlapping of two characters) with BP_Hero and in that case makes game state to "Lost". Also exposed max walk speed variable to be editable. It's also the blueprint of AI, that has AI Controller class BP_EnemyAIController
BP_EnemyAIController. Starts blackboard and runs behaviour tree, has implementation of logic when Enemy sees player. Mainly it's blueprint for setting Blackboard values so that Enemy could understand in behaviour tree when to chase player or patrol between 3 points.


(Added during doing something from Part 4)
WBP_HUD. It's what gets shown in the screen, in this case Target Score, Score (that is being updated by binding to event dispatcher of gamemode), Image of coin, Controls hint.\
WBP_Main_Menu. Widget that shows Main Menu (Play, Settings, Quit). It doesn't work right now, but in case I want to do additional widget, I would make it work.\
WBP_Pause. Widget that shows only text "Paused" and disables/enables if you press "Escape" button. The logic of pressing buttons is implemented there as well. \
WBP_Win. Shows text "You won" and Restart button. The logic of Restart button is implemented in the blueprint.\ 
WBP_Lose. Shows text "You lost" and Restart button. The logic of Restart button is implemented in the blueprint.

# Part 1. Level blockout and player movement

This part is describing mainly what each change of max walk speed/jump velocity/air control does.

## Changing movement parameters

Changed Max Walk Speed from 600,0 cm/s to 450,0 cm/s. Changing Max Walk Speed changes maximum speed that character can achieve.\
Changed Jump Z Velocity from 500,0 cm/s to 350,0 cm/s. Changing Jump Z Velocity changes maximum height of the jump.\
Changed Air Control from 0,35 to 1,0. Changing Air Control changes ability to move freely in the air. 0,0 means that if you jump, you basically can't move in any direction other than up and down. 1,0 makes you being able to move freely in jump. Basically, from what I understood, Air Control gives us control to move in the air in any direction.

## Adjusting the camera

Wanted to mention that spring arm length (400,0 cm) and default camera offset (everything at zero) already makes player see the arena well and doesn't make camera clip through walls.

## Double jump

I implemented double jump, but I'm not sure whether it's right to just change Jump Max Count on character from 1 to 2 rather than creating blueprints. Of course, the Jump Max Hold Time is 0, so that we can't levitate in the air.
Additionally, as the task didn't state, I didn't do animation in case of double jump.

# Part 2. Collectibles and score.

This part mainly answers the question why the cast check is needed.

## Why cast check is needed
From what I understood, the cast check in this case is needed in order for Sphere collision component to understand that it collided with BP_Hero. Also it's needed to access variables and functions of BP_Hero.

# Part 3. Enemy: patrol
Nothing to answer here. Probably one of the most difficult parts of my work to do after figuring out event dispatcher.

# Part 4. Interface, audio and polish
This part mainly answers the question why I should be updating the score through functions or event and not per-frame binding. 

The reason why we need to update through functions or event it's because if we just update the score text for example through Details and bind it, It will happen basically every frame, no matter if score changed or not changed. That's why we should use events for example that is being called only when coin gets picked up, and only then we update the text. Basically I understood that it's just better in terms of performance.

# Part 5. Profiling, packaging and report

## Asset list with sources and licenses
Coin_pickup_sound was made by me\
Background_loop music was made by me\
Coin_image was made by me.\
Enemy_started_chase was made by me.

## Known bugs
During part 1 there were no bugs.\
During part 2 there were no bugs.\

During part 3 I couldn't understand whether it's better to just duplicate BP_ThirdPersonCharacter and make the BP_Enemy this way. Even though it's required to make pawn BP_Enemy, I don't know how to manually insert stuff applicable to the Enemy as character, so I duplicated BP_ThirdPersonCharacter.\
Also I couldn't figure out how to expose sight radius as it's hidden very very deep in ai sight config.

# What I learned and what was hard
I think I learnt a bit more about git, what folders i should include in .gitignore and actually I'm sort of proud that i made my first ever push commit into github. The hardest part is to have desire to continue even when you already see deadline coming and you have not a lot accomplished. So far, thanks to lecture about Unreal, I made my first Gamemode (it's still confusing to me what is it and their components though), sprint logic and double jump. I understand that maybe I did the base minimum, I tried a lot to understand stuff through documentation, sometime I looked at videos to understand some part of the lecture. So far right now I have finished part 1, and maybe the difficulty was to make obstacles be on the ground, set rules in gamemode, enhanced input is still a bit confusing to me, but changing movement parameters and adding double jump felt fun and easy in part 1.\
While I was completing task 2, I understood that it's hard for me to understand what enhanced input is. I tried to make the code according to the lecture about adding map input, yet it's hard for me to understand what its purpose, especially when without it, the project seem to work fine.

While working with Part 2, I learned how to make spinning and collectible coin, how to make it add points and disappear when BP_Hero collides with it, also how to make game state enumeration. It was hard for me to understand event dispatcher, probably cast to something. Especially event dispatcher, because I spent I think way too much time understanding how to make it work and how to make it basically.

While working with Part 3, I learned how to place NavMeshBoundVolume so that enemy can understand where to go, how to make enemy and how to make blackboard and behaviour tree. The most difficult was to do behaviour tree as I couldn't really find detailed explanations about it in lecture. Though I made it work. The main problems why I had issue with this part is because I forgot to add blackboard and run behaviour tree on beginplay for example, or I was lazy to check with print string what worked or not. Also I had problems with navmesh and thought I did map wrong but it turned out i just needed to make navmesh to my entire floor and room. It was hard part basically of my work.

While working with Part 4, I learned how to make widgets, especially how to update score by using event dispatcher (it was also the difficult part).




