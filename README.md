# Collect and Avoid

Game where player moves around an arena, collects items for points, avoids an enemy that patrols and chases, and wins or loses.

## How to run the packaged build

## Version

Unreal Engine 5.8.4

## Settings

Everything done on "Epic" Viewport scalability group.

## Controls
W -- Movement Forward
A -- Movement Left
S -- Movement Backward
D -- Movement Right
Left Shift -- Sprint
Space -- Jump. You can also press space 2 times to double jump

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
IMC\_ = Input Mapping Context\

## The structure of the folders is the following

Content/CollectAndAvoid  
From CollectAndAvoid there are folders Blueprints, Materials, Meshes, Maps, UI, Input_Action.

## Blueprints, their description and their functions
BP_Hero. The main character that can move, jump, has camera that follows him. During completion of task, has sprint logic implemented and add input mapping implemented.
BP_Gamemode. The place that controls what Controller class to use (in this case it's BP_ThirdPersonPlayerController, free asset from Unreal Engine), default pawn class (In our case it's BP_Hero).
Basically it's where rules are being set


# Part 1. Level blockout and player movement

This part is describing mainly what each change of max walk speed/jump velocity/air control does.

## Changing movement parameters

Changed Max Walk Speed from 600,0 cm/s to 450,0 cm/s. Changing Max Walk Speed changes maximum speed that character can achieve.
Changed Jump Z Velocity from 500,0 cm/s to 350,0 cm/s. Changing Jump Z Velocity changes maximum height of the jump.
Changed Air Control from 0,35 to 1,0. Changing Air Control changes ability to move freely in the air. 0,0 means that if you jump, you basically can't move in any direction other than up and down. 1,0 makes you being able to move freely in jump. Basically, from what I understood, Air Control gives us control to move in the air in any direction.

## Adjusting the camera

Wanted to mention that spring arm length (400,0 cm) and default camera offset (everything at zero) already makes player see the arena well and doesn't make camera clip through walls.

## Double jump

I implemented double jump, but I'm not sure whether it's right to just change Jump Max Count on character from 1 to 2 rather than creating blueprints. Of course, the Jump Max Hold Time is 0, so that we can't levitate in the air.
Additionally, as the task didn't state, I didn't do animation in case of double jump.

# Part 2. Collectibles and score.

This part answers the question why the cast check is needed.

## Why cast check is needed

# Part 3. Enemy: patrol

# Part 4. Interface, audio and polish

# Part 5. Profiling, packaging and report

## Asset list with sources and licenses

## Known bugs
During part 1 there were no bugs.
# What I learned and what was hard

