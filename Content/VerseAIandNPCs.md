AI and NPCs
Learn how to use NPCs and create custom AI logic and behaviors for your islands!

AI and NPCs
In this section, you'll find everything you need to know about using artificial intelligence (AI) and non-playable characters (NPCs) on your island. This allows you to add a variety of gameplay and facilitate interesting interactions between the player and creatures and characters!

To understand how creating NPCs and AI behaviors work in UEFN, check out:

Understanding NPC Behaviors

NPC Types

One way to quickly set up and add custom behavior to an NPC is with the NPC Spawner Device. In this section, you’ll find all the information you need:

NPC Spawner Device

NPC Character Definition

Using the NPC Spawner with Animations

Create Custom NPC Behavior page

Want to see these concepts and devices in action? Check out our tutorials:

Create Your Own NPC Medic

Stronghold Template
Stronghold Template

Use Verse to create a stealth game where players must eliminate guards.

Understanding NPC Behaviors
Understanding NPC Behaviors

Learn about NPC Behavior and States and how NPCs use them for decision-making

NPC Spawner Devices
NPC Spawner Devices

Use NPCs to engage with players and liven your gameplay.

NPC Character Definitions
NPC Character Definitions

Create Character Definitions to add attributes that can be imported into the NPC Spawner device.

Using the NPC Spawner with Animations
Using the NPC Spawner with Animations

Use custom animations and emotes with the NPC Spawner device and Verse code.

Create Custom NPC Behavior
Create Custom NPC Behavior

Use Verse code to create your own NPC behavior unique to your game design needs!

NPC Types
NPC Types

Learn about the different types of NPCs and how each of them works.

Stronghold Template
Use Verse to create a stealth game where players must eliminate guards.

Stronghold Template
In this game, players can choose their play style by either sneaking through or fighting their way through a stronghold. This stronghold is guarded by an AI that patrols designated areas.

The gameplay supports either solo or a squad of four players.


You can find Verse Stronghold template in the Feature Examples section of the Project Browser.

Enter the island code 2218-1545-9149 to play and see the Verse Stronghold template’s mechanics in action.

This tutorial serves as a walkthrough that highlights and explains important mechanics used to create the Verse Stronghold template. It will also show you how to add audio and visual effects like barks and alarm lights.

Verse Language Features Used
Arrays

Events

Agents

Characters

Steps
Follow these steps to learn how to use Verse with devices to create a multiplayer stealth game with AI guards that can patrol designated areas.

1. Create a New Project
1. Create a New Project

Learn how to create a new project and modify the island settings.

2. Add Devices
2. Add Devices

Add and configure the devices that drive Stronghold.

3. Add Verse Script to Devices
3. Add Verse Script to Devices

Learn how to set up the Verse device to customize gameplay.

4. Set Up Leash Devices
4. Set Up Leash Devices

Learn how to set up leash devices for AI to patrol.

5. Set Up Audio and Visual Effects
5. Set Up Audio and Visual Effects

Learn how to set up audio and visual effects to enhance gameplay.

Array
An array is a container where you can store elements of the same type, and access the elements by their position in the array.

Array
When you have variables of the same type, you can collect them into an array. An array is a container type where you specify the type of the elements with []type, such as []float. An array is useful because it scales to however many elements you store in it without changing your code for accessing the elements.

For example, if you have multiple players in your game, you can create an array and initialize it with all the players.

Verse
Players : []player = array{Player1, Player2}
Players : []player = array{Player1, Player2}
An array containing 2 players
Verse has the pattern where definition mirrors use. Defining an array and using it follows that pattern.

Array Length
You can get the number of elements in an array by accessing the member Length on the array. For example, array{10, 20, 30}.Length returns 3.

Accessing Elements in an Array
Elements in an array are ordered in the same position in the array as you inserted them, and you can access the element at that position, called its index, in the array. For example, to get the first player, you’d access the Players array with Players[0].

The first element in an array has an index of 0 and each subsequent element’s index increases in number. For example, array{10, 20, 30}[0] is 10 and array{10, 20, 30}[1] is 20.

Index

0

1

2

Element

10

20

30

The last index in an array is one less than the length of the array. For example, array{10, 20, 30}.Length is 3 and the index for 30 in array{10, 20, 30} is 2.

Accessing an element in an array is a failable expression and can only be used in a failure context, such as an if expression. For example:

Verse
ExampleArray : []int = array{10, 20, 30, 40, 50}
for (Index := 0..ExampleArray.Length - 1):
    if (Element := ExampleArray[Index]):
        Print("{Element} in ExampleArray at index {Index}")
ExampleArray : []int = array{10, 20, 30, 40, 50} for (Index := 0..ExampleArray.Length - 1): if (Element := ExampleArray[Index]): Print(&quot;{Element} in ExampleArray at index {Index}&quot;)
This code will print:

Verse
10 in ExampleArray at index 0
    20 in ExampleArray at index 1
    30 in ExampleArray at index 2
    40 in ExampleArray at index 3
    50 in ExampleArray at index 4
10 in ExampleArray at index 0 20 in ExampleArray at index 1 30 in ExampleArray at index 2 40 in ExampleArray at index 3 50 in ExampleArray at index 4
Changing an Array and its Elements
Arrays, like all other values in Verse, are immutable. If you define an array variable, that allows you to assign a new array to the variable, or mutate individual elements.

For example:

Verse
# Array1 is an array of integers
Array1 : []int = array{10, 11, 12}

# Array2 is an array variable of integers
var Array2 : []int = array{20, 21, 22}

# we concatenate Array1, Array2, and a new array of integers
# and assign that to the Array2 variable
set Array2 = Array1 + Array2 + array{30, 31}

This code will print:

Verse
10 at index 0
    77 at index 1
    12 at index 2
    20 at index 3
    21 at index 4
    22 at index 5
    30 at index 6
    31 at index 7
10 at index 0 77 at index 1 12 at index 2 20 at index 3 21 at index 4 22 at index 5 30 at index 6 31 at index 7
Multi-Dimensional Arrays
The arrays in the previous examples were all one-dimensional, but you can also create multi-dimensional arrays. Multi-dimensional arrays have another array, or arrays, stored at each index, similar to columns and rows in a table.

For example, the following code produces a two-dimensional (2D) array, visualized in the following table:

Verse
var Counter : int = 0
Example : [][]int =
    for (Row := 0..3):
        for(Column := 0..2):
            set Counter += 1
var Counter : int = 0 Example : [][]int = for (Row := 0..3): for(Column := 0..2): set Counter += 1
 	Column 0	Column 1	Column 2
Row 0

1

2

3

Row 1

4

5

6

Row 2

7

8

9

Row 3

10

11

12

To access elements in a 2D array, you must use two indices. For example, Example[0][0] is 1, Example[0][1] is 2, and Example[1][0] is 4.

The following code shows how to use a for expression to iterate through the Example 2D array.

Verse
if (NumberOfColumns : int = Example[0].Length):
    for(Row := 0..Example.Length-1, Column := 0..NumberOfColumns):
         if (Element := Example[Row][Column]):
             Print("{Element} at index [{Row}][{Column}]")
if (NumberOfColumns : int = Example[0].Length): for(Row := 0..Example.Length-1, Column := 0..NumberOfColumns): if (Element := Example[Row][Column]): Print(&quot;{Element} at index [{Row}][{Column}]&quot;)
This code will print:

Verse
1 at index [0][0]
    2 at index [0][1]
    3 at index [0][2]
    4 at index [1][0]
    5 at index [1][1]
    6 at index [1][2]
    7 at index [2][0]
    8 at index [2][1]
    9 at index [2][2]
    10 at index [3][0]
The number of columns in each row is not required to be constant.

For example, the following code produces a two-dimensional (2D) array, visualized in the following table, where the number of columns in each row is greater than the previous row:

Verse
Example : [][]int =
    for (Row := 0..3):
        for(Column := 0..Row):
            Row * Column
Example : [][]int = for (Row := 0..3): for(Column := 0..Row): Row * Column
 	Column 0	Column 1	Column 2	Column 3
Row 0

0

Row 1

0

1

Row 2

0

2

4

Row 3

0

3

6

9

Persistable Type
An array is persistable if the type of elements in the array are persistable, which means that you can use them in your module-scoped weak_map variables and have their values persist across game sessions. For more details on persistence in Verse, check out Using Persistable Data in Verse.

event
Events are things that trigger functions. Functions are things that devices do.  Compare to function.

With direct event binding, you tell a device to communicate directly with another device by binding their functions and events together. When a device activates, or a player performs an action, that's an example of an event. Events trigger other devices to do a particular thing or set a particular condition, and that action or condition is a function.  

This is how you use devices to create gameplay.

In Verse, an event is an action or occurrence that can be identified. For example, the Button device has the InteractedWithEvent, which occurs whenever a player interacts with the button. You can define behavior for whenever a specific event occurs by subscribing with an event handler.  

agent
An agent can represent either a player or an AI.  

player
A type in Verse that represents a human player. Compare to agent.

character
In UEFN, a character is a type of Pawn that includes the ability to walk around. A character is a subclass of a Pawn Actor that is intended to be used as a player character. The character subclass includes a collision setup, input bindings for bipedal movement, and additional code for movement controlled by the player.

In Verse, a character can also refer to a single typographical element in a string.

1. Create a New Project
Learn how to create a new project and modify the island settings.

1. Create a New Project
This section will show you how to create a new project and start creating the gameplay.

Open UEFN and create a new empty project.

Select the IslandSettings device in the Outliner and locate User Options - Game Rules.

Island Settings
Modify the User Options as shown below.

Use the Search bar to locate each setting faster.

Option	Value	Explanation
Max Players

4

There will be a maximum of four players.

Teams

Cooperative

This will be a cooperative game.

Team Size

4

The team size will be four.

Spawn Pad Selection

Near Teammates

Players will spawn near each other.

Auto Start

False

The game will wait to start until manually activated.

Game Start Countdown

3

The game will start after three seconds.

Harvest Style

Creative

The Creative values are used for resource gathering during the game.

Allow Building

None

Players will not be allowed to build during the game.

Environment Damage

Off

Players will not be allowed to destroy the environment.

Structure Damage

None

Players will not be allowed to destroy structures.

Respawn Time

5.0

Players will respawn after five seconds.

Jump Fatigue

True

Continuous jumping will apply a penalty to jump height.

Glider Redeploy

True

Players will be able to freely deploy their gliders without the use of items.

Flight Speed

1.0x

There will be a movement multiplier of 1 when flying.

Game Winner Display Time

3.0

The overall game winner’s name will be shown at the end of the game for 3 seconds.

Game Score Display Time

15.0

The final scoreboard will be shown at the end of the game for 15 seconds.

Round Winner Display Time

3.0

The round winner’s name will be shown at the end of the round for 3 seconds.

Round Score Display Time

15.0

The scoreboard will be shown at the end of the round for 15 seconds.

HUD Info Type

True

AI enemy elimination will be tracked in the HUD.

Map Screen Display

Overview Map

The overview map will display when a player presses the Map key.

Game End Callout

Cooperative

Shows everyone the same end screen and uses the Victory Sound.

Victory Sound

Success 1

Determines what sound to play when players win the game.

Next Section
2. Add Devices
2. Add Devices

Add and configure the devices that drive Stronghold.

2. Add Devices
Add and configure the devices that drive Stronghold.

2. Add Devices
This section will show you how to set up the devices that drive this gameplay.

This tutorial uses the following devices:

4 x Player Spawners

7 x Guard Spawners

1 x Tracker

2 x HUD Messages

1 x Item Granter

3 x End Games

1 x Map Indicator

Player Spawner Device
Player Spawner
Build a stronghold and place four Player Spawner devices. Position these devices 80 meters away from the stronghold to avoid having players detected when starting the game mode.

To set up this device, configure the User Options as follows:

Option	Value	Explanation
Visible in Game

False

This device will not be visible during the game.

Guard Spawner Device
Guard Spawner
Place three Guard Spawners in the stronghold and four guard spawners away from the stronghold to serve as reinforcements. You can change this amount to suit your gameplay.

Two of the stronghold Guard Spawners will be for snipers, and will spawn one AI from each device.

To set up these devices, configure the User Options as follows:

Guard Spawner Settings
Option	Value	Explanation
Spawn Count

1

This device will have one guard spawn at a time.

Item List

Select a Rail Gun

Select Add Element then select a sniper rifle in the Item Definition row.

Index 0

Rail Gun

Select a rail gun in the Item Definition row.

Allow Infinite Spawn

False

Guards from this device will not spawn infinitely.

Team Index

2

Players will be Team 1, which means guards will be hostile toward players when they spot them.

Spawn Timer

1.0

Sets the minimum time between spawning guards.

Spawn Radius

2.5

Sets the maximum distance from the device that a guard can spawn.

Show Health Bar

True

A health bar will be displayed above the guards.

Max Patrol Distance

2.5

Sets the guard’s maximum patrol distance from the spawner.

Visibility Range

70.0

Sets the guard’s maximum sight perception distance when unaware. Hearing is not affected by this.

Drop Inventory on Elimination

False

Guards will not drop their inventory on elimination.

Accuracy

VERY HIGH

Defines how guards are at shooting.

The next stronghold Guard Spawner will be used for assault.

To set up this device, configure the User Options as follows:

Assault Guard Spawner
Option	Value	Explanation
Guard Type

Grotto

Sets the type of guard that will be spawned by this device.

Item List

Select an assault rifle

Select Add Element then select an assault rifle in the Item Definition row.

Index 0

Assault Rifle

Select an assault rifle in the Item Definition row.

Allow Infinite Spawn

False

Guards will not spawn from this device infinitely.

Team Index

2

Players will be Team 1, which means guards will be hostile toward players when they spot them.

Spawn Timer

1.0

Sets the minimum time between spawning guards.

Spawn Radius

18.0

Sets the maximum distance from the device that a guard can spawn.

Show Health Bar

True

A health bar will be displayed above the guards.

Max Patrol Distance

18.0

Sets the guard’s maximum patrol distance from the spawner.

Visibility Range

70.0

Sets the guard’s maximum sight perception distance when unaware. Hearing is not affected by this.

Drop Inventory on Elimination

False

Guards will not drop their inventory on elimination.

Accuracy

HIGH

Defines how guards are at shooting.

The last two Guard Spawners will be placed outside of the stronghold for reinforcements. Place these devices at least 40 meters away from the stronghold.

Reinforcements will only spawn if the initial guards at the stronghold were alerted by the presence of a player.

To set up this device, configure the User Options as follows:

Option	Value	Explanation
Guard Type

Grotto

Sets the type of guard that will be spawned by this device.

Spawn Count

2

Sets the number of guards this spawner can have active at any time.

Item List

Select an assault rifle

Select Add Element then select an assault rifle in the Item Definition row.

Index 0

Ranger Assault Rifle

Select a ranger assault rifle in the Item Definition row.

Allow Infinite Spawn

False

Guards will not spawn infinitely from this device.

Total Spawn Limit

2

Sets the maximum number of guards this spawner can produce during its lifetime.

Team Index

2

Players will be Team 1, which means guards will be hostile toward players when they spot them.

Spawn Radius

5.0

Sets the maximum distance from the device that a guard can spawn.

Show Health Bar

True

A health bar will be displayed above the guards.

Max Patrol Distance

200.0

Sets the guard’s maximum patrol distance from the spawner.

Visibility Range

70.0

Sets the guard’s maximum sight perception distance when unaware. Hearing is not affected by this.

Drop Inventory on Elimination

False

Guards will not drop their inventory on elimination.

Accuracy

HIGH

Defines how guards are at shooting.

Tracker Device
Tracker Device
The Tracker device is used to display the objective and keeps track of the total number of guards to eliminate, which can vary depending on whether reinforcements have spawned.

To set up this device, configure the User Options as follows:

Tracker Settings
Option	Value	Explanation
Stat to Track

Events

Determines which statistic will be used as the Tracker Value.

Target Value

6

Sets the target value at which the Tracker will be considered complete.

Assign on Game Start

False

Determines whether applicable players will be assigned this Tracker when the game starts.

Assign When Joining in Progress

False

Determines whether applicable players will be assigned this Tracker when joining a game currently in progress.

Tracker Title

Eliminate Stronghold Guards

Assigns a title to the Tracker which will be displayed if Show on HUD is switched on.

Description Text

Number of Guards

Assigns a description to the Tracker which will be displayed below the title if Show on HUD is switched on.

Sharing

Team

Determines whether the Tracker progress is counted individually, as a team, or whether everyone contributes to a single Tracker value.

Winning Team

Team Index

Determines which team wins the round when the Tracker is completed.

HUD Message Device
HUD Message
The HUD Message device displays a message to all players when the reinforcements are triggered. This message is triggered via Verse when one of the guards at the stronghold is alerted.

Place two devices, one for fallback and one for reinforcement, and configure the User Options as follows:

Fallback
Fallback Message
Option	Value	Explanation
Message

Guards Retreating to the Stronghold!

Insert the message to be displayed.

Reinforcement
Reinforcement Message
Option	Value	Explanation
Message

Detected! Incoming Reinforcement!

Insert the message to be displayed.

Item Granter Device
Item Granter
Use an Item Granter to offer players a loadout with weapons and items to combat the guards.

To set up this device, configure the User Options as follows:

Item Granter Settings
Option	Value	Explanation
On Grant Action

Keep All

Defines the action to perform when the device grants an item.

Grant

All Items

All items in the device will be granted.

Item List

Select three weapons and a healing item

Select Add Element then select items in the Item Definition row.

Index 0

Auto Shotgun

Select an auto shogun in the Item Definition row.

Index 1

Assault Rifle

Select an assault rifle in the Item Definition row.

Index 2

Suppressed Sniper Rifle

Select a suppressed sniper rifle in the Item Definition row.

Index 3

Bandage

Select a bandage in the Item Definition row.

Map Indicator Device
Map Indicator
Add a Map Indicator device to label the stronghold on the player’s map.

To set up this device, configure the User Options as follows:

Map Indicator Settings
Option	Value	Explanation
Small Icon

UI Icon Enemy 64

Select an icon to be displayed.

Large Icon

UI Icon Enemy 128

Select an icon to be displayed.

Icon Color

Red

Select an icon color.

End Game Device
End Game Device
This tutorial uses three End Game devices for completing the stronghold with or without being detected or simply failing to eliminate all enemies.

To set up an End Game device for completing the stronghold without being detected, configure the User Options as follows:

End Game Settings
Option	Value	Explanation
Winning Team

Activating Team

Determines which team will win when the device is activated.

Custom Victory Callout

Stronghold was cleared! [Undetected]

Sets the message to be displayed on victory or cooperative game end.

Game End Callout

Cooperative

Sets the callout type of the game end screen. Cooperative shows everyone the same end screen using the Custom Victory Callout.

To set up an End Game device for completing the stronghold with alerted guards, configure the User Options as follows:

End Game Detetected
Option	Value	Explanation
Winning Team

Activating Team

Determines which team will win when the device is activated.

Custom Victory Callout

Stronghold was cleared! [Detected]

Sets the message to be displayed on victory or cooperative game end.

Game End Callout

Cooperative

Sets the callout type of the game end screen. Cooperative shows everyone the same end screen using the Custom Victory Callout.

To set up an End Game device if all players ran out of lives and could not eliminate all the stronghold guards, configure the User Options as follows:

End Game Fail
Option	Value	Explanation
Winning Team

Activating Team

Determines which team will win when the device is activated.

Custom Victory Callout

Game Over! Stronghold is Undefeated!

Sets the message to be displayed on victory or cooperative game end.

Game End Callout

Cooperative

Sets the callout type of the game end screen. Cooperative shows everyone the same end screen using the Custom Victory Callout.

Next Section
Add Verse Script to Devices

Player Spawner Devices
Use Player Spawn Pad Devices to spawn players onto your island.

Player Spawner Devices
The Player Spawn Pad spawns the player at any location on their island.

This device can only spawn one player. You will need to place individual spawners for islands with multiple players. Otherwise, they will always fall from the sky and have to parachute down.

For help on how to find the Player Spawner device, see Using Devices.

If you're using multiple copies of a device on an island, it can be helpful to rename them. You can choose names that relate to each device's purpose, so it's easier to remember what each one does.

Device Options
You can configure this device with the following options.

Default values are bold.

Option	Value	Description
Enabled During Phase

Always, None, Create Only, Game Countdown Only, Gameplay Only

Determines the game phases during which this device will be enabled during which the device will be enabled.

Player Team

None, Any, Pick a team

Determines which team spawns on this pad.

Player Class

Any, No Class, Pick a team

Determines which class can activate the device.

Priority Group

Don't Override, Pick a number

Determines the priority order in which spawn pads will be used. Use the arrows to pick a number, or click in the field and type in a number. If all Primary pads are unavailable, players will spawn on Secondary pads and the Tertiary.

Use as Island Start

On, Off

Determines whether or not a spawn pad can be used when players are spawning in to the island during the Pre-Game phase.

Visible in Game

On, Off

Determines whether the spawn pad is visible during games.

Play Audio

No, Yes, Only If Visible

Determines whether the device should play audio effects.

Enemy Range Check

None, Pick a range

If an enemy is within this radius, you can prefer not to spawn at this location. If no other locations are suitable, the player may still spawn here.

Display Enemy Range

Off, On, When Near

Visualizes the Enemy Range Check option value. The location sphere will never show while playing, only during Create mode.

Respawn Alive Players

Yes, No

If a Respawn at Player Spawner function is triggered, this determines if players who are alive are also respawned.

Direct Event Binding
Following are the direct event binding options for this device.

Functions
A function listens for an event on a device then performs an action.

For any function option, click the option, then Select Device to access and select from the Device dropdown menu.

Once you've selected a device, click Select Event to bind the timer to an event that will trigger the function for the device.

If more than one device should be affected by a function, press the Add button and repeat.

Option	Description
Enable When Receiving From

Enables the device when an event occurs.

Disable When Receiving From

Disables the device when an event occurs.

Spawn Player When Receiving From

Spawns a player at this spawner, or respawns an existing player, when an event occurs.

Events
An event tells another device when to perform a function.

For any event option, click the option, then Select Device to access and select from the Device dropdown menu.

Once you've selected a device, click Select Function to bind the timer to a function for that device.

If more than one device is affected by the function, press the Add button and repeat.

Option	Description
On Player Spawned Send Event To

When a player spawns or respawns from this spawner, this sends an event to the selected device, which triggers the selected function.

On Spawn Failed Send Event To

When a player would spawn or respawn from this spawner, but the spawner is invalid or ineligible for spawning, this sends an event to the selected device, which triggers the selected function.

Gameplay Examples
Loadout Lobby

Tug of War

devices
player
spawner

Guard Spawner Devices
Raise the stakes for your players by spawning guards to attack them!

Guard Spawner Devices
The Guard Spawner can spawn a group of enemies that patrol an area to protect it from players. Like sentries, guards have a detection system. This means players can disguise themselves or engage in stealth tactics, which gives players more strategic options for gameplay. Unlike sentries, however, guards will act as a team to attack players, or help other guards on their team.

You can determine whether players can hire guards or not, and if they can be hired you can customize many additional options related to hiring. You can also enable players to give hired guards commands, using the Can Be Given Commands option. Players can use the middle mouse button, or press the left arrow on the D-pad, to open the Command Wheel.

To find the Dance Mannequin device, see Finding and Placing Devices.

Contextual Filtering
Some devices are affected by a feature called contextual filtering. This feature hides or displays options depending on the values selected for certain related options. This feature will reduce clutter in the Customize panel and make options easier to manage and navigate.

However, it may not be easy to recognize which options or values trigger contextual filtering. To help you identify them, in our device docs we use italic for any values that trigger contextual filtering. All options will be listed, including those affected by contextual filtering; if they are hidden or displayed based on a specific option's value, there will be a note about that in the Description field for that option.

Device Options
This device has some basic functionality, like choosing the type and number of guards, and whether guards can spawn through walls. Additionally, there are some advanced options, like how many guards are spawned, and the amount of time between spawns.

You can configure this device with the following options.

Default values are bold. Values that trigger contextual filtering are italic.

Option	Value	Description
Guard Type

Shadow, Pick a guard type, Random

Choose what type of guard will spawn. There's a wide selection to choose from.

Spawn Count

4, Pick a number

This sets the maximum number of guards this device can have active at one time. When the device activates, it will spawn one guard at a time, until it has this number of guards active. An island can only have 30 active guards spawned across all Guard Spawner devices on the island.

Allow Infinite Spawn

Yes, No

Determines whether or not the device has a spawn limit.

Character Cosmetic

Don't Override, Pick a character skin

Determines what character skin the device uses.

Guard Team Option

Team Index, Team Neutral, Team Wildlife & Creatures

Determines the team type the guards will be assigned to. If you choose Team Index, another option displays below this one.

Guard Team Index

Team 1, Pick a team

This option only displays if the Guard Team Option is set to Team Index. Determines which team the guards are assigned to.

Spawn on Timer

On, Off

Determines if guards are spawned on the Spawn Timer countdown, or if they are spawned by events. If this is set to On, an additional option displays below this one.

Spawn Timer

3 seconds, Pick an amount of time

This option only displays if the Spawn On Timer option is set to On. Sets the minimum amount of time between the spawn of one guard and the next. Setting this to 0 means guards spawn as quickly as possible, but this is capped by performance limits.

Spawn Through Walls

On, Off

Determines whether guards must spawn within line of sight of the spawner, or whether they can spawn behind walls and inside buildings that are within range.

Show Spawn Radius

On, Off

Determines if the spawn radius is shown in a preview cylinder when you are editing your island.

Spawn Radius

10M, Pick a distance

The maximum distance at which a guard can spawn.

Use Device Spawn Rotation

On, Off

Determines whether guards' spawn orientation matches the device orientation. If this option is set to Off, the guard spawns facing the direction of the Patrol Path it spawns on.

Play Spawn Visual Effect

On, Off

Determines whether a visual effect plays when a guard spawns.

Enabled at Game Start

Enabled, Disabled

Determines whether the device is automatically enabled at the start of the game.

Invulnerable

On, Off

Determines if guards spawned are invulnerable or if they are damageable. If this is set to Off, two additional options display below this one.

Starting Health

100, Pick an amount

This option only displays if the Invulnerable option is set to Off. Determines the starting health value for spawned guards.

Max Health

100, Pick an amount

This option only displays if the Invulnerable option is set to Off. Determines the maximum health value for spawned guards.

Starting Shield

No Shield, Pick an amount

Determines the starting shield value for spawned guards.

Max Shield

No Shield, Pick an amount

Determines the maximum shield value for spawned guards.

Show Health Bar

Yes, No

Determines whether a guard's health is displayed in a health bar above the guard's head.

Enable Patrol

On, Off

This determines whether the guards move around to patrol an area, or whether they stay in one place.

Max Patrol Distance

10M, Pick a distance

This is the maximum amount of distance a patrolling guard can move from the spawner location. This does not apply if you are using an AI Patrol Path device to set specific Patrol Paths and Patrol Path Groups.

Spawn On Patrol Path Group

Group None, Pick a group number

Assigns guards to the selected Patrol Path Group.

Visibility Range

40M, Pick a distance

Sets the maximum distance for guards' sight perception. Guards can still become alerted based on sound regardless of this range.

Visibility Range Restriction

Only When Unaware, Always

Determines whether the value for the Visibility Range option is in effect always, or only when guards are not alerted.

Team Awareness Propagation

Yes, No

If the guards are assigned to a team, this determines whether a guard's detection of players is spread to the guard's team.

Drop Inventory On Elimination

Yes, No

Determines whether a guard drops their entire inventory when they are eliminated.

Accuracy

Moderate, Pick a level

Determines how accurate guards are when they shoot at players.

Despawn Guards when Disabled

Yes, No

Determines whether spawned guards remain or if they are despawned when the spawner is disabled.

Can Be Hired

Yes, No

Determines whether the spawned guards can be hired by a player. If you choose Yes, additional options display below this one.

Allow Hire Conversation

Yes, No

This option only displays if the Can Be Hired option is set to Yes. Determines whether players can hire guards using a conversation interaction. If you choose No, guards can only be hired or dismissed using events.

Hired Guard Name

Enter text

This option only displays if the Can Be Hired option is set to Yes. Type in a name for a hired guard. This name will be used in the "Hire a Guard" conversation. The text field is limited to 16 characters.

Maximum Hired Guards

Don't Override, Pick a number

This option only displays if the Can Be Hired option is set to Yes. Determines the maximum number of guards spawned by this device that a player can hire in the game. Don't Override means the maximum is the same as the value set in the Island Settings.

Auto Hire When Spawned

No Auto Hire, Last Hiring Player, Triggering Player

This option only displays if the Can Be Hired option is set to Yes. Determines whether the spawned guard is automatically hired. Values for this option are:

No Auto Hire: Spawned guards are not automatically hired.

Last Hiring Player: The spawned guard is automatically hired by the last hiring player.

Triggering Player: The spawned guard is automatically hired by the player that triggered the spawner.

Restore Health & Shield When Hired

No, Yes

This option only displays if the Can Be Hired option is set to Yes. Determines whether a damaged guard's health and shield will be restored to default values when the guard is hired.

Despawn When Dismissed

No, Yes

This option only displays if the Can Be Hired option is set to Yes. Determines whether the hired guard automatically despawns when the player dismisses the guard.

Can Be Given Commands

No, Yes

This option only displays if the Can Be Hired option is set to Yes. Determines if a spawned Guard can be given commands. By default, only the most recently hired Guard can be given commands.

Use Alertness

On, Off

Determines whether the guard displays its alertness level over its head.

Direct Event Binding
Following are the direct event binding options for this device.

Functions
A function listens for an event on a device then performs an action.

For any function, click the option, then Select Device to access and select from the Device dropdown menu.

Once you've selected a device, click Select Event to bind the device to an event that will trigger the function for the device.

If more than one device or event triggers a function, click the Add button to add a line and repeat these steps.

Option	Description
Enable When Receiving From

This function enables the device when an event occurs.

Disable When Receiving From

This function disables the device when an event occurs.

Spawn When Receiving From

This function spawns a guard when an event occurs.

Despawn When Receiving From

This function despawns a guard when an event occurs.

Reset Total Spawn Count When Receiving From

This function resets the total spawn count for this device when an event occurs.

Hire When Receiving From

This function hires a guard when an event occurs.

Dismiss All Hired Guards When Receiving From

This function dismisses any hired guards that spawned from this device when an event occurs.

Dismiss Instigator Hired Guards When Receiving From

This function dismisses any guards hired by the instigating player when an event occurs.

Set Guard Hireable When Receiving From

All guards spawned by this device are set as hireable when an event occurs.

Set Guard Not Hireable When Receiving From

All guards spawned by this device are set as not hireable when an event occurs.

Force Attack Target When Receiving From

When an event occurs, this function forces a guard to attack a specific target, bypassing perception checks.

Events
Direct event binding uses events as transmitters. An event tells another device to perform a function.

For any event option, click the option, then Select Device to access and select from the Device dropdown menu.

Once you've selected a device, click Select Function to bind the timer to a function for that device.

If more than one function is triggered by the event, click the Add button to add a line and repeat these steps.

Option	Description
On Spawned Send Event To

When the device spawns a guard, it sends an event to the selected device, which triggers the selected function.

On Alerted to Player Send Event To

When a guard is alerted to the player, it sends an event to the selected device, which triggers the selected function.

On Alerted to AI Send Event To

When a guard is alerted to an AI entity, it sends an event to the selected device, which triggers the selected function.

On Alerted Send Event To

When a guard is alerted, it sends an event to the selected device, which triggers the selected function.

On Target Lost Send Event To

When a guard loses sight of its target, it sends an event to the selected device, which triggers the selected function.

On Suspicious Send Event To

When a guard becomes suspicious, it sends an event to the selected device, which triggers the selected function.

On Unaware Send Event To

When a guard becomes unaware, it sends an event to the selected device, which triggers the selected function.

On Eliminated Send Event To

When a guard is eliminated, it sends an event to the selected device, which triggers the selected function.

On Eliminating Player Send Event To

When a guard eliminates a player, it sends an event to the selected device, which triggers the selected function.

On Eliminating AI Send Event To

When a guard eliminates an AI entity, it sends an event to the selected device, which triggers the selected function.

On Eliminating Send Event To

When a guard eliminates an opponent, it sends an event to the selected device, which triggers the selected function.

On Damaged Send Event To

When a guard takes damage, it sends an event to the selected device, which triggers the selected function.

On Hired Send Event To

When a guard is hired by a player, it sends an event to the selected device, which triggers the selected function.

On Dismissed Send Event To

When a player dismisses a guard, it sends an event to the selected device, which triggers the selected function.

Tracker Devices
Create and track custom objectives for your players to complete.

Tracker Devices
Use the Tracker device to create and track custom objectives that a player can complete, and send a signal to another device when the player completes a tracked objective.

You can track objectives set for individual players, a team, or multiple teams. For teams, you can also track persistence data for individual players from one session to the next. (For more on this, see Tracking Persistence Data below.

For help on how to find the Tracker device, see Using Devices.

You'll need a separate tracker for each objective you want to track.

If you're using multiple copies of a device on an island, it can be useful to rename them. Choosing names that relate to a device's purpose makes it easier to remember what each one does, and easier to find a specific device when using the Event Browser.

Contextual Filtering
Some devices are affected by a feature called contextual filtering. This feature hides or displays options depending on the values selected for certain related options. This feature will reduce clutter in the Customize panel and make options easier to manage and navigate.

However, it may not be easy to recognize which options or values trigger contextual filtering. To help you identify them, in our device docs we use italic for any values that trigger contextual filtering. All options will be listed, including those affected by contextual filtering; if they are hidden or displayed based on a specific option's value, there will be a note about that in the Description field for that option.

Device Options
This device has some basic functionality, like which stat is tracked, and the value for that stat when the target is met. There are also some advanced options, like whether completion progress is shared among team members or tracked individually.

Default values are bold. Values that trigger contextual filtering are italic.

You can configure this device with the following options.

Option	Values	Description
Stat to Track

Eliminations, Pick a stat to track

Determines which statistic the device will track for the Tracker Value.

Stats that can be tracked are:

Events

Eliminations (default)

Eliminated

Score

Chest Opened

Llama Opened

Player Revived

Player Interrogated

Race Checkpoint Activated

Fish Fished

Weapon Fished

Prop Destroyed

Shield Potion Consumed

Distance Traveled on Foot

Distance Traveled in Vehicle

Distance Traveled in Air

Distance Traveled

Round Completed

Round Won

Game Completed

Game Won

Play Time Elapsed

Reset on First Spawn

No, Yes

Determines whether the tracked stat will be reset when the player spawns in to a new game or round. If Stat to Track is set to Rounds Completed, Rounds Won, Games Complete, or Games Won, the device will not be reset regardless of the setting you select here.

Target Value

10, Pick a number

When the device counts to the selected value, the objective is complete. If you select 0, the tracker will never complete.

Starting Value

0, Pick or enter a number

Determines the value the tracker is set to when it first begins tracking.

Valid Team

Any, Pick or enter a number

This tracker can be assigned to players on the selected team.

Assign on Game Start

On, Off

Determines whether this tracker is assigned to applicable players when the game starts.

Assign When Joining in Progress

On, Off

Determines whether a player will be assigned this tracker when they join a game already in progress.

Sharing

Individual, Team, All

Determines whether progress is tracked for individual players, for all members of a team, or whether all players contribute progress toward a single target value. Note that if you want to use the Resolves Conflicts option with persistence data (statistics carried forward from session to session) you will need to set this to Team or All, as Resolves Conflicts doesn't apply to individual players. See Tracking Persistence Data for more info.

Target Team

Any, Pick or enter a number

Determines which team is tracked when the Stat to Track option is set to Eliminations or Eliminated.

Target Class

Any, Pick or enter a number

Determines which class is tracked when the Stat to Track option is set to Eliminations or Eliminated.

When Target Is Reached

Do Nothing, End Round, Complete Tracker

Determines what happens when the target tracker value is reached.

Winning Team

Completing Team Wins, Use Game Win Conditions, Pick or enter a number

Determines which team wins the round when the tracker is completed. This option is only valid if the When Target is Reached option is set to End Round.

Amount to Change on Event

1, Pick or enter a number

Determines how much to increment (add) or decrement (subtract) the tracker value each time the Increment Progress When Receiving From or Decrement Progress When Receiving From option is triggered.

Show on HUD

No, Detailed, List, Both

Determines whether tracker progress is displayed on the player's HUD. If you choose Detailed or Both, a color-coded text box displays in the upper left of the player's HUD.

Quest Box
Tracker Title

Enter text

Assigns a title to the tracker, which is displayed if Show on HUD is enabled. The text field has a 32-character limit.

Description Text

Enter text

Assigns a description to the tracker, which is displayed below the title if the Show on HUD option is enabled. The text field has a 64-character limit.

Show Progress

Total, Remaining, Off

Determines whether Tracker Progress is displayed after the Tracker Description if the Show on HUD option is enabled. If you choose Total, the tracker will count up to the target value. If you choose Remaining, the tracker will count down from the target value.

HUD Widget

Default, Slim, Tiny

Determines which widget is used for the HUD.

Tracker Completion Ceremony

Yes, No

Determines whether or not the completion of this tracker will be accompanied by a ceremony.

Quest Icon

None, Pick an icon

Sets the icon that shows on the quest box if the Shown on HUD option is set to show tracked stats. Click the icon to open the Icon Library picker, and choose an icon by scrolling through the Icon Library, or type a word into the search box to search for a specific icon. Select an icon, then click the checkmark. See the Icon List table below for available icons.

Icon Picker
Color

#FFFFFF, Pick a color

Sets the color of the icon and the quest box. Click the color swatch to open the color picker. Each color swatch has its hex code next to the swatch. You can also type a hex code into the search bar to find a specific color. Select a color, then click the checkmark.

Color Picker
Use Persistence

Off, On

Determines whether this device should load data from earlier game sessions. If you set this to On, more options will show. Also see Tracking Persistence Data below.

Auto Save

Yes, No

This only displays if Use Persistence is set to On. Determines if the device saves its data automatically.

Auto Load

Initial Spawn, Off

This only displays if Use Persistence is set to On. Determines whether the device data and player's progress is automatically loaded. If this is set to Initial Spawn, data will only be loaded when the player initially spawns. If this is set to Off, data is never auto-loaded, and the creator needs to activate this with an event.

Resolves Conflicts

Highest, Lowest, First Player, Average, Median

This option only displays if Use Persistence is set to On. Conflict resolution is how the game treats persistence data when players join a new session. When a tracker affects more than one player at the same time, the setting selected here will determine how the tracked value is applied. Note that this option only has an effect on the game if Sharing is set to Team or All. It has no effect if Sharing is set to Individual.

This option determines what number the tracker should start with at the beginning of a session.

Highest: Applies the highest value in the group to each player.

Lowest: Applies the lowest value in the group to each player.

First Player: Uses the value from the first player loaded into that session and applies it to each player in the group.

Average: Takes the average value across all tracked players in the current session.

Median: Takes the value in the middle of all sorted values for this session.

Resolves Conflict After Tracker Active

Yes, No

This option only displays if Use Persistence is set to On. This option determines whether the value of the tracked stat is recalculated based on the persistence value of new players.

Tracking Persistence Data
You can set the Tracker device to collect persistence data, meaning stats tracked across multiple sessions, with multiple players or teams.

Persistence is based on player data for a specific island, and will track multiple players for a single island.

For example, if you have a group quest where players have to collectively tame 200 wolves, but the group only manages to tame 100 before the session ends, a player can return the next day and continue taming the wolves. However, the player may be playing with a different group entirely, and that's where conflict resolution becomes important.

If the Resolves Conflict option is set to Average, in the new group, you might have one player with a persistent tracked value of 50, another with a value of 100, and a third player new to the game who starts with 0. In this case the starting value for each player would be 50+100+0/3, or 50 if you've selected Average.

The same tracked values set for Median would be 50, based on the median (middle) value: 0 - 50 - 100.

Direct Event Binding
Following are the direct event binding options for this device.

Functions
A function listens for an event on a device then performs an action.

For any function option, click the option, then Select Device to access and select from the Device dropdown menu.

Once you've selected a device, click Select Event to bind the timer to an event that will trigger the function for the device.

If more than one device should be affected by a function, press the Add button and repeat.

Option	Description
Remove From All When Receiving From

This function removes the tracker from all valid players when an event occurs.

Complete When Receiving From

Immediately completes the tracker when when an event occurs.

Reset Progress When Receiving From

Resets the progress for the triggering player (and any players sharing progress) when an event occurs.

Increment Progress When Receiving From

Increases the tracker's v+alue when an event occurs.

Remove When Receiving From

Removes the tracker from the triggering player, and any players sharing the event.

Assign When Receiving From

Assigns the tracker to the instigating player (and any players sharing progress) when an event occurs.

Assign to All When Receiving From

Assigns the tracker to all valid players when an event occurs.

Increase Target Value When Receiving From

Increases the value of the target when an event occurs.

Decrease Target Value When Receiving From

Decreases from the target value when an event occurs.

Decrement Progress When Receiving From

Subtracts from the target value when an event occurs.

Save When Receiving From

Saves the device data and player's personal progress when an event occurs.

Load for Player When Receiving From

Loads instigating player's data when an event occurs .

Load for All When Receiving From

Loads all player data when an event occurs.

Clear Persistence When Receiving From

Clears instigating player's data when an event occurs.

Save for All When Receiving From

Saves player data for all players when an event occurs.

Clear for All When Receiving From

Clears data for all players when an event occurs.

Events
An event tells another device when to perform a function.

For any event option, click the option, then Select Device to access and select from the Device dropdown menu.

Once you've selected a device, click Select Function to bind the timer to a function for that device.

If more than one device is affected by the function, press the Add button and repeat.

Option	Description
When Complete Send Event To

When the tracker completes, it sends an event to the selected device, which triggers the selected function.

On Saved Send Event To

When the tracker saves data and players progress, it sends an event to the selected device, which triggers the selected function..

On Loaded Send Event To

When the tracker loads data and players progress, it sends an event to the selected device, which triggers the selected function.

On Cleared Send Event To

When device clears persistent data, it sends an event to the selected device, which triggers the selected function.

Using the Tracker Device in Verse
You can use the code below to control a Tracker device in Verse. This code shows how to use events and functions in the Tracker device API. Modify it to fit the needs of your experience.

Verse
using { /Fortnite.com/Devices }
using { /Verse.org/Simulation }
using { /Verse.org/Random }
using { /UnrealEngine.com/Temporary/Diagnostics }

# A Verse-authored creative device that can be placed in a level
tracker_device_verse_example := class(creative_device):

    # Reference to the Switch Device in the level.
    # In the Details panel for this Verse device,
To use this code in your UEFN experience, follow these steps.

Drag a Tracker device onto your island.

Create a new Verse device named tracker_device_verse_example. See Create Your Own Device Using Verse for steps.

In Visual Studio Code, open tracker_device_verse_example.verse in Visual Studio Code and paste the code above.

Compile your code and drag your Verse-authored device onto your island. See Adding Your Verse Device to Your Level for steps.

Add a reference for the Tracker device on your island to your Verse device. See Adding a Verse Reference to a Creative Device in Your Level for steps.

Save your project and click Launch Session to playtest.

Tracker Device Verse API
See the tracker_device API Reference for more information on using the Tracker device in Verse.

HUD Message Devices
Create custom HUD messages for players based on time or activities.

HUD Message Devices
The HUD Message device displays messages to all players or specific ones, either through a trigger from another device or through a timer from the start of a round.

If you're using multiple copies of a device on an island, it can be helpful to rename them. Choosing names that relate to a device's purpose makes it easier to remember what each one does, and easier to find a specific device when using the Event Browser.

Contextual Filtering
Some devices are affected by a feature called contextual filtering. This feature hides or displays options depending on the values selected for certain related options. This feature will reduce clutter in the Customize panel and make options easier to manage and navigate.

However, it may not be easy to recognize which options or values trigger contextual filtering. To help you identify them, in our device docs we use italic for any values that trigger contextual filtering. All options will be listed, including those affected by contextual filtering; if they are hidden or displayed based on a specific option's value, there will be a note about that in the Description field for that option.

Device Options
You can configure this device with the following options.

Default values are bold. Values that trigger contextual filtering are italic.

Option	Value	Description
Message

Enter text and format text

Click the Format Styles tab to choose a style for your text. A list of styles available is on the right. Each individual word must be clicked to select, then clicked again to de-select it. When you want to apply a style, click every word you want to have that style. If you want some words to have one style, and other words to have a different style, make sure you de-select previously selected words before selecting new words for the next style.

Format Styles Tab
Show on Round Start

Off, On

Determines if the message automatically appears at the start of a round. If you set this to On, another option displays below this one.

Time From Round Start

Off, 10 seconds, Pick an amount of time

This only displays if the Show on Round Start option is set to On. Displays the message based on the length of time after the round starts.

Background Opacity

0\%, Pick or enter a percentage

Determines the opacity of the message's background. By default, the background is transparent.

Background Color

#2600CE, Pick a color swatch

If you have set a background opacity in the Background Opacity option, this determines the color of the background. Click the color swatch to open the Color Picker. Each color swatch has its Hex Code next to the swatch. You can also type a Hex Code into the Search bar to find a specific color. Select a color, then click the checkmark.

Color Picker
Message Recipient

All, Friendlies, Enemies, Triggering Player, Pick or enter a team number  

Determines which players receive the HUD message.

Show for Duration

Timed, Permanent  

Determines whether the device shows the message for a specific period of time. If you choose Timed, the Display Time option displays below this one.  

Display Time

5 seconds, Permanent, Pick an amount of time  

This option only displays if the Show for Duration option is set to Timed. Determines how long the message id displayed.  

Text Style

Default, Pick a style  

Determines the style applied to the message text when it is displayed.

Play Sound

Message - Important, Pick a sound  

Determines which sound should accompany the message when it is displayed.

Placement

Bottom Center, Top Center, Center Right, Custom

Choose where in the HUD the message displays. If you choose Custom, several additional options are displayed below this one.  

Screen Anchor

Top Left, Top Center, Top Right, Center Left, Center, Center Right, Bottom Left, Bottom Center, Bottom Right  

This option is only displayed if you have the Placement option is set to Custom. Determines where on the screen the message is anchored, as well as the alignment of the message itself.  

Placement Horizontal

0, Pick a positive or negative number  

This option is only displayed if you have the Placement option is set to Custom. Determines how far away, in pixels, the message is from the anchor point set in the Screen Anchor option. Positive numbers move it to the right, negative numbers move it to the left.  

Placement Vertical

0, Pick a positive or negative number  

This option is only displayed if you have the Placement option is set to Custom. Determines how far away, in pixels, the message is from the anchor point set in the Screen Anchor option. Positive numbers move it upward, negative numbers move it downward.  

HUD Widget

Basic, Critical  

Determines the visuals of the HUD message.

Layer

0, Pick a layer number  

Determines what layer the message displays on. Only one message at a time will display on a layer, and any other messages set to that layer will be queued. Setting messages to different layers causes multiple messages to be displayed simultaneously.

Priority

5, Display Immediately, Pick or enter a priority number  

Determines the priority for this message. Messages with a lower number (such as 1) are a higher priority, and will move any displayed message on the same layer to a queue. If you choose Display Immediately the message will display immediately and ignore any other messages.  

Allow Multiple in Queue

Off, On  

By default, a message will only be queued if the device doesn't already have a message in the queue, or a message already displayed. If you choose On, you can have multiple messages queued on this device.    

Show Behavior If Showing

Reset Display Time, Replay, Ignore  

Determines what happens if the device is directed to display a message when that message is already displayed.

Queue Timeout

Don't Queue, Pick an amount of time  

If a message is queued because a higher priority message is being displayed, this determines how long the message remains in the queue.

Queue Message for Join In Progress Players

On, Off  

Determines if this message is queued and then displayed to players that join the game while it is in-progress. This takes into account the value set for the Queue Timeout option.  

Re-Evaluate Messages On Show

Off, On  

When a message is ready to be displayed, this determines if it is checked to make sure it is still relevant. This is useful if players can change class or team during the game, or otherwise become ineligible to see a message.

Intro Animation

None, Zoom, Fade and Zoom, Fade, Reverse Zoom, Bounce, Slow Zoom, Slow Fade and Zoom, Slow Fade, Slow Reverse Zoom, Slide From Top, Slide From Bottom, Slide From Left, Slide From Right  

Determines how the HUD Message is animated as it displays.

Outro Animation

None, Zoom, Fade and Zoom, Fade, Reverse Zoom, Bounce, Slow Zoom, Slow Fade and Zoom, Slow Fade, Slow Reverse Zoom, Slide From Top, Slide From Bottom, Slide From Left, Slide From Right  

Determines how the HUD Message is animated as it is removed.

Text Style Set

Don't Override, Default, Legacy HUD  

Determines the style set for the text.

Don't Override: This uses the text style set in the My Island settings.

Default: This uses the new default style for the HUD Message device.

Legacy HUD: This uses the text style from the old HUD Message device.  

Override Default Text Style

On, Off  

Determines if the device uses the text style set in the Text Style Set option, or if you can customize the text style. If this is set to On, multiple additional options are displayed that allow you to customize the text style.  

Text Color

White, Pick a color swatch  

This option is only displayed if Override Default Text Style is set to On. Determines the color of the text in the HUD Message. Click the swatch to open the Color Picker. This is similar to the Color Picker for Background Color, but has names for colors rather than Hex Codes. Select a color, then click the checkmark to close the Color Picker.  

Shadow Offset

1, Pick or enter a number  

This option is only displayed if Override Default Text Style is set to On. Determines the drop-shadow offset amount.  

Outline Strength

1, Pick or enter a number    

This option is only displayed if Override Default Text Style is set to On. Determines the outline strength on the text.  

Size

18, Pick or enter a size  

This option is only displayed if Override Default Text Style is set to On. Determines the font size of the text.  

Text Justification

Left, Center, Right, Invariant Left, Invariant Right  

Determines which side the text is aligned to. If you choose Invariant Left or Invariant Right, the text aligns to that side no matter what language the text is displayed in.  

Direct Event Binding
Direct event binding allows devices to communicate directly, which makes your workflow more intuitive, and gives you more freedom to focus on your design ideas.

Below are the functions and events for this device.

Functions
A function listens for an event on a device then performs an action. 

For any function, click the option, then Select Device to access and select from the Device dropdown menu.

Once you've selected a device, click Select Event to bind the device to an event that will trigger the function for the device.

If more than one device or event triggers a function, click the Add button to add a line and repeat these steps.

Option	Description
Show When Receiving From

This function displays the HUD message when an event occurs. If more than one device or event can display message, you can click the Add button for this option, which adds another line.

Hide When Receiving From

This function hides the message. If more than one device or event can hide the message,you can click the Add button for this option, which adds another line.

Clear Layer When Receiving From

This function clears all text layers when an event occurs. If more than one device or event can clear all layers, click the Add button to add another line.

Events
This device has no events.

Item Granter Devices
Use this device to grant items to a player during the game.

Item Granter Devices
The Item Granter device can automatically place items into player inventories during your game, or you can set conditions for manually placing items in player inventories.

You can determine what items are granted and when, and set other conditions by configuring the device using the options listed below. You can set whether to send an item to a player's inventory, or drop it near a player in-game. You can also use other devices to trigger the Item Granter.

To register items with the Item Granter, follow these steps.

In the Creative inventory, use the Weapons and Items tabs to find the items you want to register with the Item Granter. Click EQUIP to put them in your Player inventory.

Stand directly beside the Item Granter.

Press the Tab key to open the Creative inventory screen, then click PLAY to switch to the Player inventory screen.

Click the desired item, then press either Z or X to split or drop the item. You can also drag the item to the side until a backpack icon appears.

When an item is registered with the Item Granter using the steps above, a hologram of the registered item will float above the device.

Like the Item Spawner, this device is the recommended method of delivering items and weapons to players in game.

The difference between the Item Spawner and the Item Granter is that the Item Spawner creates the registered item and drops it into the game world for players to pick up while the Item Granter automatically places the registered devices into the player's inventory.

Looking for more inspiration? See D-Launcher Device Design Examples to kick off your imagination!

To find the Item Granter device, go to the Creative inventory and select the Devices tab. From there you can search or browse for the device. For more information on finding devices see Using Devices.

If you're using multiple copies of a device on an island, it can be helpful to rename them. You can choose names that relate to each device’s purpose, so it’s easier to remember what each one does.

Device Options
The Item Granter has some basic functionality, like what item to grant to players, what to do with a player's existing inventory when granting an item, and whether to give a player extra ammo if the player is given a weapon. Additionally, there are some advanced options, like setting conditions for when a player is granted an item, if players from certain teams get different items, and how the items in the device are cycled.

Contextual Filtering
Some devices are affected by a feature called contextual filtering. This feature hides or displays options depending on the values selected for certain related options. This reduces clutter in the Customize panel and makes options easier to manage and navigate. To help identify them, values that trigger contextual filtering are in italic.

All options are listed, including those affected by contextual filtering; if they are hidden or displayed based on a specific option's value, there will be a note about it in the Description field for that option.

You can configure this device with the following options.

Default values are bold. Values that trigger contextual filtering are italic.

Option	Value	Description
Enabled on Game Start

Yes, No

Determines whether or not the device is enabled when the game starts.

Receiving Players

Triggering Team, Triggering Player, All, Pick a team

Determines which players receive the item.

On Grant Action

Clear Inventory, Clear Items, Clear Resources, Keep All

Defines the action that occurs when the device grants an item to a player.

Grant

Current Item, All Items

Current Item: Only the item selected on the device is granted to the player. All Items: All the items registered with the device are granted to the player.

Grant Condition

Always, Only If Empty, Only If Space, Only If Not Owned

Only grants items to players that meet this condition.

Values for this option are:

Always: Always grants items to players.

Only If Empty: Only grants items to players if their inventory is completely empty.

Only If Space: Only grants items to players if there is space in the player's inventory.

Only If Not Owned: Only grants items to players if the item is not already in the player's inventory.

Grant on Cycle

Yes, No

When the device cycles to a new item, it grants that new item to the player.

Equip Granted Item

No, Yes

If the device gives items, equip the item listed. If Yes is selected, the Item On Grant option becomes available.

Item to Grant

Item 1, Pick an item number

This option only appears if Equip Granted Item is set to Yes. If the device gifts items, equip the item listed here. If you choose an item later than the number gifted, the last item will be equipped instead.

Remove Item On Grant

No, Yes

When an item is granted, it is removed from the Item Granter.

Initial Weapon Ammo

Don't Override, select a number from 1 to 999

Sets the amount of ammunition loaded in the weapon when granted, limited by the weapon's magazine size.

Spare Weapon Ammo

Default, select a number from 1 to 999

Sets how much spare ammunition is added to the player's inventory when a weapon is granted. Default provides ammo based on the ammo type used by the weapon.

Cycle Behavior

Stop, Wrap

Determines how the device cycles through the items registered to the device.

Values for this option are:

Stop: The device cannot cycle forward past the last item, or cycle backward past the first item.

Wrap: When the device reaches the last item registered, it will cycle around to the first item.

Grant while offline

No, Yes

If you choose Yes the device will continue granting items to players, even while they are not on the island.

Drop Items at Player Location

Never, Always, If Inventory Full

Determines when an inventory item should be dropped at the player's location rather than place it in the player's inventory. If set to Never, the Ownership of Dropped Item option becomes hidden.

Ownership of Dropped Item

All, Receiving Player, Instigator

Determines who can pick up a dropped item.

Values for this option are:

All: Any player can pick up the item.

Receiving Player: Only the receiving player can pick up the item.

Instigator: Only the player who instigates the device can pick up the item.

Grant on Timer

Off, Pick an amount of time

If this option is set to an amount of time, the device grants items to players every time that amount of time has passed.

Grant Time

Pick a time

Grants an item at intervals based on time set.

Play Audio

No, Yes

Determines whether the device plays audio effects.

Grant on Game Start

Off, On

Set whether player gets the item at the start of the game.

Direct Event Binding
Following are the direct event binding options for this device.

Functions
A function listens for an event on a device then performs an action.

For any function option, click the option, then Select Device to access and select from the Device dropdown menu.

Once you've selected a device, click Select Event to bind the timer to an event that will trigger the function for the device.

If more than one device should be affected by a function, press the Add button and repeat.

Option	Description
Enable When Receiving From

Enables the device when an event occurs.

Disable When Receiving From

Disables the device when an event occurs.

Grant Item When Receiving From

Grants an item when an event occurs.

Cycle To Previous Item When Receiving From

The device cycles to the previous item when an event occurs.

Cycle To Next Item When Receiving From

The device cycles to the next item when an event occurs.

Cycle To Random Item When Receiving From

The device cycles to a random item when an event occurs.

Restock Items When Receiving From

If items have been removed from the device, the device is restocked with items when an event occurs.

Clear Save Data For Player When Receiving From

This option only works when the Grant While Offline is set to Yes. The instigating player no longer receives items when that player is offline.

Events
An event tells another device when to perform a function.

For any event option, click the option, then Select Device to access and select from the Device dropdown menu.

Once you've selected a device, click Select Function to bind the timer to a function for that device.

If more than one device is affected by the function, press the Add button and repeat.

Option	Description
On Item Granted Send Event To

When the device grants an item to a player, it sends an event to the selected device, which triggers the selected function.

Gameplay Examples Using Item Granters
Mazey Escape

End Game Devices
Determine when to end a round or game.

End Game Devices
You can set the End Game device to end either the current round or the entire game, and determine which team met the conditions for the win condition.

This device can be activated by another device using direct event binding.

  To find the End Game device, see Using Devices.  

If you're using multiple copies of a device on an island, it can be helpful to rename them. Choosing names that relate to a device's purpose makes it easier to remember what each one does, and easier to find a specific device when using the Event Browser.

Contextual Filtering
Some devices are affected by a feature called contextual filtering. This feature hides or displays options depending on the values selected for certain related options. This feature will reduce clutter in the Customize panel and make options easier to manage and navigate.

However, it may not be easy to recognize which options or values trigger contextual filtering. To help you identify them, in our device reference documents we use italic for any values that trigger contextual filtering. All options will be listed, including those affected by contextual filtering; if they are hidden or displayed based on a specific option's value, there will be a note about that in the Description field for that option.

Device Options
This device has some basic functionality, like displaying custom victory callouts and determining which team wins the game as well as more advanced functions.

Default values are bold. Values that trigger contextual filtering are italic.

Use the options below to customize this device.

Option	Value	Description
What to End

End Round, End Game

When activated, it determines whether the round ends or the entire game ends.

Winning Team

Winning Team, Activating Team, Pick a team

Determines which team will win when the device is activated. Requires the selected team to have at least one player. Use the arrows to choose a team, or click in the field to type in a team number.

Custom Victory Callout

Enter text

Enter a message to be displayed on victory or cooperative game end. The field has a 150-character limit.

Custom Defeat Callout

Enter text

Enter a message to be displayed on the defeat screen. The field has a 150-character limit.

Game End Callout

You Win/Lose, Placement, Cooperative

This determines what displays on the game-end screen. By default, it displays You Win or You Lose. If you choose Cooperative, everyone is shown the same game-end screen, which uses the sound selected in the Victory Sound setting and the text entered in the Custom Victory Callout setting.

Enabled at Game Start

Enabled, Disabled

Determines if this device is enabled when the game is started.

Activating Team

Any, Pick a team

Determines which team can activate the device. Use the arrows to choose a team, or click in the field to type in a team number.

Allowed Class

No Class, Any, Pick a class

Determines which class can activate the device. Use the arrows to choose a class, or click in the field to type in a class number.

Post Game Type

Classic, Battle Royale, Custom

Classic uses the Creative game-end screen. If you choose Battle Royale, your game uses the Fortnite Battle Royale game-end screen. If you choose Custom, more options display that you can use to customize the game-end screen.

Custom Show Scoreboard

Off, On

Determines whether the scoreboard is displayed at the end of the game. This option only displays if you set the Post Game Type as Custom.

Custom Victory Animation Style

Lightning Bolts, Pick a style

Determines the style used for the custom victory game-end animation. Only displays if Post Game Type is Custom.

Custom Victory Animation Color Set

Golden Yellow, Pick a color

Determines the color set used for the custom Victory game-end animation. Only displays if Post Game Type is Custom.

Custom Victory Animation Text

Enter text

Type in the text you want displayed at game-end for the ictory condition. The text field is limited to 15 characters. Only displays if Post Game Type is Custom.

Custom Victory Animation Sub Text

Enter text

Type in flavor text displayed at game end for the victory condition. The text field is limited to 84 characters.

Custom Defeat Animation Style

Lightning Bolts, Pick a style

Determines the style used for the custom defeat game-end animation.

Custom Defeat Animation Color Set

Golden Yellow, Pick a color

Determines the color set used for the custom defeat game-end animation.

Custom Defeat Animation Text

Enter text

Type in the text you want displayed at game end for the Defeat condition. The text field is limited to 15 characters.

Custom Defeat Animation Sub Text

Enter text

Type in flavor text displayed at game end for the Defeat condition. The text field is limited to 84 characters.

Custom Tie Animation Style

Lightning Bolts, Pick a style

Determines the style used for the custom tie game-end animation. Only displays if Post Game Type is Custom.

Custom Tie Animation Color Set

Golden Yellow, Pick a color

Determines the color set used for the custom tie game-end animation. Only displays if Post Game Type is Custom.

Custom Tie Animation Text

Enter text

Type in the text you want displayed at game end for the tie condition. The text field is limited to 15 characters. Only displays if Post Game Type is Custom.

Custom Tie Animation Sub Text

Enter text

Type in flavor text to display at game end for the tie condition. The text field is limited to 84 characters. Only displays if Post Game Type is Custom.

Direct Event Binding
Following are the direct event binding options for this device.

Functions
A function listns for an event on a device then performs an action.

For any function, click the option, then Select Device to access and select from the Device dropdown menu.

Once you've selected a device, click Select Event to bind the device to an event that will trigger the function for the device.

If more than one device or event triggers a function, click the Add button to add a line and repeat these steps.

Option	Description
Activate When Receiving From

Ends the round or game when an event occurs.

Enable When Receiving From

Enables the device when an event occurs.

Disable When Receiving From

Disables the device when an event occurs.

Events
This device has no events.

Map Indicator Devices
Place custom points of interest and markers to orient players and direct their attention.

Map Indicator Devices
The Map Indicator device lets you add points of interest to your island that can help players quickly orient to where they are in relation to where they want to go.

These markers display on both the minimap and the overview map.

To find the Map Indicator device, go to the Creative inventory and select the Devices tab. From there you can search or browse for the device. For more information on finding devices, Using Devices.

Device Options
This device has some basic functionality, like determining the icon and icon color, and entering text to display at the indicator location. Additionally, there are some advanced options, like determining which team can see the indicator.

You can configure this device with the following options.

Default values are bold.

Option	Value	Description
Enabled on Game Start

Yes, No

Determines whether the device is enabled when the game starts.

Icon

A, Pick an icon

Sets the icon the map indicator displays on the map. Click the right arrow to open the Icon Library Picker. Choose an icon by scrolling through the Icon Library, or enter a word in the search bar to find a specific icon. Select an icon, then click the checkmark to close the Icon Picker.

Icon Picker
Icon Color

White, Red, Orange, Yellow, Green, Teal, Blue, Purple

Determines the color of the icon.

Show on Which Map

Both, Minimap, Overview Map

Control which maps you want the indicator to display on.

Text

Enter text

You can type in text you want to be displayed on the map at the indicator location. The text field has an 80 character limit.

Text Color

White, Red, Orange, Yellow, Green, Teal, Blue, Purple

Determines the color of the text. Use the Color Picker to find a color.

Assigned Team

All, Pick a team

Determines which team can see the map indicator.

Invert Team

No, Yes

If you select Yes, the Assigned Team is the only team that cannot see the map indicator. If you leave the default No,the assigned team is the only team that can see it.

Assigned Class

Any, No Class, Pick a class

Players with the selected class assigned can activate the device. If you choose No Class, only players who are not assigned a class can activate it. If you choose Any, all players with an assigned class can activate it.

Invert Class

No, Yes

By default, only the Assigned Class can see the map indicator. If you set this to Yes, the assigned class is the only class that cannot see it.

Show Objective Pulse to Instigator Only

On, Off

The Objective Pulse will only appear or disappear for the activating player.

Show Objective Pulse to Friendly Players

On, Off

An Objective Pulse will appear to Friendly players, indicating the location of the device in relation to the player.

Icon Scale

1.0, select a value

Select a number less than 1.0 to make it smaller, or more than 1.0 to make it larger.

Direct Event Binding
Direct event binding allows devices to communicate directly, which makes your workflow more intuitive, and gives you more freedom to focus on your design ideas.

Below are the following direct event binding options for this device.

Functions
A function listens for an event on a device then performs an action.

For any function option, click the option, then Select Device to access and select from the Device dropdown menu.

Once you've selected a device, click Select Event to bind the timer to an event that will trigger the function for the device.

If more than one device should be affected by a function, press the Add button and repeat.

Option	Description
Enable When Receiving From

Enables this device when an event occurs.

Disable When Receiving From

Disable this device when an event occurs.

Activate Objective Pulse When Receiving From

When an event occurs that triggers this device, it activates a pulse near the instigating player that points toward the device.

Deactivate Objective Pulse When Receiving From

Deactivates the pulse when an event occurs.

Events
This device has no events.

Gameplay Examples Using Map Indicators
Search and Destroy

3. Add Verse Script to Devices
Learn how to set up the Verse device to customize gameplay.

3. Add Verse Script to Devices
This section will show you how to add the Verse script and place the Verse device to customize gameplay.

Verse
Navigate to Verse > Verse Explorer to create a Verse script.

Verse Explorer
Then, right-click your project file name and select Add new Verse file to project.

New File
Select Verse Device and give it a name then click Create. In this tutorial, the Verse device is named Stronghold_Game_Manager.

Verse Script
Double-click the device’s verse file to bring up the Verse script. Copy and paste the code below.

Verse
using { /Fortnite.com/AI }
using { /Fortnite.com/Characters }
using { /Fortnite.com/Devices }
using { /Fortnite.com/Game }
using { /UnrealEngine.com/Temporary/Diagnostics }
using { /UnrealEngine.com/Temporary/SpatialMath }
using { /Verse.org/Simulation }
using { /Verse.org/Verse }

# The Stronghold is a game mode in which the goal is for players to eliminate all hostile enemies at a heavily guarded Stronghold
Build Code
Next, navigate to Verse > Build Verse Code to compile the Verse script.

Content Drawer
Navigate to All/"Project Name"/CreativeDevices/ and select your Verse device.

Device Drag
Then, drag your Verse device onto your map. This will only appear after compiling the Verse script.

With your Verse device selected, navigate to the Details panel and update the User Options as shown below.

Device Settings
Option	Value	Explanation
Visible in Game

True

This device will be visible during the game.

Enabled at Game Start

True

This device will be enabled when the game begins.

Guards_InitialSpawners

7 Array elements

Click the plus sign to add three elements to this setting.

0

Guard Spawner Init

This is an array of all the devices used to spawn the initial Guards at the stronghold.

1

Guard Spawner Sniper Tower 1

This is an array of all the devices used to spawn the initial Guards at the stronghold.

2

Guard Spawner Sniper Tower 2

This is an array of all the devices used to spawn the initial Guards at the stronghold.

3

Guard Spawner Investigate Crash

This is an array of all the devices used to spawn the crash site Guards.

4

Guard Spawner Initial Move to Sniper A

This is an array of all the devices used to move a set of Guard spawners.

5

Guard Spawner Initial Move to Sniper B

This is an array of all the devices used to move a set of Guard spawners.

4

Guard Spawner Init Patrol

This is an array of all the devices used to move a set of patrol Guards.

GuardsInitialSpawnersAdditional

Guard Spawner Init Additional

Spawns an additional set of guards.

GuardReinforcementSpawners

Guard Spawner Reinforcement_East

Spawns reinforcement guards for a certain area.

GuardReinforcementSpawners

Guard Spawner Reinforcement_North

Spawns reinforcement guards for a certain area.

GuardReinforcementSpawners

Guard Spawner Reinforcement_West

Spawns reinforcement guards for a certain area.

GuardReinforcementSpawnersAdditional

Guard Spawner Reinforcement_East_Additional

Spawns additional reinforcement guards for a certain area.

GuardReinforcementSpawnersAdditional

Guard Spawner Reinforcement_West_Additional

Spawns additional reinforcement guards for a certain area.

Objective Tracker

Tracker

Displays the stronghold objectives and elimination count.

MessageDeviceReinforcement

HUD Message Device Reinforcement

Displays the reinforcement on-screen message.

MessageDeviceFallback

HUD Message Device Fallback

Displays the fallback on-screen message.

EndGameVictoryDeviceUndetected

End Game Device Undetected

Displays the victory and undetected end screen.

EndGameVictoryDeviceDetected

End Game Device Detected

Displays the victory and detected end screen.

EndGameFailDevice

End Game Device Fail

Displays the failed end screen because the player ran out of lives.

PlayerRetries

2

Determines the number of lives the player has to try to complete the stronghold successfully. If the player runs out of lives, the stronghold is failed.

ReinforcementLeashReferernce

Leash Position Stronghold

The Leash Position devices use its position as the origin of the reinforcement leash.

FallbackLeashReference

Leash Position Fallback

The Leash Position device uses its position as the origin of the fallback leash.

LeashesToDisableForFallback

5 Array elements

Determines the leashes to disable for guards to fallback.

0

Guards Leash Position 1

Determines the outer radius for the stronghold leash.

1

Guards Leash Position 2

Determines in centimeters the inner radius for the defend fallback leash. Must be smaller than the outer radius.

2

Reinforcement Leash Position

Determines the reinforcement leash position.

3

Sniper tower 1 leash position

Determines the leash position for the first sniper tower.

4

Spiper tower 2 leash position

Determines the leash position for the second sniper tower.

Explosive Device

Explosive Device

References the Explosive Barrel device.

Next Section
Set Up Leash Devices

4. Set Up Leash Devices
Learn how to set up leash devices for AI to patrol.

4. Set Up Leash Devices
This section will show you how to set up the leash devices that control the areas that the AI guards will patrol.

Leashes
A leash is a custom location set in Verse to tell guards where to move. Use a leash to designate locations for guards to patrol in the stronghold.

Guards will only patrol if they have the patrol flag enabled. Otherwise, they will stand still until they see a threat.

In this tutorial, we will use a prop, the Verse device, as a dummy to easily move the center of the leashes.

Verse Explorer
To create a new Leash Position device, click the Verse header make sure the Verse Explorer is checked.

Add Verse File
Next, navigate to the Verse Explorer tab and right-click your project file, then select Add new Verse file to project.

Verse Script
Select Verse device and give it a name, then click Create.

Double-click the device Verse file to bring up the Verse script. Copy and paste the code below.

Verse
using { /Fortnite.com/AI }
using { /Fortnite.com/Characters }
using { /Fortnite.com/Devices }
using { /UnrealEngine.com/Temporary/SpatialMath }
using { /Verse.org/Random }
using { /Verse.org/Simulation }
# Defines a leash volume that can be assigned to guards
stronghold_leash_position := class(creative_device):
    # Leash is applied by default to all guards spawned by those devices
    @editable
    GuardsSpawners:[]guard_spawner_device := array{}
    # Guards on those patrol paths can go outside the leash (only one device per path)
    @editable
    PatrolPaths:[]ai_patrol_path_device := array{}
    # Set the leash inner radius. This value must be in centimeters.
    # This defines the volume that must be reached when this leash is assigned to guards
    @editable
    LeashInnerRadius<private>:float = 2300.0
    # Set the leash outer radius. This value must be in centimeters
    # This defines the volume in which guards must stay in when this leash is assigned
    @editable
    LeashOuterRadius<private>:float = 2400.0
    # List of guards currently assigned to this leash
    var<private> Guards : []agent = array{}
    OnBegin<override>()<suspends>:void=
        for (GuardSpawner : GuardsSpawners):
            GuardSpawner.SpawnedEvent.Subscribe(ApplyLeashOnGuard)
        for (PatrolPath : PatrolPaths):
            PatrolPath.PatrolPathStartedEvent.Subscribe(PatrolPathStarted)
            PatrolPath.PatrolPathStoppedEvent.Subscribe(PatrolPathStopped)
    ApplyLeashOnGuard(Guard:agent):void=
        if (Leashable:=Guard.GetFortCharacter[].GetFortLeashable[]):
            Leashable.SetLeashPosition(GetTransform().Translation, LeashInnerRadius, LeashOuterRadius)
           set Guards += array{Guard}
    ClearLeashOnGuard(Guard:agent):void=
        if (Leashable:=Guard.GetFortCharacter[].GetFortLeashable[]):
            Leashable.ClearLeash()
       option {set Guards = Guards.RemoveFirstElement[Guard]}
    DisableLeashAndPatrolPaths():void=
        for (Guard : Guards):
            if (Leashable:=Guard.GetFortCharacter[].GetFortLeashable[]):
                Leashable.ClearLeash()
        for (PatrolPath : PatrolPaths):
            PatrolPath.Disable()
        set Guards = array{}
    PatrolPathStarted(Guard:agent):void=
        if:
            Guards.Find[Guard]
            Leashable:=Guard.GetFortCharacter[].GetFortLeashable[]
        then:
            Leashable.ClearLeash()
    PatrolPathStopped(Guard:agent):void=
        if:
            Guards.Find[Guard]
            Leashable:=Guard.GetFortCharacter[].GetFortLeashable[]
        then:
            Leashable.SetLeashPosition(GetTransform().Translation, LeashInnerRadius, LeashOuterRadius)
using { /Fortnite.com/AI } using { /Fortnite.com/Characters } using { /Fortnite.com/Devices } using { /UnrealEngine.com/Temporary/SpatialMath } using { /Verse.org/Random } using { /Verse.org/Simulation } # Defines a leash volume that can be assigned to guards stronghold_leash_position := class(creative_device): # Leash is applied by default to all guards spawned by those devices @editable GuardsSpawners:[]guard_spawner_device := array{} # Guards on those patrol paths can go outside the leash (only one device per path) @editable PatrolPaths:[]ai_patrol_path_device := array{} # Set the leash inner radius. This value must be in centimeters. # This defines the volume that must be reached when this leash is assigned to guards @editable LeashInnerRadius<private>:float = 2300.0 # Set the leash outer radius. This value must be in centimeters # This defines the volume in which guards must stay in when this leash is assigned @editable LeashOuterRadius<private>:float = 2400.0 # List of guards currently assigned to this leash var<private> Guards : []agent = array{} OnBegin<override>()<suspends>:void= for (GuardSpawner : GuardsSpawners): GuardSpawner.SpawnedEvent.Subscribe(ApplyLeashOnGuard) for (PatrolPath : PatrolPaths): PatrolPath.PatrolPathStartedEvent.Subscribe(PatrolPathStarted) PatrolPath.PatrolPathStoppedEvent.Subscribe(PatrolPathStopped) ApplyLeashOnGuard(Guard:agent):void= if (Leashable:=Guard.GetFortCharacter[].GetFortLeashable[]): Leashable.SetLeashPosition(GetTransform().Translation, LeashInnerRadius, LeashOuterRadius) set Guards += array{Guard} ClearLeashOnGuard(Guard:agent):void= if (Leashable:=Guard.GetFortCharacter[].GetFortLeashable[]): Leashable.ClearLeash() option {set Guards = Guards.RemoveFirstElement[Guard]} DisableLeashAndPatrolPaths():void= for (Guard : Guards): if (Leashable:=Guard.GetFortCharacter[].GetFortLeashable[]): Leashable.ClearLeash() for (PatrolPath : PatrolPaths): PatrolPath.Disable() set Guards = array{} PatrolPathStarted(Guard:agent):void= if: Guards.Find[Guard] Leashable:=Guard.GetFortCharacter[].GetFortLeashable[] then: Leashable.ClearLeash() PatrolPathStopped(Guard:agent):void= if: Guards.Find[Guard] Leashable:=Guard.GetFortCharacter[].GetFortLeashable[] then: Leashable.SetLeashPosition(GetTransform().Translation, LeashInnerRadius, LeashOuterRadius)
In the Verse tab, select Build Verse Code to compile the Verse script.

Leash Device
From the Content Browser, find the Verse device in All/"Project Name"/Creative Devices/.

Place two Leash Position devices, one for the stronghold leash and one for the fallback leash. You can name them to easily differentiate between the two.

Leash Settings
In the Leash Position properties, uncheck Visible in Game so these devices are hidden when playing.

Earlier in the Stronghold Game Manager, you already set the inner and outer radius for the leash.

AI Patrol Path Setup
You can use the AI Patrol Path Node devices to set up with the default patrolling behaviors for the Guard AIs.

AI Patrol Path
To make the AI Patrol Path Node device work as the initial patrolling behavior, set the Guard Spawner’s setting Spawn on Patrol Path Group to be the same value of the AI Patrol Path Node device’s setting Patrol Path Group.

The AI Patrol Path Node device can also be assigned or disabled at runtime through event binding or its associated Verse APIs.

Patrol Path
Patrol Path
Like the above images, you will need to set the Patrol Path Group option to same number for both the Guard Spawner and the AI Patrol Path Node. Doing this will cause the spawned AIs to pick the patrol path to use.

Debug AI Navmesh
Debug View
You can turn on the navmesh debug view from the Island Settings and enable both Debug & Navigation options. This would help determine if AIs can navigate to certain locations or not.

Next Section
5. Set Up Audio and Visual Effects
5. Set Up Audio and Visual Effects

Learn how to set up audio and visual effects to enhance gameplay.

5. Set Up Audio and Visual Effects
Learn how to set up audio and visual effects to enhance gameplay.

5. Set Up Audio and Visual Effects
This section will show you how to set up audio, like barks, and visual effects, like camera shakes, to create engaging gameplay.

Audio Player Device
You can use the Audio Player device to set use dialog lines from guards. In game development, these are often referred to as barks.

Barks
You can find imported audio in "Project folder" > Barks. Click the Play icon to hear the audio file, then drag and drop it onto your island.

Audio File
Dropping an audio file onto your island will place an Audio Player device, which is hooked up to a Verse device to play a series of customs guard callouts. These callouts react to different events, like spotting the player or taking damage.

Place one Audio Player for every unique piece of audio that you want to play. This tutorial uses 14 different barks, with 14 different Audio Player devices placed.

To set up these devices, customize the following settings:

Leash Audio
Option	Value	Explanation
Volume

4.0

This setting can vary depending on your recording.

Restart Audio when Activated

True

This audio will play from the beginning when activated.

Play on Hit

False

This device will not play audio when hit by a player.

Play Location

Instigating Player

Audio will be played based on the instigating player's loacation instead of the device location.

Enable Volume Attenuation

False

Changes the volume based on the distance from the device or guard set to play it. For this tutorial, the player can hear the audio no matter how far away they are.

Next, set up the Verse script to handle the logic for triggering the Audio Player devices during the game, then place the Verse device. For this tutorial, the device is named Stronghold Bark Manager.

Paste the following Verse script.

Verse
using { /Fortnite.com/Devices }
using { /Fortnite.com/Game }
using { /Fortnite.com/Characters }
using { /Verse.org/Random }
using { /Verse.org/Simulation }
using { /UnrealEngine.com/Temporary/Diagnostics }
using { /UnrealEngine.com/Temporary/SpatialMath }
# Audio bark that can be played on a NPC
audio_npc_bark := class<concrete>:
    # Audio device to play barks
    @editable
    BarkDevice:audio_player_device := audio_player_device{}
    # Option to allow NPCs to repeat the bark
    @editable
    CanRepeat:logic = true
    # Delay between the event and the beginning of the bark
    @editable
    Delay:float = 0.0
    # Delay before repeating this bark
    @editable
    Cooldown:float = 5.0
    # Bark name for logging
    @editable
    BarkID:string = "Missing ID"
    # Is the cooldown timer elapsed
    var<private> IsInCooldown:logic = false
    # Event to stop the bark
    StopBarkEvent<private>:event() = event(){}
    PlayBark(Agent:agent)<suspends>:void=
        var IsPlaying:logic = false;
        defer:
            if (IsPlaying?):
                set IsPlaying = false
                set IsInCooldown = false
                BarkDevice.Stop(Agent)
        race:
            block:
                StopBarkEvent.Await()
                return
            block:
                AwaitAgentDown(Agent)
                return
            block:
                if (Delay > 0.0):
                    Sleep(Delay)
                if (IsInCooldown?):
                    return
                BarkDevice.Play(Agent)
                set IsPlaying = true
                set IsInCooldown = true
                Sleep(2.0)
                set IsPlaying = false
        if (CanRepeat?):
            Sleep(Cooldown)
            set IsInCooldown = false
    StopBark():void=
        StopBarkEvent.Signal()
    AwaitAgentDown<private>(Agent:agent)<suspends>:void=
        if (Character := Agent.GetFortCharacter[]):
            loop:
                if (Character.GetHealth() <= 0.0):
                    return
                Character.DamagedEvent().Await()
# Script that handles barks from guards
stronghold_bark_manager := class(creative_device):
    # Reference to the Game Manager to monitor perception events
    @editable
    StrongholdGameManager:stronghold_game_manager := stronghold_game_manager{}
    # Audio Player Devices
    @editable
    BarkNPCDown:audio_npc_bark = audio_npc_bark{BarkID := "Man Down", Delay := 0.3}
    @editable
    BarkFallback:audio_npc_bark = audio_npc_bark{BarkID := "Fallback", CanRepeat := false, Delay := 3.0}
    @editable
    BarkNeedBackup:audio_npc_bark = audio_npc_bark{BarkID := "Need Backup", CanRepeat := false, Delay := 2.0}
    @editable
    BarkGoToLeash:audio_npc_bark = audio_npc_bark{BarkID := "Reinforcements En Route", CanRepeat := false, Delay := 4.0}
    @editable
    BarkDamageTaken:audio_npc_bark = audio_npc_bark{BarkID := "Took Damage", Delay := 0.2}
    @editable
    BarkDamagePlayer:audio_npc_bark = audio_npc_bark{BarkID := "Hit Player", Delay := 0.2}
    @editable
    BarkEliminatedPlayer:audio_npc_bark = audio_npc_bark{BarkID := "Eliminated Player", Delay := 0.3}
    @editable
    BarkPlayerSpotted:audio_npc_bark = audio_npc_bark{BarkID := "Spotted Player", CanRepeat := false}
    @editable
    BarkPlayerLost:audio_npc_bark = audio_npc_bark{BarkID := "Lost Player", Cooldown := 10.0}
    @editable
    BarkGuardSuspicious:audio_npc_bark = audio_npc_bark{BarkID := "Suspicious", Cooldown := 10.0}
    @editable
    BarkGuardUnaware:audio_npc_bark = audio_npc_bark{BarkID := "Unaware", Cooldown := 10.0}
    # Variable to store if guards were looking for targets
    var<private> HasLostTarget:logic := false
    # Runs when the device is started in a running game
    OnBegin<override>()<suspends>:void=
        ConfigureBarks()
        sync:
            AwaitReinforcements()
            AwaitFallback()
            PlayAwarenessBarks()
    PlayBark(Bark:audio_npc_bark, Guard:agent):void=
        spawn {Bark.PlayBark(Guard)}
    # Play a bark when reinforcement is called
    AwaitReinforcements<private>()<suspends>:void=
        AlertedGuard := StrongholdGameManager.ReinforcementsCalledEvent.Await()
        PlayBark(BarkNeedBackup, AlertedGuard)
    # Play a bark when guards regroup in the stronghold
    AwaitFallback<private>()<suspends>:void=
        StrongholdGameManager.FallbackEvent.Await()
        if:
            Guard := StrongholdGameManager.AlertedGuards[0]
        then:
            PlayBark(BarkFallback, Guard)
    PlayAwarenessBarks<private>()<suspends>:void=
        loop:
            race:
                PlayGuardsSuspiciousBark()
                PlayPlayerSpottedBark()
                PlayPlayerLostBark()
                PlayGuardsUnawareBark()
    PlayPlayerSpottedBark<private>()<suspends>:void=
        Guard:=StrongholdGameManager.PlayerDetectedEvent.Await();
        set HasLostTarget = false
        PlayBark(BarkPlayerSpotted, Guard)
    PlayPlayerLostBark<private>()<suspends>:void=
        Guard:=StrongholdGameManager.PlayerLostEvent.Await();
        set HasLostTarget = true
        PlayBark(BarkPlayerLost, Guard)
    PlayGuardsSuspiciousBark<private>()<suspends>:void=
        Guard:=StrongholdGameManager.GuardsSuspiciousEvent.Await();
        PlayBark(BarkGuardSuspicious, Guard)
    PlayGuardsUnawareBark<private>()<suspends>:void=
        Guard:=StrongholdGameManager.GuardsUnawareEvent.Await();
        if (HasLostTarget?):
            set HasLostTarget = false
            if (not StrongholdGameManager.FallbackTriggered?):
                PlayBark(BarkGuardUnaware, Guard)
    SubscribeToGuardSpawnerEvents(GuardSpawnerDevice:guard_spawner_device):void =
        GuardSpawnerDevice.DamagedEvent.Subscribe(OnGuardDamaged)
        GuardSpawnerDevice.EliminatedEvent.Subscribe(OnGuardEliminated)
        GuardSpawnerDevice.EliminatingEvent.Subscribe(OnPlayerEliminated)
     # Configure all barks
    ConfigureBarks():void=
        # Subscribe To Player Damage Event
        AllPlayers := GetPlayspace().GetPlayers()
        for (StrongholdPlayer : AllPlayers, StrongholdPC := StrongholdPlayer.GetFortCharacter[]):
            StrongholdPC.DamagedEvent().Subscribe(OnPlayerDamaged)
        # Run through guards spawner list from stronghold manager and subscribe to all key events
        for (GuardSpawner : StrongholdGameManager.GuardsInitialSpawners):
            SubscribeToGuardSpawnerEvents(GuardSpawner)
        for (GuardSpawner : StrongholdGameManager.GuardsReinforcementSpawners):
            SubscribeToGuardSpawnerEvents(GuardSpawner)
        # Have a separate case for when the reinforcements spawn
        if:
            FirstReinforcementSpawner := StrongholdGameManager.GuardsReinforcementSpawners[0]
        then:
            FirstReinforcementSpawner.SpawnedEvent.Subscribe(HandleReinforcementSpawned)
      # Guard is down, try to play a bark on the closest alerted guard
    OnGuardEliminated(InteractionResult:device_ai_interaction_result):void=
        if (EliminatedGuard := InteractionResult.Target?):
            # Find closest alive guard to play this bark
            var ClosestGuard:?agent = false
            if:
                set ClosestGuard = option{StrongholdGameManager.AlertedGuards[0]}
                EliminatedGuardCharacter := EliminatedGuard.GetFortCharacter[]
            then:
                for (AlertedGuard : StrongholdGameManager.AlertedGuards, AlertedGuardCharacter := AlertedGuard.GetFortCharacter[]):
                    if:
                        not ClosestGuard? = AlertedGuard
                        ClosestGuardCharacter := ClosestGuard?.GetFortCharacter[]
                        DistanceSquaredToAlertedGuard := DistanceSquared(AlertedGuardCharacter.GetTransform().Translation, EliminatedGuardCharacter.GetTransform().Translation)
                        DistanceSquaredToClosestGuard := DistanceSquared(ClosestGuardCharacter.GetTransform().Translation, EliminatedGuardCharacter.GetTransform().Translation)
                        DistanceSquaredToAlertedGuard < DistanceSquaredToClosestGuard
                    then:
                        set ClosestGuard = option{AlertedGuard}
            if (Guard := ClosestGuard?):
                spawn {BarkNPCDown.PlayBark(Guard)}
   # Guard is hit, try to play a bark if the guard is not down
    OnGuardDamaged(InteractionResult:device_ai_interaction_result):void=
        if (Guard := InteractionResult.Target?):
            spawn {BarkDamageTaken.PlayBark(Guard)}
    # Player is hit, try to play a bark on the guard that damaged the player
    OnPlayerDamaged(DamageResult:damage_result):void=
        if:
            fort_character[DamageResult.Target].GetHealth() > 0.0
            Guard := DamageResult.Instigator?.GetInstigatorAgent[]
        then:
            spawn {BarkDamagePlayer.PlayBark(Guard)}
    # Player is down, try to play a bark on the guard that eliminated the player
    OnPlayerEliminated(InteractionResult:device_ai_interaction_result):void=
        if (Guard := InteractionResult.Source?):
            spawn {BarkEliminatedPlayer.PlayBark(Guard)}
    HandleReinforcementSpawned(Guard:agent):void=
        spawn {BarkGoToLeash.PlayBark(Guard)}
using { /Fortnite.com/Devices } using { /Fortnite.com/Game } using { /Fortnite.com/Characters } using { /Verse.org/Random } using { /Verse.org/Simulation } using { /UnrealEngine.com/Temporary/Diagnostics } using { /UnrealEngine.com/Temporary/SpatialMath } # Audio bark that can be played on a NPC audio_npc_bark := class<concrete>: # Audio device to play barks @editable BarkDevice:audio_player_device := audio_player_device{} # Option to allow NPCs to repeat the bark @editable CanRepeat:logic = true # Delay between the event and the beginning of the bark @editable Delay:float = 0.0 # Delay before repeating this bark @editable Cooldown:float = 5.0 # Bark name for logging @editable BarkID:string = "Missing ID" # Is the cooldown timer elapsed var<private> IsInCooldown:logic = false # Event to stop the bark StopBarkEvent<private>:event() = event(){} PlayBark(Agent:agent)<suspends>:void= var IsPlaying:logic = false; defer: if (IsPlaying?): set IsPlaying = false set IsInCooldown = false BarkDevice.Stop(Agent) race: block: StopBarkEvent.Await() return block: AwaitAgentDown(Agent) return block: if (Delay > 0.0): Sleep(Delay) if (IsInCooldown?): return BarkDevice.Play(Agent) set IsPlaying = true set IsInCooldown = true Sleep(2.0) set IsPlaying = false if (CanRepeat?): Sleep(Cooldown) set IsInCooldown = false StopBark():void= StopBarkEvent.Signal() AwaitAgentDown<private>(Agent:agent)<suspends>:void= if (Character := Agent.GetFortCharacter[]): loop: if (Character.GetHealth() <= 0.0): return Character.DamagedEvent().Await() # Script that handles barks from guards stronghold_bark_manager := class(creative_device): # Reference to the Game Manager to monitor perception events @editable StrongholdGameManager:stronghold_game_manager := stronghold_game_manager{} # Audio Player Devices @editable BarkNPCDown:audio_npc_bark = audio_npc_bark{BarkID := "Man Down", Delay := 0.3} @editable BarkFallback:audio_npc_bark = audio_npc_bark{BarkID := "Fallback", CanRepeat := false, Delay := 3.0} @editable BarkNeedBackup:audio_npc_bark = audio_npc_bark{BarkID := "Need Backup", CanRepeat := false, Delay := 2.0} @editable BarkGoToLeash:audio_npc_bark = audio_npc_bark{BarkID := "Reinforcements En Route", CanRepeat := false, Delay := 4.0} @editable BarkDamageTaken:audio_npc_bark = audio_npc_bark{BarkID := "Took Damage", Delay := 0.2} @editable BarkDamagePlayer:audio_npc_bark = audio_npc_bark{BarkID := "Hit Player", Delay := 0.2} @editable BarkEliminatedPlayer:audio_npc_bark = audio_npc_bark{BarkID := "Eliminated Player", Delay := 0.3} @editable BarkPlayerSpotted:audio_npc_bark = audio_npc_bark{BarkID := "Spotted Player", CanRepeat := false} @editable BarkPlayerLost:audio_npc_bark = audio_npc_bark{BarkID := "Lost Player", Cooldown := 10.0} @editable BarkGuardSuspicious:audio_npc_bark = audio_npc_bark{BarkID := "Suspicious", Cooldown := 10.0} @editable BarkGuardUnaware:audio_npc_bark = audio_npc_bark{BarkID := "Unaware", Cooldown := 10.0} # Variable to store if guards were looking for targets var<private> HasLostTarget:logic := false # Runs when the device is started in a running game OnBegin<override>()<suspends>:void= ConfigureBarks() sync: AwaitReinforcements() AwaitFallback() PlayAwarenessBarks() PlayBark(Bark:audio_npc_bark, Guard:agent):void= spawn {Bark.PlayBark(Guard)} # Play a bark when reinforcement is called AwaitReinforcements<private>()<suspends>:void= AlertedGuard := StrongholdGameManager.ReinforcementsCalledEvent.Await() PlayBark(BarkNeedBackup, AlertedGuard) # Play a bark when guards regroup in the stronghold AwaitFallback<private>()<suspends>:void= StrongholdGameManager.FallbackEvent.Await() if: Guard := StrongholdGameManager.AlertedGuards[0] then: PlayBark(BarkFallback, Guard) PlayAwarenessBarks<private>()<suspends>:void= loop: race: PlayGuardsSuspiciousBark() PlayPlayerSpottedBark() PlayPlayerLostBark() PlayGuardsUnawareBark() PlayPlayerSpottedBark<private>()<suspends>:void= Guard:=StrongholdGameManager.PlayerDetectedEvent.Await(); set HasLostTarget = false PlayBark(BarkPlayerSpotted, Guard) PlayPlayerLostBark<private>()<suspends>:void= Guard:=StrongholdGameManager.PlayerLostEvent.Await(); set HasLostTarget = true PlayBark(BarkPlayerLost, Guard) PlayGuardsSuspiciousBark<private>()<suspends>:void= Guard:=StrongholdGameManager.GuardsSuspiciousEvent.Await(); PlayBark(BarkGuardSuspicious, Guard) PlayGuardsUnawareBark<private>()<suspends>:void= Guard:=StrongholdGameManager.GuardsUnawareEvent.Await(); if (HasLostTarget?): set HasLostTarget = false if (not StrongholdGameManager.FallbackTriggered?): PlayBark(BarkGuardUnaware, Guard) SubscribeToGuardSpawnerEvents(GuardSpawnerDevice:guard_spawner_device):void = GuardSpawnerDevice.DamagedEvent.Subscribe(OnGuardDamaged) GuardSpawnerDevice.EliminatedEvent.Subscribe(OnGuardEliminated) GuardSpawnerDevice.EliminatingEvent.Subscribe(OnPlayerEliminated) # Configure all barks ConfigureBarks():void= # Subscribe To Player Damage Event AllPlayers := GetPlayspace().GetPlayers() for (StrongholdPlayer : AllPlayers, StrongholdPC := StrongholdPlayer.GetFortCharacter[]): StrongholdPC.DamagedEvent().Subscribe(OnPlayerDamaged) # Run through guards spawner list from stronghold manager and subscribe to all key events for (GuardSpawner : StrongholdGameManager.GuardsInitialSpawners): SubscribeToGuardSpawnerEvents(GuardSpawner) for (GuardSpawner : StrongholdGameManager.GuardsReinforcementSpawners): SubscribeToGuardSpawnerEvents(GuardSpawner) # Have a separate case for when the reinforcements spawn if: FirstReinforcementSpawner := StrongholdGameManager.GuardsReinforcementSpawners[0] then: FirstReinforcementSpawner.SpawnedEvent.Subscribe(HandleReinforcementSpawned) # Guard is down, try to play a bark on the closest alerted guard OnGuardEliminated(InteractionResult:device_ai_interaction_result):void= if (EliminatedGuard := InteractionResult.Target?): # Find closest alive guard to play this bark var ClosestGuard:?agent = false if: set ClosestGuard = option{StrongholdGameManager.AlertedGuards[0]} EliminatedGuardCharacter := EliminatedGuard.GetFortCharacter[] then: for (AlertedGuard : StrongholdGameManager.AlertedGuards, AlertedGuardCharacter := AlertedGuard.GetFortCharacter[]): if: not ClosestGuard? = AlertedGuard ClosestGuardCharacter := ClosestGuard?.GetFortCharacter[] DistanceSquaredToAlertedGuard := DistanceSquared(AlertedGuardCharacter.GetTransform().Translation, EliminatedGuardCharacter.GetTransform().Translation) DistanceSquaredToClosestGuard := DistanceSquared(ClosestGuardCharacter.GetTransform().Translation, EliminatedGuardCharacter.GetTransform().Translation) DistanceSquaredToAlertedGuard < DistanceSquaredToClosestGuard then: set ClosestGuard = option{AlertedGuard} if (Guard := ClosestGuard?): spawn {BarkNPCDown.PlayBark(Guard)} # Guard is hit, try to play a bark if the guard is not down OnGuardDamaged(InteractionResult:device_ai_interaction_result):void= if (Guard := InteractionResult.Target?): spawn {BarkDamageTaken.PlayBark(Guard)} # Player is hit, try to play a bark on the guard that damaged the player OnPlayerDamaged(DamageResult:damage_result):void= if: fort_character[DamageResult.Target].GetHealth() > 0.0 Guard := DamageResult.Instigator?.GetInstigatorAgent[] then: spawn {BarkDamagePlayer.PlayBark(Guard)} # Player is down, try to play a bark on the guard that eliminated the player OnPlayerEliminated(InteractionResult:device_ai_interaction_result):void= if (Guard := InteractionResult.Source?): spawn {BarkEliminatedPlayer.PlayBark(Guard)} HandleReinforcementSpawned(Guard:agent):void= spawn {BarkGoToLeash.PlayBark(Guard)}
This script stores a reference to each Audio Player device and references the Stronghold Game Manager Verse device as a conduit for its references to the Guard Spawners.

Customizable Lights
Customizable Lights
In addition to getting audio feedback from AI guards, you can also give players visual feedback from the environment.

This tutorial uses two sets of Customizable Light devices around the stronghold. A red light indicates a detected status while an orange light indicates an alerted status.

To set up these devices, customize the following settings:

Option	Value	Explanation
Initial State

False

Determines the light’s initial state when the device is enabled.

Light Size

100.00

Determines the size, range, and amplitude of the of the light flare.

Cast Shadows

True

Allows the light to cast shadows.

Enabled During Phase

Gameplay Only

Lights will only be enabled during the gameplay.

Light Intensity

30.0

Determines the intensity of the light.

Rhythm Time

x8

Determines the time multiplier for the Rhythm Preset.

Dimming Amount

100.0

Determines the amount to dim the light when using the channel controls.

Dimming Time

0.1

Determines the dimming transition duration in seconds.

VFX Creator
vfxCreator
This tutorial also uses a VFX Creator device at the top of the base to act as a signal flare for reinforcements when players are first detected. This flare is controlled by the Verse device and will go off along with the corner lights when guards are alerted to make their states visually clear.

To set up these devices, customize the following settings:

VFX Settings
Option	Value	Explanation
Start Effects When Enabled

False

Determines whether the device will execute the effects when enabled.

Sprite Size

2.0

Sets the Effect Sprite initial size.

Sprite Duration

5.0

Sets how much time each sprite will appear.

Main Color

Red

Sets the main color for the effects.

Main Color Brightness

200.0

Sets the Main Color brightness.

Sprite Speed

100.0

Sets how fast the effects sprites start to move.

Effect Gravity

15.0

Sets how fast the effect sprites can fall.

Randomness

100.0

Determines how random the movement will be and adds variation to size.

Keep Size

False

Determines whether sprites keep its size or use a custom size that changes over time.

Effect Generation Amount

4.0

Sets how many effect sprites are generated.

Spawn Zone Shape

Point

Determines the space shape where the sprites initially appear.

Spawn Zone Size

0.05

Sets the size of the spawn shape in tiles.

Enabled During Phase

Gameplay Only

Determines the game phases during which the device will be enabled.

Loop

Never

Determines if the effect plays once, loops forever, or by a custom amount of times.

Radio Device
This tutorial uses two Radio devices, one for high-alert combat music and the other for cautious music.

The tense player music uses: Radio > Music Loops > Music_StW_Low_Combat01_Cue'.

The player-spotted combat music uses the Radio > Music Loops > Music_StW_High_Combat01_Cue'.

Set up a Verse script that you can call Stronghold_Alert_Manager to listen when a guard has detected the player, or when all guards have lost track of the player to alternate between the two states in the stronghold.

Paste the following Verse script.

Verse
using { /Verse.org/Simulation }
using { /Verse.org/Simulation/Tags }
using { /Verse.org/Colors }
using { /UnrealEngine.com/Temporary/Diagnostics }
using { /Fortnite.com/Devices }
# tags for customizable lights
alerted_lights_tag := class(tag){}
combat_lights_tag := class(tag){}
# Script that handles music and turn on lights when guards are alerted
stronghold_alert_manager := class(creative_device):
    # Reference to the Game Manager to monitor perception events
    @editable
    StrongholdGameManager:stronghold_game_manager := stronghold_game_manager{}
    # Reference to Radio that plays combat music
    @editable
    RadioCombat:radio_device := radio_device{}
    # Reference to Radio that plays alerted music
    @editable
    RadioAlerted:radio_device := radio_device{}
    # VFX to play when alarm/flare is shot
    @editable
    FlareAlarmVFXCreator:vfx_creator_device := vfx_creator_device{}
  # Class Data
    var<private> CustomizableLightDevicesAlerted: []customizable_light_device = array{}
    var<private> CustomizableLightDevicesCombat: []customizable_light_device = array{}
  # Change the camp to alerted when player is lost / killed
    WaitForAlerted()<suspends>:void=
        # do not go back to alerted after fallback
        if (StrongholdGameManager.FallbackTriggered?):
            Sleep(Inf)
        StrongholdGameManager.GuardsUnawareEvent.Await()
        Sleep(3.0)
        SetAlertedMood()
    # Change the camp to combat when player is spotted
    WaitForCombat()<suspends>:void=
        race:
            StrongholdGameManager.PlayerDetectedEvent.Await()
            StrongholdGameManager.FallbackEvent.Await()
        Sleep(2.0)
        SetCombatMood()
    # Runs when the device is started in a running game
    OnBegin<override>()<suspends>:void=
        FindLightsWithTag()
        MonitorStrongholdAlertStatus()
    # Main Loop checking if stronghold is in combat or alerted
    MonitorStrongholdAlertStatus()<suspends>:void=
        loop:
            WaitForCombat()
            WaitForAlerted()
     # Sets Base to Combat by toggling lights red and playing high intensity music
    SetCombatMood():void=
        # Loop through Combat Lights and turn them on
        for(LightsToTurnOn: CustomizableLightDevicesCombat):
            LightsToTurnOn.TurnOn()
        # Loop through Alert Lights and turn them off
        for(LightsToTurnOff: CustomizableLightDevicesAlerted):
            LightsToTurnOff.TurnOff()
        # Turn on combat audio and turn off alerted audio
        RadioCombat.Play()
        RadioAlerted.Stop()
        FlareAlarmVFXCreator.Toggle()
    # Sets Base to Alerted by toggling lights yellow and playing  tense music
    SetAlertedMood():void=
        for(LightsToTurnOn: CustomizableLightDevicesAlerted):
            LightsToTurnOn.TurnOn()
        for(LightsToTurnOff: CustomizableLightDevicesCombat):
            LightsToTurnOff.TurnOff()
        RadioCombat.Stop()
        RadioAlerted.Play()
    # Loops through creative devices for the lights with this specific Verse tag and saves them to a list
    FindLightsWithTag() : void=
        TaggedAlertedLightDevices := GetCreativeObjectsWithTag(alerted_lights_tag{})
        TaggedCombatLightDevices := GetCreativeObjectsWithTag(combat_lights_tag{})
        for(AlertedLight : TaggedAlertedLightDevices, CustomizableLight := customizable_light_device[AlertedLight] ):
            CustomizableLight.TurnOff()
            set CustomizableLightDevicesAlerted += array{CustomizableLight}
        for(CombatLight : TaggedCombatLightDevices, CustomizableLight := customizable_light_device[CombatLight] ):
            CustomizableLight.TurnOff()
            set CustomizableLightDevicesCombat += array{CustomizableLight}
using { /Verse.org/Simulation } using { /Verse.org/Simulation/Tags } using { /Verse.org/Colors } using { /UnrealEngine.com/Temporary/Diagnostics } using { /Fortnite.com/Devices } # tags for customizable lights alerted_lights_tag := class(tag){} combat_lights_tag := class(tag){} # Script that handles music and turn on lights when guards are alerted stronghold_alert_manager := class(creative_device): # Reference to the Game Manager to monitor perception events @editable StrongholdGameManager:stronghold_game_manager := stronghold_game_manager{} # Reference to Radio that plays combat music @editable RadioCombat:radio_device := radio_device{} # Reference to Radio that plays alerted music @editable RadioAlerted:radio_device := radio_device{} # VFX to play when alarm/flare is shot @editable FlareAlarmVFXCreator:vfx_creator_device := vfx_creator_device{} # Class Data var<private> CustomizableLightDevicesAlerted: []customizable_light_device = array{} var<private> CustomizableLightDevicesCombat: []customizable_light_device = array{} # Change the camp to alerted when player is lost / killed WaitForAlerted()<suspends>:void= # do not go back to alerted after fallback if (StrongholdGameManager.FallbackTriggered?): Sleep(Inf) StrongholdGameManager.GuardsUnawareEvent.Await() Sleep(3.0) SetAlertedMood() # Change the camp to combat when player is spotted WaitForCombat()<suspends>:void= race: StrongholdGameManager.PlayerDetectedEvent.Await() StrongholdGameManager.FallbackEvent.Await() Sleep(2.0) SetCombatMood() # Runs when the device is started in a running game OnBegin<override>()<suspends>:void= FindLightsWithTag() MonitorStrongholdAlertStatus() # Main Loop checking if stronghold is in combat or alerted MonitorStrongholdAlertStatus()<suspends>:void= loop: WaitForCombat() WaitForAlerted() # Sets Base to Combat by toggling lights red and playing high intensity music SetCombatMood():void= # Loop through Combat Lights and turn them on for(LightsToTurnOn: CustomizableLightDevicesCombat): LightsToTurnOn.TurnOn() # Loop through Alert Lights and turn them off for(LightsToTurnOff: CustomizableLightDevicesAlerted): LightsToTurnOff.TurnOff() # Turn on combat audio and turn off alerted audio RadioCombat.Play() RadioAlerted.Stop() FlareAlarmVFXCreator.Toggle() # Sets Base to Alerted by toggling lights yellow and playing tense music SetAlertedMood():void= for(LightsToTurnOn: CustomizableLightDevicesAlerted): LightsToTurnOn.TurnOn() for(LightsToTurnOff: CustomizableLightDevicesCombat): LightsToTurnOff.TurnOff() RadioCombat.Stop() RadioAlerted.Play() # Loops through creative devices for the lights with this specific Verse tag and saves them to a list FindLightsWithTag() : void= TaggedAlertedLightDevices := GetCreativeObjectsWithTag(alerted_lights_tag{}) TaggedCombatLightDevices := GetCreativeObjectsWithTag(combat_lights_tag{}) for(AlertedLight : TaggedAlertedLightDevices, CustomizableLight := customizable_light_device[AlertedLight] ): CustomizableLight.TurnOff() set CustomizableLightDevicesAlerted += array{CustomizableLight} for(CombatLight : TaggedCombatLightDevices, CustomizableLight := customizable_light_device[CombatLight] ): CustomizableLight.TurnOff() set CustomizableLightDevicesCombat += array{CustomizableLight}

Understanding NPC Behaviors
Learn about NPC Behavior and States and how NPCs use them for decision-making

Understanding NPC Behaviors
Non-player character (NPC) behaviors play a critical role in many games. From companions to bosses, merchants to guards, how NPCs interact with the world around them drives engaging, immersive gameplay. At first glance, these behaviors may seem intimidating, but in reality, most NPCs follow a strict set of logical rules. Understanding these rules is key when creating NPCs, and on this page, you’ll learn about how NPCs interact with the world, and how you can visualize and manipulate their behaviors to create your own unique experiences.

The NPC Spawner Device facilitates a lot of NPC and AI interactions. To learn more about the device see, NPC Spawner Device, NPC Character Definition, Create Custom NPC Behavior page, and Using the NPC Spawner with Animations.

Logic Rules
Most NPCs do not act randomly, and choose their next action based on their state. You can understand an NPC’s state as a snapshot of the NPC’s world at a particular moment. The actions the NPC is taking, the actions players are taking, and any other variables the NPC might know about all make up the NPC’s state. NPCs use logical rules to decide when to transition from state to state and may have many different rules depending on their current state.

Finite-State Machines
A common way to visualize states is through a Finite-State Machine (FSM). A finite-state machine describes the different states an NPC can be in and the transitions it makes from state to state. Nodes represent the different states, and the arrows between them describe the conditions needed to transition from one state to the next. A basic FSM diagram might look like this:

Basic FSM
Here the FSM has three states and starts in State 1. Once specific conditions are reached the NPC jumps from one state to the next, and continues jumping states as conditions change.

For instance, consider the FSM for a simple battle medic character. If there are injured teammates nearby, the medic heals teammates. If there are enemies nearby, the medic attacks enemies. Otherwise, it stands idle. A basic FSM for this character might look like the following:

Basic Medic FSM
FSMs help you visualize and understand the way characters work, and help you map out the ways characters respond to events and the world around them.

Guard Example Finite-State Machine
For an in-game example, let’s look at the guard NPC. Guard NPCs can be either spawned from the guard spawner device or created with a guard-type NPC Character Definition. A guard-type NPC follows a particular set of logic rules, which correspond to the different active states the guard can be in:

Idle

Patrolling

Suspicious

Alert

Attacking

When a guard spawns, it either begins idle or starts patrolling if the patrol option is enabled. When the guard detects a target, it begins to fill the suspicion meter. If the meter is filled, the guard enters the alert phase, otherwise, it returns to patrolling. While alert, the guard will continuously navigate to their target, attacking them if they’re in range. If the target is eliminated or escapes the guard, the guard will return to patrolling. You can visualize the guard’s logic with the following FSM:

Guard FSM
This FSM provides a high-level overview of guard behavior, but there may be many more rules and actions a guard take. NPCs may be acting on multiple things at once, and it’s important to consider environmental factors as you add them to your experiences.

NPC States and Verse
NPCs in UEFN inherit from the AI module and expose functions you can use to directly control their state. For instance, the navigatable interface lets you navigate an NPC to an area, while the focus_interface lets you force a character to focus on a particular object or agent. By using these interfaces within either Verse Devices or NPC Behaviors, you can create custom NPCs to populate your experiences.

For more information on creating your own NPC Behaviors, check out the Create Custom NPC Behavior page.

For instance, consider the following NPC Behavior:

Verse
using { /Fortnite.com/AI }
using { /Fortnite.com/Characters }
using { /Fortnite.com/Game }
using { /Verse.org/Simulation }
 
on_damaged_behavior<public> := class(npc_behavior):
 
    # This function runs when the NPC is spawned in the world and ready to follow a behavior.
    OnBegin<override>()<suspends>:void=
        if:
            Agent := GetAgent[]
            FortCharacter := Agent.GetFortCharacter[]
        then:
            # Subscribe the character's damaged event to OnDamaged
            FortCharacter.DamagedEvent().Subscribe(OnDamaged)
 
    # When the NPC is damaged, start chasing the character
    # that instigated the damage
    OnDamaged(DamageResult:damage_result):void=
        Instigator := DamageResult.Instigator
        if:
            # Get the Agent and the Navigatable interface
            Agent := GetAgent[]
 
            Character := Agent.GetFortCharacter[]
            Navigatable := Character.GetNavigatable[]
 
            # Get the agent that instigated the damage
            InstigatingAgent := agent[Instigator?]
 
        then:
            # Start navigating to the InstigatingAgent
            NavigationTarget := MakeNavigationTarget(InstigatingAgent)
            spawn{Navigatable.NavigateTo(NavigationTarget)}
using { /Fortnite.com/AI } using { /Fortnite.com/Characters } using { /Fortnite.com/Game } using { /Verse.org/Simulation } on_damaged_behavior<public> := class(npc_behavior): # This function runs when the NPC is spawned in the world and ready to follow a behavior. OnBegin<override>()<suspends>:void= if: Agent := GetAgent[] FortCharacter := Agent.GetFortCharacter[] then: # Subscribe the character's damaged event to OnDamaged FortCharacter.DamagedEvent().Subscribe(OnDamaged) # When the NPC is damaged, start chasing the character # that instigated the damage OnDamaged(DamageResult:damage_result):void= Instigator := DamageResult.Instigator if: # Get the Agent and the Navigatable interface Agent := GetAgent[] Character := Agent.GetFortCharacter[] Navigatable := Character.GetNavigatable[] # Get the agent that instigated the damage InstigatingAgent := agent[Instigator?] then: # Start navigating to the InstigatingAgent NavigationTarget := MakeNavigationTarget(InstigatingAgent) spawn{Navigatable.NavigateTo(NavigationTarget)}
All NPCs implement the damageable interface, which allows them to take damage. Subscribing a function to the damageable interface’s DamagedEvent lets you know when your NPC is damaged, and lets you run code in response. In the above script, when an NPC that implements this behavior is damaged, it will get the agent that damaged it and store it in a variable InstigatingAgent. Then, using the NPC’s navigatable interface, it will set the instigator as a NavigationTarget and chase it down.

This behavior is an extension of the NPC’s original behavior. If this script is attached to guard-type character, they will still perform all their regular guard behaviors, but when damaged will navigate directly to their target. The same applies to wildlife and custom-type characters. NPC behavior scripts are a powerful tool to extend NPC functionality and allow you to create your own custom NPCs to fit your experiences. For more information on creating your own custom NPC behavior scripts, see Create Custom NPC Behavior.

NPC Types
Different types of NPCs implement different base behaviors, and custom NPCs you create from these NPC types will inherit these behaviors. For more information on the different base types of NPCs and their associated behaviors, see NPC Types.

Navigating in World
When navigating the world, NPCs have to make choices about the best route to take to get to their destination. Does the guard mantle over a wall, or smash through it? Should it swim through water, or go around it? NPCs make these decisions based on the world’s navigation mesh. NPCs use the navigation mesh to make pathfinding decisions and update their choices as the world updates around them. For more information on using and visualizing the navigation mesh, see the Navigation Mesh page.

NPC Spawner Devices
Use NPCs to engage with players and liven your gameplay.

NPC Spawner Devices
This feature is in Beta. You can publish an island with this feature, but be aware that changes may break your island and may require your active intervention.

With the NPC Spawner device, you can create unique creatures, enemies, and more with engaging roles that bring your gameplay to life. These non-playable characters (NPCs) can have health, patrol set paths, and even aid players in solving puzzles. Use this device to assign scripts and NPC Character Definitions  that you can reuse across multiple NPC Spawner devices.

Include NPCs, characters with artificial intelligence (AI), in your gameplay to add an extra layer of immersion. You can customize NPCs to perform various actions, from reviving teammates to following players.

NPC Spawner in UEFN
The NPC Spawner is different from the Character device,  in that you can make custom configurations that alter how a character looks, moves, and behaves with the NPC Spawner.

The Character device, like the Guard Spawner device, is useful for a singular instance of a basic character. However, both are limited to Fortnite outfits. The NPC Spawner device can create instances of characters with either Fortnite uniform guards, wildlife, or custom NPCs with user-imported meshes'.

This is currently an Unreal Editor for Fortnite (UEFN) only device located in All > Fortnite > Devices > !Beta > NPC Spawner. limited to Fortnite outfits.

Using Brand Specific NPCs
Custom-branded NPCs are available in the NPC Spawner through a character definition. 

Depending on the IP, you can find the unique NPCs in one or both of the following: 

The NPC Character Type which can include unique modifiers.

Through the Cosmetic Modifier when selecting a Custom or Guard character type.

Branded assets have specific rules and guidelines for use. Check the brand rules for the IP assets you intend to use. To learn more about the various brand partners and content, see Game Collections.   

You can only use brand assets in a project specific to the relevant IP property.

Contextual Filtering
Some devices are affected by a feature called contextual filtering. This feature highlights or shades options depending on the values selected for certain related options. This feature reduces clutter in the Details panel and makes options easier to manage and navigate.

User Options
User Options
With the User Options settings, you can set the spawn conditions, reference character definitions, and designate functions and events.

The default values are bold. Values that trigger contextual filtering are in italics.

Option	Value	Description
Spawn Count

1, Type an amount

Sets the number of NPCs this spawner can have active at any time. When the spawner activates, it produces one NPC at a time.

Spawn Through Walls

True, False

Determines whether NPC must spawn within line-of-sight of the spawner or if they can spawn behind obstructing walls.

Spawn Character at Game Start

True, False

Determines whether the spawner is already enabled when the game starts to spawn NPC characters. Set this to False to have an animated character.

NPC Behavior Script Override

None, Select a script

Overrides the default or assigned behavior of the NPC Character Definition assigned to this device.

NPC Character Definition

None, Select a Character Definition

Sets the character definition for spawning NPCs of a specific character type. Select from an existing character definition or create a new one from the dropdown.

If you drag an NPC Character Definition into the viewport, this field is automatically populated. 

Additional NPC Character Modifiers

Add an Array element

Adds an extra list of modifiers to apply to the NPC. The character type you select in the character definition affects the available list of modifiers.  

To add a modifier, click the plus icon, and then select from the Index dropdown. Additional options for the modifier become available. Modifiers you assign to the device overrides modifiers you assigned in the Character Definition. Visit the NPC Character Definitions documentation to learn more  about modifiers.  

Allow Infinite Spawn

True, False

Determines whether the spawner has a total spawn limit or not.

Total Spawn Limit

1, Type an amount

sets the maximum number of AIs this spawner can produce during its lifetime.

Spawn On Timer

True, False

Determines whether the AI is spawned on the Spawn Timer countdown or spawned on events.

Spawn Timer

3.0s, Type an amount

Sets the minimum time between spawning AIs.

Show Spawn Radius

True, False

Determines if the spawn radius will be shown or not.

Spawn Radius

1.0m, Type an amount

Sets the maximum distance from the device that AI can spawn.

Despawn AIs When Disabled

True, False

When the device is disabled, this determines whether AIs remain spawn or despawn.

Direct Event Binding
Following are the direct event binding options for this device.

Functions
A function listens for an event on a device and then performs an action.

For any function, click the option, then Select Device to access and select from the Device dropdown menu.

Once you've selected a device, click Select Event to bind the device to an event that will trigger the function for the device.

If more than one device or event triggers a function, press the Add button to add a line and repeat these steps.

Option	Description
Enable

Enables this device when an event occurs.

Disable

Disables this device when an event occurs.

Spawn

Spawns AI on this device when an event occurs.

Despawn

Despawns AI on this device when an event occurs.

Reset Total Spawn Count

Resets the count for the Total Spawn Limit when an event occurs.

Events
Direct event binding uses events as transmitters. An event tells another device to perform a function.

For any event option, click the option, then Select Device to access and select from the Device dropdown menu.

Once you've selected a device, click Select Function to bind the timer to a function for that device.

If more than one function is triggered by the event, press the Add button and repeat.

Option	Description
On Spawned

Sends an event to a linked device when a player interacts with the button.

On Eliminated

Sends an event to a linked device when a player interacts with the button.

Using The NPC Spawner in Verse
You can use the code below to control an NPC Spawner device in Verse. This code uses all features of the NPC Spawner device API. Modify it to fit the needs of your experience.

Verse
using { /Fortnite.com/AI }
using { /Fortnite.com/Characters }
using { /Fortnite.com/Devices }
using { /Verse.org/Simulation }
using { /UnrealEngine.com/Temporary/Diagnostics }
 
 
# Visit [here](https://dev.epicgames.com/documentation/en-us/uefn/create-your-own-device-in-verse) to create a verse device.
 
 
# A Verse-authored creative device that can be placed in a level
npc_spawner_device_example := class(creative_device):
 
 
    # Reference to the NPC Spawner Device in the level.
    # In the Details panel for this Verse device,
    # set this property to your NPC Spawner Device.
    @editable
    MyNPCSpawnerDevice:npc_spawner_device = npc_spawner_device{}
 
 
    # Runs when the device is started in a running game.
    OnBegin<override>()<suspends>:void=
 
 
        # Example for subscribing to an event on the Creative device.
        # Signaled when a character is spawned from the NPC Spawner Device.
        # Sends the `agent` character who was spawned.
        MyNPCSpawnerDevice.SpawnedEvent.Subscribe(OnCharacterSpawned)
 
 
        # Signaled when a character Spawned from the NPC Spawner Device is
        # eliminated. Sends a device_ai_interaction_result of the agent who eliminated
        # the character, and
        MyNPCSpawnerDevice.EliminatedEvent.Subscribe(OnCharacterEliminated)
 
 
        # Spawn a character from the NPC Spawner Device.
        MyNPCSpawnerDevice.Spawn()
 
 
        Sleep(15.0)
 
 
        # Eliminates all creatures spawned by this device.
        MyNPCSpawnerDevice.DespawnAll(false)
 
 
    # This function runs when a character is spawned from the NPC Spawner
    # because it's an event handler for SpawnedEvent.
    OnCharacterSpawned(SpawnedAgent:agent):void=
 
 
        Print("A character just spawned from this device.")
 
 
        # When a character spawns, have them focus on the first player in the playspace
        if:
            FortCharacter := SpawnedAgent.GetFortCharacter[]
            FocusInterface := FortCharacter.GetFocusInterface[]
            PlayerToFocus := GetPlayspace().GetPlayers()[0]
        then:
            spawn{FocusInterface.MaintainFocus(PlayerToFocus)}
 
 
    # This function runs when the character spawned from the NPC Spawner
    # is eliminated, because it's an event handler for EliminatedEvent.
    OnCharacterEliminated(AIInteractionResult:device_ai_interaction_result):void=
 
 
        # `Source` is the `agent` that has eliminated the creature.
        # If the creature was eliminated by a non-agent then `Source` is 'false'.
        # `Target` is the creature that was eliminated.
        if(AIInteractionResult.Source?):
            Print("The character was eliminated by another agent.")
        else:
            Print("The character was not eliminated by another agent.")
using { /Fortnite.com/AI } using { /Fortnite.com/Characters } using { /Fortnite.com/Devices } using { /Verse.org/Simulation } using { /UnrealEngine.com/Temporary/Diagnostics } # Visit [here](https://dev.epicgames.com/documentation/en-us/uefn/create-your-own-device-in-verse) to create a verse device. # A Verse-authored creative device that can be placed in a level npc_spawner_device_example := class(creative_device): # Reference to the NPC Spawner Device in the level. # In the Details panel for this Verse device, # set this property to your NPC Spawner Device. @editable MyNPCSpawnerDevice:npc_spawner_device = npc_spawner_device{} # Runs when the device is started in a running game. OnBegin<override>()<suspends>:void= # Example for subscribing to an event on the Creative device. # Signaled when a character is spawned from the NPC Spawner Device. # Sends the `agent` character who was spawned. MyNPCSpawnerDevice.SpawnedEvent.Subscribe(OnCharacterSpawned) # Signaled when a character Spawned from the NPC Spawner Device is # eliminated. Sends a device_ai_interaction_result of the agent who eliminated # the character, and MyNPCSpawnerDevice.EliminatedEvent.Subscribe(OnCharacterEliminated) # Spawn a character from the NPC Spawner Device. MyNPCSpawnerDevice.Spawn() Sleep(15.0) # Eliminates all creatures spawned by this device. MyNPCSpawnerDevice.DespawnAll(false) # This function runs when a character is spawned from the NPC Spawner # because it's an event handler for SpawnedEvent. OnCharacterSpawned(SpawnedAgent:agent):void= Print("A character just spawned from this device.") # When a character spawns, have them focus on the first player in the playspace if: FortCharacter := SpawnedAgent.GetFortCharacter[] FocusInterface := FortCharacter.GetFocusInterface[] PlayerToFocus := GetPlayspace().GetPlayers()[0] then: spawn{FocusInterface.MaintainFocus(PlayerToFocus)} # This function runs when the character spawned from the NPC Spawner # is eliminated, because it's an event handler for EliminatedEvent. OnCharacterEliminated(AIInteractionResult:device_ai_interaction_result):void= # `Source` is the `agent` that has eliminated the creature. # If the creature was eliminated by a non-agent then `Source` is 'false'. # `Target` is the creature that was eliminated. if(AIInteractionResult.Source?): Print("The character was eliminated by another agent.") else: Print("The character was not eliminated by another agent.")
To use this code in your UEFN experience, follow these steps.

Drag an NPC Spawner device onto your island.

Create a new Verse device named npc_spawner_device_verse_example. See Create Your Own Device Using Verse for steps.

In Visual Studio Code, open npc_spawner_device_verse_example.verse in Visual Studio Code and paste the code above.

Compile your code and drag your Verse-authored device onto your island. See Adding Your Verse Device to Your Level for steps.

Select your Verse device in the Outliner.

In the device’s Details panel, assign the object reference for the NPC Spawner to the NPC Spawner device on your island. You can use the eyedropper to pick the device in the Viewport or use the dropdown to search for the device.

Save your project and click Launch Session.

NPC Spawner Device API
See the npc_spawner_device API Reference for more information on using the NPC Spawner device in Verse.

NPC Character Definitions
Create Character Definitions to add attributes that can be imported into the NPC Spawner device.

NPC Character Definitions
This feature is in Early Access. You can publish an island with this feature, but be aware that through the Early Access period, changes may break your island and may require your active intervention.

Create NPC Character Definitions to modify NPCs beyond the NPC Spawner device's basic settings. With the NPC Spawner’s basic options, you can create instances of characters. Through Character Definitions, you can customize character type, behavior, and modifiers. You can even write Verse scripts that further instruct character behaviors.

With Character Definitions, you can save the properties of custom characters as assets. Any NPC Spawner in your project can then reference and reuse these assets. After connecting the asset to an NPC Spawner device, you can use the device's settings to override specific Character Definition properties.

NPC Character Definition in UEFN
The NPC Spawner device's modifiers override any Character Definition modifiers to provide the means for slight variations in NPC instances.

Creating Character Definitions
Character Defeinition Thumbnail
You can either create Character Definitions through the Content Drawer or directly through the NPC Spawner's settings.

Your modified Character Definitions can be seen once imported into the NPC Spawner device. If you create a Character Definition within the NPC Spawner, your modifications are immediately reflected in the NPC Spawner device.

To create a Character Definition through the Content Drawer, follow these steps:

Navigate to your project's content folder and left-click within the Content Drawer.

In the pop-up window, navigate to Artificial Intelligence > NPC Character Definition.

Name your Character Definition then double-click the thumbnail to edit your NPC's properties.

To create a Character Definition through the NPC Spawner device, follow these steps:

Place an NPC Spawner device and open its Details panel.

In the User Options, navigate to NPC Character Definition and left-click on its dropdown menu.

In its Create New Asset window, select NPC Character Definition.

Name your Character Definition then double-click its square thumbnail to open the Character Definition window.

Character Definitions
Character Definitions
Through the Character Definition's settings, you can customize the following options.

NPC Character Type

NPC Behavior

NPC Character Modifiers

NPC Character Type
Character Type
Select from the NPC Character Type dropdown to set the base properties for how your character exists in the gameplay. You can choose a character modeled after Fortnite guards and wildlife, or create customized behaviors with Verse.

This setting has contextual filtering and will trigger different options once selected.

Character Type	Description
Custom

Behaviors are defined in Verse.

Guard

NPCs have the same functionality as the Guard Spawner, though you can have more control over properties like movement and behavior.

Wildlife

Creates the subtype options of Boar, Chicken, Raptor, and Wolf. Each subtype has its own default behavior. Wildlife NPCs have the same functionality as the Wildlife Spawner, though you can  control over properties like movement and behavior.

  Additional character types are available when working on specific brand islands. To learn more, see the Custom IP Character Definitions section on this page.   

NPC Character Behavior
Character Behavior
After you select a character type, you can set the character's behavior. You can set behaviors as empty, default, or assigned through Verse.

Character Behavior	Description
Empty Behavior

Available with Custom character types. Creates a blank behavior for NPCs to remain in their reference pose. This is useful to remove NPC behaviors so it will only be animated in Sequence cinematics.

Default Behavior

Available with the Guard and Wildlife character types. Allows you to alter the behavioral settings of characters intended to have the mannerisms of Battle Royale guards.

Verse Behavior

Available with all character types. Allows you to include any Verse scripts for your character.

For more information on creating your own NPC Behaviors, check out the Create Custom NPC Behavior page.

NPC Character Modifiers
Character Modifiers
Use Character Modifiers to customize the characteristics of your character. Each Character Type will have its own preset of starting modifiers automatically applied when you select it.

Click the plus arrow to add more Character Modifiers. You can only have one of each modifier active at a time.


Character Modifiers	Description
Awareness Modifier

Modifies alertness and awareness. 

Cosmetic Modifier

Modifies looks and cosmetics. You can choose between Fortnite Character Item Definitions (CIDs), which will display as internal names.

Effects Modifier

Modifies the effects applied to an NPC.

Guard Perception Modifier

Modifies sight and hearing.

Health Modifier

Modifies health and shield.

Inventory Modifier

Modifies an NPC's inventory.

Navigation Modifier

Modifies the NPC's navigation parameters.

Patrol Path Modifier

Modifies the patrol path.

Team Modifier

Modifies the team. You can apply a team number or specify if the NPC is considered a wildlife, creature, or neutral.

UI Modifier

Modifies the display information for an NPC, such as name and health bar.

Custom IP Character Definitions
A few brand partners have their own NPCs available through a NPC Character Definition. 

Depending on the IP, you can find the unique NPCs in one or both of the following: 

The NPC Character Type which can include unique modifiers.

Through the Cosmetic Modifier when selecting a Custom or Guard character type.

IP assets have specific rules and guidelines for use. Check the brand rules for the IP assets you intend to use. To learn more about the various brand partners and content, see Game Collections.   

You can only use brand assets in a project specific to the relevant IP property.

Importing Character Definitions
Importing Character Definitions
After your Character Definition is created and saved, import it into an NPC Spawner device's NPC Character Definition setting. Once imported, your NPC Spawner's character automatically updates to reflect your Character Definition.

You can use the same Character Definition for multiple devices and make slight variations to characters by overriding individual device settings. Any updates you make for the Character Definition will affect every device it's assigned to.

Placing Character Definitions
You can place Character Definitions directly from the Content Drawer or through the NPC Spawner device.

To place multiple Character Definitions, you may need to save the level first.

Dragging a Character Definition from the Content Drawer is a shortcut with the same functionality as placing an NPC Spawner device with an assigned Character Definition.

Using the NPC Spawner with Animations
Use custom animations and emotes with the NPC Spawner device and Verse code.

Using the NPC Spawner with Animations
Prerequisite topics
In order to understand and use the content on this page, make sure you are familiar with the following topics:

Animated Mesh Device
Sequencer and Control Rig
Camera Rig Rails and Rig Crane
This feature is in Early Access. You can publish an island with this feature, but be aware that through the Early Access period, changes may break your island and may require your active intervention.

NPC Spawners require a Binding Lifetime track in sequencer. There is no way to retroactively add this track to existing sequences created before 31.00. You have to re-publish any islands that use an NPC spawner in a sequence after adding the Binding Lifetime track.

To add a Binding Lifetime track:

Click the + icon next to the NPC Spawner in the Track list.

Select Binding Lifetime from the drop down menu.

Use Sequencer to create custom character animations can be play in a variety of ways and on multiple devices, including the NPC Spawner device. Use either events or Sequencer paired with Cinematic Sequence devices to set and play animations with patterned behaviors along select points of the AI Patrol Path.

You can import and migrate custom animations from Unreal Engine (UE) including MetaHumans. To do so, you may have to retarget the skeletal mesh to fit NPC characters since Fortnite characters have their own skeletal structure.

MetaHuman characters are memory intensive. It's best to limit the number of MetaHuman assets you use.

Animating NPCs in Sequencer
The NPC Spawner device opens a variety of gameplay creativity for your project, from interactive characters to informative cutscenes. Create custom animations for the NPC Spawner with Control Rig, or you can import animations you bought or created in other software.

You can also use the FK Control Rig to animate NPCs with a retargeted animation or emote.

Learn more about the FK Control Rig animation workflows in UE documentation.

To capture animations with NPC characters, follow the steps below.

Right-click in the Content Browser to create a Level Sequence.


Rename your Level Sequence thumbnail.


Double-click the Level Sequence thumbnail to open the Sequencer Editor.

Click +Track then select Actor to Sequencer > NPC Spawner. This adds the NPC Spawner device to the Level Sequence track.


You can drag the NPC Spawner device into the track list from the Outliner to add it to the Level Sequence.

Click the + icon next to the NPC Spawner device in the track list and select Control Rig > Control Rig Classes > FK Control Rig. This adds the NPC's skeleton to the track, giving you access to individual bones of the skeleton to manipulate and record.

Select the bones you want to move from the Viewport, Anim Outliner, or Sequencer and move them into a starting position for your animation.

Set the first keyframe by clicking the + icon next to the bones you moved.


If you have an animation you created or purchased as an FBX animation sequence file, you can add those files to an NPC Spawner device's animation track in the timeline by clicking the + icon next to the NPC Spawner and selecting Animation > Animation file.

Continue to move the bones and set new keyframes in the Sequencer timeline until your animation is complete. Once the animation is done, play the animation in Sequencer to make sure the movement suits your preferences.

A simple way to play an animation backwards is by right-clicking on the animation file in the timeline and selecting Properties > Reverse.

When you're satisfied with the results, it's time to bake the animation to the skeletal mesh. Right-click on the NPC Spawner and select Bake Animation Sequence.

Make sure the limbs of your skeletal mesh don't clip through other parts of the skeletal mesh body when you play back the animation.

Recording Behavioral Attributes
You can use behavioral attributes with the NPC Spawner device as well. The behavior options determine the base characteristic the NPC inherits from Fortnite Battle Royale NPCs. These characteristics determine whether the NPC acts like a guard or wildlife.

For more information on how to set the behavioral attributes with the NPC Spawner device, refer to the NPC Character Definition document.

Once you've set up these behavioral attributes, you can keyframe the animations in a Level Sequence and play them on a Cinematic Sequence device during the gameplay. Unlike the steps above, you don't need to bake the performance into the Control Rig since the behavior is set in the NPC Spawner device's options.

You can also use the animation you create, or the inherited behavior with the AI Patrol Path Node device and record the NPC following the path you create with the Cine Camera Actor.

Spawnable and Replaceable NPC Bindings
There are now two more ways to bring an NPC into your sequences: the spawnable NPC binding and the replaceable NPC binding. These bindings are created from NPC Character definitions.

Spawnable NPC Binding
Using a cinematic sequence, the spawnable NPC binding can spawn an actor into the world based on an NPC Character definition. This NPC can be animated in Sequencer the same way you would any skeletal mesh.

To create a spawnable NPC binding, simply drag your NPC character definition into Sequencer:


Click gif to enlarge.

The spawnable binding can be animated just like any other skeletal mesh actor. For example:

Click + Animation and select a dance emote for the NPC Character definition.


Click gif to enlarge.

Move your playhead further ahead, drag your NPC to a new location, and set a new keyframe. The NPC will now move from point A to point B.


Click gif to enlarge.

Replaceable NPC Binding
The replaceable NPC binding will take control of an NPC spawned into the world and place it into your sequence. They can then perform animations created in Sequencer. While the NPC is bound by the sequencer, all behavior, perception and path following is paused. These are resumed when the NPC is unbound.

The NPC will be placed back to its original location when it is no longer bound.

To create a replaceable NPC binding, create a spawnable NPC binding, right-click your binding, and choose Convert selecting binding to > Replaceable NPC Character.


Click gif to enlarge.

After the conversion, the track is replaced with a binding lifetime track. All changes made to the spawnable binding are retained.

For the NPC to be found and bound during gameplay, you need to add a modifier to the NPC Character Definition: the sequencer modifier. You can add this to your NPC Character Definition using the same method as other modifiers. If you don't add this modifier, you will get a validation failure.


Click gif to enlarge.

The sequencer modifier has a Unique Identifier property. This property is used to locate the spawned NPC in game. The default value is the name of the NPC Character Definition. Note that if two different NPC Character Definitions have the same unique Identifier, both can be bound when your sequence plays in game.

Playing Sequences in Game
To play your sequences, use the cinematic sequence device normally.

A spawnable binding does not need any further setup to play.

A replaceable binding requires you to add an NPC Spawner in your world that uses your NPC Character Definition. If the replaceable binding fails to find an NPC to bind to, you will see the following line in your client log:

LogFortNPCMovieSceneBindings: Warning: Could not bind to a pawn using NPC Character Definition Guard. Please ensure there is at least one spawned.

If you want to spawn the NPC at the same time as your sequence is due to be played. Consider using a spawnable binding or hook the On Spawned event up to the Play function on the cinematic sequence device.

Custom Blueprint NPCs
Most NPC types will bind as skeletal meshes, with the exception of an NPC character definition that uses a custom Blueprint.

Custom BP
This will bind the Blueprint and expose additional components, such as VFX, which can then be modified in the sequencer.

Here you can see a Niagara particle system has been modified in Sequencer to make the NPC's head explode:


Click gif to enlarge.

Known Restrictions
Replaceable NPC bindings can only be used with the Cinematic Sequence device set to Visibility: Everyone. Using any other Visibility setting will fail validation.

Trying to use a replaceable NPC binding with rideable or tameable wildlife NPCs will fail validation.

Replaceable NPC bindings that use an NPC Character Definition cannot use the Force Keep State option on the Finish Completion State Override user option. Trying to use this option will fail validation.

When an NPC is bound by sequencer it will snap into place. Additionally, latency issues can cause very short visual bugs when the NPC is bound and unbound. For this reason it is highly advised to make use of techniques such as spawning the NPC offscreen, screen fades, VFX or the visibility track when using a replaceable NPC binding.

Calling Animations with Verse
By exposing animations to Verse using asset reflection, you can play custom animations on your NPCs using the animation module.

Animation Controller Interface
The play_animation_controller interface allows you to play an animation on a character and can be retrieved with the GetPlayAnimationController() function. This interface exposes two functions that play animations. The synchronous Play() function, and the asynchronous PlayAndAwait() function.

Both functions accept the following parameters:

Option	Value	Description
Animation

Select an Animation

The animation to play. Must specify an animation in the Assets.digest.verse file.

PlayRate

1.0, Select a Play Rate

The speed to play the animation at. A value of 1.0 corresponds to the default speed of the animation

BlendInTime

0.0, Select a BlendInTime

The length of time to blend the previous animation into the current one.

BlendOutTime

0.0, Select a BlendOutTime

The length of time to blend the current animation into the next one.

StartPositionSeconds

0.0, Select a StartPositionSeconds

The position in seconds to start playing the animation from.

Play And Await Function
The PlayAndAwait() function plays an animation asynchronously and returns an instance of the play_animation_result enum, which contains three values, Completed, Interrupted, and Error. These correspond to a completed animation, an animation that was interrupted, and an error occurring respectively. By querying this enum, you can execute different code based on the result of your animation.

Verse
AnimationResult := PlayAnimController.PlayAndAwait(MyAnimation)
    case(AnimationResult):
        play_animation_result.Completed => Print("Animation Completed!")
        play_animation_result.Interrupted => Print("Animation Interrupted.")
        play_animation_result.Error => ("Error Occurred during animation.")
AnimationResult := PlayAnimController.PlayAndAwait(MyAnimation) case(AnimationResult): play_animation_result.Completed => Print("Animation Completed!") play_animation_result.Interrupted => Print("Animation Interrupted.") play_animation_result.Error => ("Error Occurred during animation.")
Play Function
The Play() function runs synchronously and returns an instance of the playing_animation_instance class. The playing_animation_instance class lets you query and manipulate an ongoing animation and contains the following values:

Value	Explanation
GetState()

This function returns the current state of animation playback in a play_animation_state enum.

Stop()

This function stops the current animation.

CompletedEvent

This event is triggered when an animation is completed

InterruptedEvent

This event is triggered when an animation is interrupted.

BlendedInEvent

This event is triggered when an animation has finished blending out.

BlendingOutEvent

This event is triggered when an animation begins to blend out.

Await()

This function waits for the animation to complete or be interrupted. Notably, this returns a play_animation_result enum, and is functionally identical to calling PlayAndAwait().

You can use the Play() function to manipulate ongoing animations or execute code when certain conditions in your animation are met.

Verse
# Play an animation synchronously and get its animation instance
AnimationInstance := PlayAnimController.Play(MyAnimation, ?PlayRate := PlayRate, ?BlendInTime := BlendInTime, ?BlendOutTime := BlendInTime, ?StartPositionSeconds := StartPositionSeconds)
 
# Subscribe to a function that runs when the animation completes
AnimationInstance.CompletedEvent.Subscribe(OnAnimationComplete)
 
Sleep(1.0)
 
AnimationState := AnimationInstance.GetState()
 
# If the animation is still playing after a second, stop the animation
 
if(AnimationState = play_animation_state.BlendingOut):
    AnimationInstance.Stop()
# Play an animation synchronously and get its animation instance AnimationInstance := PlayAnimController.Play(MyAnimation, ?PlayRate := PlayRate, ?BlendInTime := BlendInTime, ?BlendOutTime := BlendInTime, ?StartPositionSeconds := StartPositionSeconds) # Subscribe to a function that runs when the animation completes AnimationInstance.CompletedEvent.Subscribe(OnAnimationComplete) Sleep(1.0) AnimationState := AnimationInstance.GetState() # If the animation is still playing after a second, stop the animation if(AnimationState = play_animation_state.BlendingOut): AnimationInstance.Stop()
Play Animation Example
The code below shows an example of an NPC behavior that uses the animation module to play an animation. Note that any custom animations you want to play on your characters must first be exposed to Verse through asset reflection, and must appear in the Assets.digest.verse file. In this example, the animation MyAnimation is located in the Animations module of the custom MyCharacter character in Assets.digest.verse, and so is called through MyCharacter.Animations.MyCharacter.

Verse
using { /Fortnite.com/AI }
using { /Fortnite.com/Animation/PlayAnimation }
using { /Verse.org/Simulation }
using { /Fortnite.com/Characters }
 
basic_play_anim_example := class(npc_behavior):
    # The speed to play the animation at.
    @editable
    PlayRate : float = 1.0
 
    # How long to blend the previous animation into
    # the current one.
    @editable
    BlendInTime : float = 0.25
 
    # How long to blend the current animation into
    # the next one.
    @editable
    BlendOutTime : float = 0.25
 
    # The position in seconds to start playing the
    # animation from.
    @editable
    StartPositionSeconds : float = 0.0
 
    # How long to wait before restarting the animation.
    @editable
    SleepDuration : float = 2.0
 
    OnBegin<override>()<suspends>:void=
        if:
            # Get the animation controller of the NPC Character
            Agent := GetAgent[]
            FortCharacter := Agent.GetFortCharacter[]
            PlayAnimController := FortCharacter.GetPlayAnimationController[]
        then:
            AnimationResult := PlayAnimController.PlayAndAwait(MyCharacter.Animations.MyAnimation, ?PlayRate := PlayRate, ?BlendInTime := BlendInTime, ?BlendOutTime := BlendInTime, ?StartPositionSeconds := StartPositionSeconds)
 
            # Print the result of running the animation.
            case(AnimationResult):
                play_animation_result.Completed => Print("Animation Completed!")
                play_animation_result.Interrupted => Print("Animation Interrupted.")
                play_animation_result.Error => ("Error Occurred during animation.")
 
            Sleep(SleepDuration)
 
            # Play an animation synchronously and get its animation instance.
            AnimationInstance := PlayAnimController.Play(MyCharacter.Animations.MyAnimation, ?PlayRate := PlayRate, ?BlendInTime := BlendInTime, ?BlendOutTime := BlendInTime, ?StartPositionSeconds := StartPositionSeconds)
 
            Sleep(SleepDuration)
 
            AnimationState := AnimationInstance.GetState()
 
            # Print the current state of the animation.
            case(AnimationState):
                play_animation_state.Playing => Print("Animation Playing!")
                play_animation_state.BlendingIn => Print("Animation Blending In!")
                play_animation_state.BlendingOut => Print("Animation Blending Out!")
                play_animation_state.Completed => Print("Animation Completed!")
                play_animation_state.Stopped => Print("Animation Stopped!")
                play_animation_state.Interrupted => Print("Animation Interrupted!")
                play_animation_state.Error => Print("Error Occurred During Animation")
        else:
            Print("Could not get animation controller")

Create Custom NPC Behavior
Use Verse code to create your own NPC behavior unique to your game design needs!

Create Custom NPC Behavior
This feature is in Early Access. You can publish an island with this feature, but be aware that through the Early Access period, changes may break your island and may require your active intervention.

The behavior of an NPC character is defined by their behavior script. The behavior script is what tells characters what actions to take in the world, such as where to go, what to fight, and how to interact with other characters. Characters such as guards and wildlife may have additional behaviors, such as perception, alertness, and the ability to be hired or tamed.

An NPC Behavior is a user-defined Verse script that adds extra functionality to an NPC character’s existing behaviors. The npc_behavior API lets you define code that runs when an NPC character spawns or despawns, and you can use it to create custom characters like medics, shopkeepers, or bosses. NPC Behaviors inherit from the npc_behavior abstract class and require importing the /Fortnite.com/AI module to use.

To run an NPC Behavior Script, you need to attach it to an NPC Character Definition. How an NPC Behavior Script interacts with a character definition depends on the NPC Character type. Custom-type NPCs need a behavior script to perform actions, while Guard and Wildlife-type NPCs will run their default behavior if they aren’t given a behavior script. For more information on creating an NPC Character Definition and the different character types, see the Character Definition page.

This tutorial goes over the basics of creating an NPC behavior script and teaches you how to spawn an NPC and navigate it to an objective.

Creating a New NPC Behavior Script
Follow these steps to create an NPC Behavior Script in UEFN that spawns a guard and patrols them between two points.

Open your project in UEFN, then in the Menu Bar, go to Verse > Verse Explorer.

In Verse Explorer, right-click on your project name and choose Add new Verse file to project to open the Create Verse Script window.

Add New Verse File to Project
In the Create Verse Script window, click NPC Behavior to select it as your template.

Name your NPC Behavior by changing the text in the NPC Behavior Name field to the name of your device. In this example, the device is named my_first_npc_behavior.

My First NPC Behavior
Click Create to create the Verse file.

In Verse Explorer, double-click the name of your Verse file to open it in Visual Studio Code.

Save your code, compile it, and create a new NPC character definition. For more information on creating an NPC character, see the Character Definition page.

Assign your my_first_behavior script as the Verse behavior of your new Character Definition.

Click launch session in the UEFN toolbar to playtest your level. When you playtest your level, characters spawned from your NPC Spawner should pick a random point near when they spawn and navigate to it. When they reach that point, they should wait a certain amount of time and navigate back to their starting point. If you’ve enabled Verse Debug Draw enabled from the Island Settings device, you should see arrows drawn that show where the character is focusing, as well as boxes that show the point a character is navigating to.


Navigatable
You can use the Navigatable API to direct characters to certain targets and for things like patrolling, guarding a point, or following another character. Guard-type NPCs can do this with AI Patrol Path nodes, but here you’ll use verse code to extend this functionality to any type of character and avoid placing additional devices in the level. The character’s navigatable interface allows you to navigate characters to a navigation_target, which you can create from an agent or position. Custom, Guard, and Wildlife-type NPCs can all use the navigatable interface. To get the character’s navigatable interface you’ll first need to get a reference to their fort_character, which you can do by calling GetFortCharacter[].

Verse
# Get the Navigatable Interface, this allows you to tell it to move.
Navigatable := Character.GetNavigatable[]
# Get the Navigatable Interface, this allows you to tell it to move. Navigatable := Character.GetNavigatable[]
In the template example, the code chooses a position from a random offset where the character spawns and saves it in a variable GoToPoint. It then creates a navigatoin_target from both the GotToPoint and the character’s spawn point.

Verse
# Create a random offset from the spawn point to walk toward.
GoToPoint := NPCSpawnPoint + vector3{X := GetRandomFloat(-DistanceFromSpawnPtToMove,DistanceFromSpawnPtToMove),
                                     Y := GetRandomFloat(-DistanceFromSpawnPtToMove,DistanceFromSpawnPtToMove),
                                     Z := 0.0 }
 
if(ShowAIDebug?):
    Print(my_first_npc_behavior_message_module.OnNavigateBeginMessage(Agent,GoToPoint.X,GoToPoint.Y,GoToPoint.Z), ?Duration := AIDebugDrawTi
 
# Create a navigation target from these two positions that the navigation interface can use.
NavTargetStart := MakeNavigationTarget(GoToPoint)
NavTargetEnd := MakeNavigationTarget(NPCSpawnPoint)
# Create a random offset from the spawn point to walk toward. GoToPoint := NPCSpawnPoint + vector3{X := GetRandomFloat(-DistanceFromSpawnPtToMove,DistanceFromSpawnPtToMove), Y := GetRandomFloat(-DistanceFromSpawnPtToMove,DistanceFromSpawnPtToMove), Z := 0.0 } if(ShowAIDebug?): Print(my_first_npc_behavior_message_module.OnNavigateBeginMessage(Agent,GoToPoint.X,GoToPoint.Y,GoToPoint.Z), ?Duration := AIDebugDrawTi # Create a navigation target from these two positions that the navigation interface can use. NavTargetStart := MakeNavigationTarget(GoToPoint) NavTargetEnd := MakeNavigationTarget(NPCSpawnPoint)
The NavigateTo() function returns a navigation_result enum, which contains info about whether the character reached their navigation_target. You can check the value of your navigation_result to give characters behaviors based on whether they reached their target or not.

Verse
# Check to see if something has interfered with the NPC reaching the intended location and print a
# message to the output log.
if (NavResultGoTo <> navigation_result.Reached):
    if(ShowAIDebug?):
        Print(my_first_npc_behavior_message_module.OnNavigateErrorMessage(Agent,GoToPoint.X,GoToPoint.Y,GoToPoint.Z), ?Duration := AIDebugDrawTime)
else:
    # Once it arrives at its location, wait for this duration in seconds
    Navigatable.Wait(?Duration := MoveToWaitDuration)
# Check to see if something has interfered with the NPC reaching the intended location and print a # message to the output log. if (NavResultGoTo <> navigation_result.Reached): if(ShowAIDebug?): Print(my_first_npc_behavior_message_module.OnNavigateErrorMessage(Agent,GoToPoint.X,GoToPoint.Y,GoToPoint.Z), ?Duration := AIDebugDrawTime) else: # Once it arrives at its location, wait for this duration in seconds Navigatable.Wait(?Duration := MoveToWaitDuration)
For more information on how characters navigate the world and to visualize the different areas characters can navigate to, see the Navigation Mesh page.

Focus
When characters perform actions, they look at specific targets. The specific target a character is looking at is the character’s focus. Characters focus on the character they’re talking to, the target they’re attacking, or the position they’re navigating to. The focus_interface lets you specify specific targets for your characters to focus on. Custom, Guard, and Wildlife-type NPCs can all use the focus interface. The MaintainFocus() function focuses your character on a target, which can be either a vector3 position or an agent. The focus_interface is part of the fort_character interface, and you can retrieve it using GetFocusInterface[].

Verse
# Get the Focus Interface, this allows you to tell it to look at something or somewhere.
Focus := Character.GetFocusInterface[]
# Get the Focus Interface, this allows you to tell it to look at something or somewhere. Focus := Character.GetFocusInterface[]
In the template example, after the character begins navigating back to the starting position, the code uses MaintainFocus() to force them to focus on the previous navigation_target. This causes the character to walk backward and watch behind them as they return to their starting point.

Verse
# Leveraging concurrency to wait until the NPC reaches its destination, while the calls to look back at its origin point 
# and drawing a debug arrow never completes, continuing, ensures only the NavigateTo can win the race.
NavResultGoToNext := race:
    # Move back to its starting position.
    Navigatable.NavigateTo(NavTargetEnd)
 
    # Sets NPC to look at its previous position which will make it walk backwards. 
    # This is meant to show the utility of the focus interface.
    block:
        Focus.MaintainFocus(GoToPoint)
        navigation_result.Interrupted
    block:
        if(ShowAIDebug?):
            DrawDebugLookAt(Character, GoToPoint) 
        else:
            Sleep(Inf)
        navigation_result.Interrupted
# Leveraging concurrency to wait until the NPC reaches its destination, while the calls to look back at its origin point # and drawing a debug arrow never completes, continuing, ensures only the NavigateTo can win the race. NavResultGoToNext := race: # Move back to its starting position. Navigatable.NavigateTo(NavTargetEnd) # Sets NPC to look at its previous position which will make it walk backwards. # This is meant to show the utility of the focus interface. block: Focus.MaintainFocus(GoToPoint) navigation_result.Interrupted block: if(ShowAIDebug?): DrawDebugLookAt(Character, GoToPoint) else: Sleep(Inf) navigation_result.Interrupted
Leashable
When guards guard an objective, you want to make sure they stay in an area around the objective and don’t wander off too far. The fort_leashable interface is a Guard-type NPC-specific interface that lets you specify a radius around a target that guards won’t patrol out of. You can leash guards to specific positions or other NPCs, and guards will update their position to stay near their leash target if it moves. Note that currently Custom and Wildlife-type NPC characters cannot use the fort_leashable interface. You can retrieve the fort_leashable interface using GetFortLeashable[].

Verse
# Get the Leash Interface, which lets you confine a guard to a certain area.
Leashable := Character.GetFortLeashable[]
# Get the Leash Interface, which lets you confine a guard to a certain area. Leashable := Character.GetFortLeashable[]
You can leash guards to either positions or other agents, such as when guarding a capture point or protecting an important NPC. Each leash has an InnerRadius and OuterRadius, which specify how close and how far in centimeters guards should stay from their leash target respectively. The template example does not use the leashable interface, but you might find it useful when creating your own guard NPCs.

Verse
# Leash the guard to a position so they stay between 500 and 1000
# cm of the position they're leashed to
Leashable.SetLeashPosition(NPCSpawnPoint, InnerRadius := 500.0, OuterRadius := 1000.0)
 
# Leash the guard to an agent so they stay between 500 and 1000
# cm of the agent they're leashed to
Leashable.SetLeashAgent(AgentToFollow, InnerRadius := 500.0, OuterRadius := 1000.0)
# Clear all leashes on the guard
Leashable.ClearLeash()
# Leash the guard to a position so they stay between 500 and 1000 # cm of the position they're leashed to Leashable.SetLeashPosition(NPCSpawnPoint, InnerRadius := 500.0, OuterRadius := 1000.0) # Leash the guard to an agent so they stay between 500 and 1000 # cm of the agent they're leashed to Leashable.SetLeashAgent(AgentToFollow, InnerRadius := 500.0, OuterRadius := 1000.0) # Clear all leashes on the guard Leashable.ClearLeash()
Debug Draw
At the top of the file, this template defines a dedicated channel for debug draw. You can use the Debug Draw to visualize certain game data for testing purposes. For instance, you can visualize the visibility range of your character, or draw a shape around the location they’re traveling to. Verse Debug Draw must be enabled from the Debug tab in Island Settings to visualize these debug shapes, and they will not appear in published experiences. The channel at the top of the file lets you hide, show, or clear all the debug shapes in a channel using a single method.

Verse
# Create a dedicated debug channel to draw to for this behavior
npc_debug_draw := class(debug_draw_channel) {}
# Create a dedicated debug channel to draw to for this behavior npc_debug_draw := class(debug_draw_channel) {}
The new_npc_behavior template class defines several values used for visualization and movement.

The MoveToWaitDuration defines how long in seconds your character waits at a point before moving.

Verse
      # How long to wait in seconds after the NPC navigates to a point before moving on.
      @editable_number(float):
          Categories:=array{my_first_npc_behavior_message_module.SettingsCategory},
          MinValue:=option{0.5},
          MaxValue:=option{10.0}
      MoveToWaitDuration:float = 5.0
# How long to wait in seconds after the NPC navigates to a point before moving on. @editable_number(float): Categories:=array{my_first_npc_behavior_message_module.SettingsCategory}, MinValue:=option{0.5}, MaxValue:=option{10.0} MoveToWaitDuration:float = 5.0
The DistanceFromSpawnPtToMove defines the range of the random offset from the spawnpoint for your character to move.

Verse
      # The negative min and absolute max x & y coordinate offset in centimeters to tell the NPC to move to
      @editable_number(float):
          Categories:=array{my_first_npc_behavior_message_module.SettingsCategory},
          MinValue:=option{0.0}
      DistanceFromSpawnPtToMove:float = 1500.0
# The negative min and absolute max x &amp; y coordinate offset in centimeters to tell the NPC to move to @editable_number(float): Categories:=array{my_first_npc_behavior_message_module.SettingsCategory}, MinValue:=option{0.0} DistanceFromSpawnPtToMove:float = 1500.0
The ShowAIDebug logic value lets you toggle drawing debug shapes from the editor.

Verse
      # Whether to draw debug to the NPC channel when Verse Debug Draw is enabled in Island Settings.
      @editable:
          Categories:=array{my_first_npc_behavior_message_module.SettingsCategory}
      ShowAIDebug:logic = true
# Whether to draw debug to the NPC channel when Verse Debug Draw is enabled in Island Settings. @editable: Categories:=array{my_first_npc_behavior_message_module.SettingsCategory} ShowAIDebug:logic = true
The AIDebugDrawTime float lets you specify the amount of time to render the debug draw location.

~~(verse) # How long in seconds to render the debug draw location and print text. # It is recommended to keep this in sync with MoveToWaitDuration otherwise the print will not be shown if a previous message is displayed. @editable_number(float): Categories:=array{my_first_npc_behavior_message_module.SettingsCategory}, MinValue:=option{0.5} AIDebugDrawTime:float = 5.0 ~~

The LookAtDebugDrawDuration float lets you specify how long to render the look arrow debug draw.

Verse
      # How long in seconds to render the look at arrow's debug draw.
      LookAtDebugDrawDuration:float = 0.5
# How long in seconds to render the look at arrow&#39;s debug draw. LookAtDebugDrawDuration:float = 0.5
The DebugDrawNPC channel defines the debug draw instance, and uses the channel defined at the top of the file.

Verse
      # How long in seconds to render the look at arrow's debug draw.
      @editable_number(float):
          Categories:=array{my_first_npc_behavior_message_module.SettingsCategory},
          MinValue:=option{0.5}
      LookAtDebugDrawDuration:float = 0.5
# How long in seconds to render the look at arrow&#39;s debug draw. @editable_number(float): Categories:=array{my_first_npc_behavior_message_module.SettingsCategory}, MinValue:=option{0.5} LookAtDebugDrawDuration:float = 0.5
Finally the VerticalOffsetToNPCHead defines this offset from the NPC’s pelvis to the head to draw the debug look arrow from. Without this offset, the debug look arrow would be drawn from the center of the NPC.

Verse
      # Used for specifying a point offset from the NPC pelvis to the head to draw the look at arrow from.
      VerticalOffsetToNPCHead<private>:float = 55.0
# Used for specifying a point offset from the NPC pelvis to the head to draw the look at arrow from. VerticalOffsetToNPCHead&lt;private&gt;:float = 55.0
Two functions in the new_npc_behavior template class draw debug shapes. The DrawDebugLocation() function draws a large point at a specified position for a LookAtDebugDrawDuration amount of time.

Verse
# This function draws a box around a specified position for a finite amount of time.
# NOTE: To see this in game, Verse Debug Draw must be enabled in Island Settings.
DrawDebugLocation(Location:vector3):void = 
    DebugDrawNPC.DrawPoint( Location, 
                            ?Color := NamedColors.SteelBlue, 
                            ?Thickness := 100.0, 
                            ?DrawDurationPolicy := debug_draw_duration_policy.FiniteDuration, 
                            ?Duration := AIDebugDrawTime )
# This function draws a box around a specified position for a finite amount of time. # NOTE: To see this in game, Verse Debug Draw must be enabled in Island Settings. DrawDebugLocation(Location:vector3):void = DebugDrawNPC.DrawPoint( Location, ?Color := NamedColors.SteelBlue, ?Thickness := 100.0, ?DrawDurationPolicy := debug_draw_duration_policy.FiniteDuration, ?Duration := AIDebugDrawTime )
The DrawDebugLookAt() function lets you visualize where a character is looking by drawing an arrow from the agent’s head to its look point.

Verse
# This function draws an arrow from the Agent's head to its look at point every half a second.
# NOTE: To see this in game, Verse Debug Draw must be enabled in Island Settings.
DrawDebugLookAt(Character:fort_character, LookAtPoint:vector3)<suspends>:void=
    loop:
        DebugDrawNPC.DrawArrow( Character.GetTransform().Translation + vector3{ Z := VerticalOffsetToNPCHead},
                                LookAtPoint,
                                ?ArrowSize := 50.0,
                                ?Color := NamedColors.Yellow,
                                ?Thickness := 5.0,
                                ?DrawDurationPolicy := debug_draw_duration_policy.FiniteDuration,
                                ?Duration := LookAtDebugDrawDuration )
 
        #This sleep matches the length of time the arrow is drawn to avoid duplicate draws.
        Sleep(LookAtDebugDrawDuration)
# This function draws an arrow from the Agent's head to its look at point every half a second. # NOTE: To see this in game, Verse Debug Draw must be enabled in Island Settings. DrawDebugLookAt(Character:fort_character, LookAtPoint:vector3)<suspends>:void= loop: DebugDrawNPC.DrawArrow( Character.GetTransform().Translation + vector3{ Z := VerticalOffsetToNPCHead}, LookAtPoint, ?ArrowSize := 50.0, ?Color := NamedColors.Yellow, ?Thickness := 5.0, ?DrawDurationPolicy := debug_draw_duration_policy.FiniteDuration, ?Duration := LookAtDebugDrawDuration ) #This sleep matches the length of time the arrow is drawn to avoid duplicate draws. Sleep(LookAtDebugDrawDuration)
Adding your Character to the Level
Now that you’ve learned about the NPC BehaviorScript, it’s time to create a character and use the script on an island. The following workflow is designed for Guard-type characters, but the NPC Behavior Script will still work for Custom and Wildlife-type characters.

Create a new NPC Character Definition named MyFirstCharacterDefinition. Click your new character definition to open the Character Definition screen.

In the Character Definition screen, modify the following properties:

Under NPC Character Type, set Type to Guard. The guard interface lets you access guard-specific character functionality, such as events for when the guard is alerted or suspicious and lets you hire guards to use as allies. Guards may also equip weapons, while Custom and Wildlife-type characters currently cannot. You can also change the name of your character under the Name tab.

Under NPC Character Behavior, set Behavior to Verse Behavior. Then set the NPC Behavior Script to my_first_npc_behavior. Your character will still have access to functionality from the guard interface, but will use your Verse script to decide what to do during OnBegin and OnEnd.

In the Modifiers tab, under Guard Spawn Modifier, click the Cosmetic tab to change your character’s cosmetic appearance. You can choose from a preexisting cosmetic, or enable Character Cosmetic Retargeting to use a custom model. Note that only guards and Custom-type characters can use character cosmetic retargeting, while wildlife cannot. For more information on character modifiers and which ones apply to different character types, see the NPC Character Definition page.

On the Modifiers tab, click Add Element to add a new modifier to your character. Change the type of the new modifier to Inventory Modifier. Note that only guards can use the inventory modifier.

Under Inventory Modifier, click Add Element to add a new item to your character’s inventory. Set the Item Definition to a weapon, item, item, or anything else your character should have. You can add multiple items to your character’s inventory, and your characters will use weapons to fight, items to heal, etc.

On the Modifiers tab, click Add Element to add a new modifier to your character. Change the type of the new modifier to UI Modifier.

Under UI Modifier, click the Name tab to change your character’s name. Your character’s name will display above their head.

My First Character Definition
Save your NPC character definition. In the Content Browser, drag your NPC character definition into the level. This will automatically create a new NPC Spawner and assign your character definition to it.


Select your NPC Spawner. In the Outliner, under User Options:

Set Spawn Count to 20. You’re going to want a few guards to help you out, so have some fun and max this out.

Click Launch Session in the UEFN toolbar to playtest your level. When you playtest, your character should spawn and patrol between their starting point and a random point near it, and engage any enemies along the way.


On Your Own
By completing this guide, you’ve learned how to create an NPC Behavior Script to make your very own custom characters. For more reading and to learn how to create specific types of characters and scenarios, check out some of the NPC Behavior tutorials listed below.

Tutorials That Use NPC Behavior
Create your own NPC Medic
Create your own NPC Medic

Use Verse Code to create a custom NPC medic.

Create your own NPC Medic
Use Verse Code to create a custom NPC medic.

Create your own NPC Medic
Medics are a common character archetype in many games. A medic's job is to heal nearby characters, and they help their teammates recover after sustaining damage. Medics serve different roles depending on the game, for instance, doctors that serve patients in a hospital, combat medics that help their team fight as well as heal, or neutral stations that heal anyone.

The medic character you'll create in this example follows a set of logic rules.

Idle:

Begin Healing Agents

Healing Loop

Navigate to Agent

The medic begins idle, and patrols until an agent enters the healing zone. That agent gets added to the medic's healing queue. The medic needs to track the agent it needs to heal next, and a queue provides a useful data structure for this purpose since queues are a first-in, first-out data structure. This means the character that enters the healing zone first will be the first to get healed.

Once the medic gets the agent it needs to heal next, it first checks if the agent's health is below the healing threshold. If so, it begins healing them at a specific rate until the agent's health reaches the threshold, or the agent exits the healing zone. While healing, the medic will attempt to stay close to the agent by continuously navigating to them. Once the agent's health is back up to the threshold, the medic gets the next agent to heal and starts the process over again. If there are no agents to heal, the medic goes back to being idle.

You can visualize the logic of the medic NPC using the Finite-State Machine below. For more information on finite-state machines, check out Understanding NPC Behaviors.

Medic FSM
By completing this guide, you'll learn how to create a custom medic character using the NPC Behavior Script that heals other nearby characters when their health is under a certain threshold. The complete script is included at the end of this guide for reference.

Creating a new NPC Behavior Script
To start creating your own NPC Medic Character, create a new NPC Behavior script named medic_example. For more information on creating your own NPC Behavior script, see Create Your Own NPC Behavior. Open the Verse file in Visual Studio Code.

Follow these steps to create an NPC Behavior Script in UEFN that spawns a medic character that heals nearby players.

Implementing the Healing Queue
The NPC Behavior Script starts with several values used for character movement and debug visualization. You won't need all of them in this script, so you'll remove the unnecessary code now.

At the top of the medic_example class definition, remove the values before OnBegin(). Your medic character will not wait to move to characters, and will instead follow them around when healing. You don't need the debug values for this example, and you'll use other objects to visualize when your medic heals characters.

In OnBegin(), after getting the character's interfaces in the first if statement, remove the code inside the then statement. Your medic character does not need to loop between points after spawning, and will instead patrol around their spawn point waiting for characters to heal.

Remove the DrawDebugLocation() and DrawDebugLookAt() functions. You won't use the debug values in this example, so you don't need the associated functions that use them either.

After removing the unneeded code, you can start to build your medic character.

At the top of the medic_example class definition, add the following values:

editable float HealingThreshold. This is the threshold of health characters must be under to receive healing.

Verse
 # The HP threshold a character must be at before healing them.
 @editable
 HealingThreshold:float = 50.0
# The HP threshold a character must be at before healing them. @editable HealingThreshold:float = 50.0
Add an editable float HealingDelay. This is the amount of time to wait between each instance of healing while healing characters. Change this depending on whether you want your medic to heal slower or faster.

Verse
 # The HP threshold a character must be at before healing them.
 @editable
 HealingThreshold:float = 50.0
    
 # How long to wait before healing characters
 @editable
 HealingDelay:float = 1.5
# The HP threshold a character must be at before healing them. @editable HealingThreshold:float = 50.0 # How long to wait before healing characters @editable HealingDelay:float = 1.5
An editable float HealingAmount. This is the amount of health to heal characters per healing instance. When your medic NPC heals a character, they will heal the character by a HealingAmount every HealingDelay seconds.

Verse
 # How long to wait before healing characters
 @editable
 HealingDelay:float = 1.5
    
 # How much to heal characters per healing instance
 @editable
 HealingAmount:float = 5.0        
# How long to wait before healing characters @editable HealingDelay:float = 1.5 # How much to heal characters per healing instance @editable HealingAmount:float = 5.0
An editable mutator zone HealVolume. This is the volume characters enter to receive healing. You'll use a mutator zone in this example because the mutator zone has an AgentEntersEvent which your medic can subscribe to and check for characters that might need healing.

Verse
 # How much to heal characters per healing instance
 @editable
 HealingAmount:float = 5.0
    
 # The volume characters enter to receive healing.
 @editable
 HealVolume:mutator_zone_device = mutator_zone_device{}
# How much to heal characters per healing instance @editable HealingAmount:float = 5.0 # The volume characters enter to receive healing. @editable HealVolume:mutator_zone_device = mutator_zone_device{}
An editable VFX spawner VFXSpawner. Visual feedback is important to know your code is working, so you'll use a VFX spawner to spawn effects when a character is being healed.

Verse
 # The volume characters enter to receive healing.
 @editable
 HealVolume:mutator_zone_device = mutator_zone_device{}
    
 # The VFX spawner to play VFX as characters are being healed.
 @editable
 VFXSpawner:vfx_spawner_device = vfx_spawner_device {}
# The volume characters enter to receive healing. @editable HealVolume:mutator_zone_device = mutator_zone_device{} # The VFX spawner to play VFX as characters are being healed. @editable VFXSpawner:vfx_spawner_device = vfx_spawner_device {}
A variable optional agent named AgentToFollow. This stores a reference to the character the medic should follow while healing them.

Verse
 # The VFX spawner to play VFX as characters are being healed.
 @editable
 VFXSpawner:vfx_spawner_device = vfx_spawner_device {}
    
 # The agent to follow while they're being healed
 var AgentToFollow:?agent = false
# The VFX spawner to play VFX as characters are being healed. @editable VFXSpawner:vfx_spawner_device = vfx_spawner_device {} # The agent to follow while they&#39;re being healed var AgentToFollow:?agent = false
A variable queue of agents named AgentsToHeal. If multiple characters need healing, your medic will heal characters based on the order they entered the HealVolume. You'll set up the queue code in the next step. For more information on the queue data structure, see stacks and queues in verse.

Verse
 # The agent to follow while they're being healed
 var AgentToFollow:?agent = false
 
 # The queue of agents to heal in the case of multiple agents entering the heal volume.
 var AgentsToHeal<public>:queue(agent) = queue(agent){}
# The agent to follow while they&#39;re being healed var AgentToFollow:?agent = false # The queue of agents to heal in the case of multiple agents entering the heal volume. var AgentsToHeal&lt;public&gt;:queue(agent) = queue(agent){}
A variable float UpdateRateSeconds. This is the amount of time to wait between updating the position of the HealVolume and VFXSpawner.

Verse
 # The queue of agents to heal in the case of multiple agents entering the heal volume.
 var AgentsToHeal<public>:queue(agent) = queue(agent){}
 
 # Used to specify how quickly to update the position of the HealVolume and VFXSpawner
 UpdateRateSeconds<private>:float = 0.1
# The queue of agents to heal in the case of multiple agents entering the heal volume. var AgentsToHeal&lt;public&gt;:queue(agent) = queue(agent){} # Used to specify how quickly to update the position of the HealVolume and VFXSpawner UpdateRateSeconds&lt;private&gt;:float = 0.1
To implement the AgentsToHeal queue, you'll use the code provided at the end of this step.

Back In Verse Explorer, right-click on your project name and choose Add new Verse file to project to open the Create Verse Script window.

Add New Verse File To Project
In the Create Verse Script window, click Verse Class to select it as your script.

Name your Verse class by changing the text in the Class Name field to queue.

Click Create to create the Verse file.

In Verse Explorer, double-click the name of your Verse file to open it in Visual Studio Code.

Replace the code in your queue file with the following code. This code implements a generic queue of type type using a list data structure. This is an example of a parametric type since the queue implementation will work regardless of the type you create it from. In your example, you'll be using a queue of characters, so your queue definition in medic_example will be queue(agent).

Verse
 list(t:type) := class:
     Data:t
     Next:?list(t)
 
 queue<public>(t:type) := class<internal>:
     Elements<internal>:?list(t) = false
     Size<public>:int = 0
 
     Enqueue<public>(NewElement:t):queue(t) =
         queue(t):
             Elements := option:
                 list(t):
                     Data := NewElement
                     Next := Elements
             Size := Size + 1
 
     Dequeue<public>()<decides><transacts>:tuple(queue(t), t) =
         List := Elements?
         (queue(t){Elements := List.Next, Size := Size - 1}, List.Data)
 
     Front<public>()<decides><transacts>:t = Elements?.Data
 
 CreateQueue<public><constructor>(InData:t where t:type) := queue(t):
     Elements := option:
         list(t):
             Data := InData
             Next := false
     Size := 1
list(t:type) := class: Data:t Next:?list(t) queue<public>(t:type) := class<internal>: Elements<internal>:?list(t) = false Size<public>:int = 0 Enqueue<public>(NewElement:t):queue(t) = queue(t): Elements := option: list(t): Data := NewElement Next := Elements Size := Size + 1 Dequeue<public>()<decides><transacts>:tuple(queue(t), t) = List := Elements? (queue(t){Elements := List.Next, Size := Size - 1}, List.Data) Front<public>()<decides><transacts>:t = Elements?.Data CreateQueue<public><constructor>(InData:t where t:type) := queue(t): Elements := option: list(t): Data := InData Next := false Size := 1
Organizing your Verse scripts into distinct folders can help with organization, as well as provide ways to easily reference commonly used files. As an example of this, you'll create a folder to store your NPC behaviors in this project. In Visual Studio Code, hit the New Folder button to create a new folder in your UEFN Project. Name the folder npc_behaviors. Then drag your medic_example Verse file into the new folder.

Your code in medic_example should now compile correctly.

Healing Characters Inside a Volume
When an injured character enters the HealVolume, your medic character should begin healing them if their health is less than the HealingThreshold. Once the character's health is above the HealingThreshold, your medic should stop healing that character, and move to the next character that needs healing. In the case of multiple characters, your medic should heal characters in the order they entered the HealVolume. Follow these steps to heal characters when they enter the HealVolume.

Back in your medic_example file, in OnBegin() after the then statement, start a loop. Inside the loop, get the result of the Dequeue() function from the AgentsToHeal queue and save it in a variable DequeueResult.

Verse
     then:
         loop:
             # Get the next agent in the queue to heal. If there is an agent to heal, heal them by calling AgentToHeal.
             # If there are no agents to heal, wait until an agent enters the HealVolume
             if:
                 DequeueResult := AgentsToHeal.Dequeue[]
then: loop: # Get the next agent in the queue to heal. If there is an agent to heal, heal them by calling AgentToHeal. # If there are no agents to heal, wait until an agent enters the HealVolume if: DequeueResult := AgentsToHeal.Dequeue[]
The DequeueResult variable is a tuple that returns both a copy of the AgentsToHeal queue with the first element removed and the agent at the front of the queue. Update AgentsToHeal by setting it to the first value in the tuple, and save the second value as the AgentToHeal.

Verse
     if:
         DequeueResult := AgentsToHeal.Dequeue[]
         set AgentsToHeal = DequeueResult(0)
         AgentToHeal := DequeueResult(1)
if: DequeueResult := AgentsToHeal.Dequeue[] set AgentsToHeal = DequeueResult(0) AgentToHeal := DequeueResult(1)
Once you have the agent to heal, you need to start healing them while they're in the HealVolume. You'll define a new function named HealCharacter() to handle this. Add a new function named HealCharacter() to the medic_example class definition. This function takes the AgentToHeal both the Navigatable and Focusable interfaces of the medic characters as function arguments. Add the <suspends> modifier to this function, since it needs to perform several asynchronous tasks when healing a character.

Verse
     # Heal the character, then wait a HealingDelayAmount of time.
     # Ends when the character's health reaches the HealingThreshold
     # or the character leaves the HealVolume.
     HealCharacter(AgentToHeal:agent, Navigatable:navigatable, Focusable:focus_interface)<suspends>:void=
# Heal the character, then wait a HealingDelayAmount of time. # Ends when the character&#39;s health reaches the HealingThreshold # or the character leaves the HealVolume. HealCharacter(AgentToHeal:agent, Navigatable:navigatable, Focusable:focus_interface)&lt;suspends&gt;:void=
In HealCharacter, check if the AgentToHeal is in the volume by calling IsInVolume[], and passing AgentToHeal as an argument. If the agent is in the volume, you can begin healing them. All healable agents implement the healthful interface, which is part of the agent's fort_character. Get the agent's fort_character and save it in a value CharacterToHeal.

Verse
     HealCharacter(AgentToHeal:agent, Navigatable:navigatable, Focusable:focus_interface)<suspends>:void=
         # Only heal the character if they are inside the HealVolume
         if:
             HealVolume.IsInVolume[AgentToHeal]
             CharacterToHeal := AgentToHeal.GetFortCharacter[]
HealCharacter(AgentToHeal:agent, Navigatable:navigatable, Focusable:focus_interface)&lt;suspends&gt;:void= # Only heal the character if they are inside the HealVolume if: HealVolume.IsInVolume[AgentToHeal] CharacterToHeal := AgentToHeal.GetFortCharacter[]
With the character ready to heal, you need to make sure your medic stays close to the character being healed. Create a navigation_target from AgentToHeal using MakeNavigationTarget and save it in a variable NavigationTarget. Then in a branch statement, call the NavigateTo() function using the NPC's navigatable interface to have your medic navigate to the AgentToHeal. Also in the branch function, call the MaintainFocus() function to make sure your medic focuses on the AgentToHeal. Using a branch statement in this context lets you run both NavigateTo() and MaintainFocus() asynchronously at the same time, and lets you run any code after your branch immediately. For more information on branch expressions, see the branch in Verse page.

Verse
     # Only heal the character if they are inside the HealVolume
     if:
         HealVolume.IsInVolume[AgentToHeal]
         CharacterToHeal := AgentToHeal.GetFortCharacter[]
     then:      
         Print("Character is in volume, starting healing")
         NavigationTarget := MakeNavigationTarget(AgentToHeal)
         branch:
             Navigatable.NavigateTo(NavigationTarget)
             Focusable.MaintainFocus(AgentToHeal)
# Only heal the character if they are inside the HealVolume if: HealVolume.IsInVolume[AgentToHeal] CharacterToHeal := AgentToHeal.GetFortCharacter[] then: Print(&quot;Character is in volume, starting healing&quot;) NavigationTarget := MakeNavigationTarget(AgentToHeal) branch: Navigatable.NavigateTo(NavigationTarget) Focusable.MaintainFocus(AgentToHeal)
Enable the VFXSpawner to play VFX as your medic heals a character. Then in a defer expression, disable the VFXSpawner. Because the code for disabling the VFXSpawner is in a defer expression, it won't run until the current scope exits. In this situation, it means that the code will only run when the function ends, so it is guaranteed to be the last thing that happens in the function. For more information on defer expressions, see the defer page.

Verse
     branch:
         Navigatable.NavigateTo(NavigationTarget)
         Focusable.MaintainFocus(AgentToHeal)
		    
     VFXSpawner.Enable()
		    
     defer:
         VFXSpawner.Disable()
branch: Navigatable.NavigateTo(NavigationTarget) Focusable.MaintainFocus(AgentToHeal) VFXSpawner.Enable() defer: VFXSpawner.Disable()
When healing the CharacterToHeal, healing should stop when one of two conditions happens. Either the character's health is healed past the HealingThreshold, or the character exits the HealVolume. To accomplish this, you'll use a race expression. Set up a race expression between a loop and an Await() on the HealVolume.AgentExitsEvent.

Verse
     branch:
         Navigatable.NavigateTo(NavigationTarget)
         Focusable.MaintainFocus(AgentToHeal)
     VFXSpawner.Enable()
     defer:
         VFXSpawner.Disable()
     race:
         loop:
         HealVolume.AgentExitsEvent.Await()
branch: Navigatable.NavigateTo(NavigationTarget) Focusable.MaintainFocus(AgentToHeal) VFXSpawner.Enable() defer: VFXSpawner.Disable() race: loop: HealVolume.AgentExitsEvent.Await()
Inside the loop, get the current health of the character using GetHealth() and save it in a value CurrentHealth. Then in an if statement, check if the CurrentHealth plus the HealingAmount is greater than the HealingThreshold. If so, your medic should stop healing and break out of the loop. However, if the character's current health is just a little less than the healing threshold, you want to heal them up to the healing threshold. Add a second if statement inside the first one that checks if CurrentHealth is less than the HealingThreshold. If so, set the character's health to the HealingThreshold.

Verse
     race:
         loop:
             CurrentHealth := CharacterToHeal.GetHealth()
             if(CurrentHealth + HealingAmount > HealingThreshold):
                 if (CurrentHealth < HealingThreshold):
                     CharacterToHeal.SetHealth(HealingThreshold)
                 PrintNPCB("Character has reached HealingThreshold, stopping healing")
                 break
         HealVolume.AgentExitsEvent.Await()
race: loop: CurrentHealth := CharacterToHeal.GetHealth() if(CurrentHealth + HealingAmount &gt; HealingThreshold): if (CurrentHealth &lt; HealingThreshold): CharacterToHeal.SetHealth(HealingThreshold) PrintNPCB(&quot;Character has reached HealingThreshold, stopping healing&quot;) break HealVolume.AgentExitsEvent.Await()
Otherwise if the CurrentHealth plus the HealingAmount is not greater than the HealingThreshold, set the character's health to the Current Health plus the HealingAmount.

Verse
     if(CurrentHealth + HealingAmount > HealingThreshold):
         if (CurrentHealth < HealingThreshold):
             CharacterToHeal.SetHealth(HealingThreshold)
         PrintNPCB("Character has reached HealingThreshold, stopping healing")
         break
     else:
         CharacterToHeal.SetHealth(CurrentHealth + HealingAmount)
if(CurrentHealth + HealingAmount &gt; HealingThreshold): if (CurrentHealth &lt; HealingThreshold): CharacterToHeal.SetHealth(HealingThreshold) PrintNPCB(&quot;Character has reached HealingThreshold, stopping healing&quot;) break else: CharacterToHeal.SetHealth(CurrentHealth + HealingAmount)
At the end of the loop, sleep for a HealingDelay amount of time. Without this sleep, characters will be healed every simulation update, so the HealingDelay will prevent them from being healed instantly. Your completed HealCharacter() code should look like the following.

Verse
     # Heal the character, then wait a HealingDelayAmount of time.
     # Ends when the character's health reaches the HealingThreshold
     # or the character leaves the HealVolume.
     HealCharacter(AgentToHeal:agent, Navigatable:navigatable, Focusable:focus_interface)<suspends>:void=
         # Only heal the character if they are inside the HealVolume
         if:
             HealVolume.IsInVolume[AgentToHeal]
             CharacterToHeal := AgentToHeal.GetFortCharacter[]
         then:
             Print("Character is in volume, starting healing")
             NavigationTarget := MakeNavigationTarget(AgentToHeal)
             branch:
                 Navigatable.NavigateTo(NavigationTarget)
                 Focusable.MaintainFocus(AgentToHeal)
             VFXSpawner.Enable()
             defer:
                 VFXSpawner.Disable()
             race:
                 loop:
                     CurrentHealth := CharacterToHeal.GetHealth()
                     if(CurrentHealth + HealingAmount > HealingThreshold):
                         if (CurrentHealth < HealingThreshold):
                             CharacterToHeal.SetHealth(HealingThreshold)
                         PrintNPCB("Character has reached HealingThreshold, stopping healing")
                         break
                     else:
                         CharacterToHeal.SetHealth(CurrentHealth + HealingAmount)
                     Sleep(HealingDelay)
                     HealVolume.AgentExitsEvent.Await()
# Heal the character, then wait a HealingDelayAmount of time. # Ends when the character's health reaches the HealingThreshold # or the character leaves the HealVolume. HealCharacter(AgentToHeal:agent, Navigatable:navigatable, Focusable:focus_interface)<suspends>:void= # Only heal the character if they are inside the HealVolume if: HealVolume.IsInVolume[AgentToHeal] CharacterToHeal := AgentToHeal.GetFortCharacter[] then: Print("Character is in volume, starting healing") NavigationTarget := MakeNavigationTarget(AgentToHeal) branch: Navigatable.NavigateTo(NavigationTarget) Focusable.MaintainFocus(AgentToHeal) VFXSpawner.Enable() defer: VFXSpawner.Disable() race: loop: CurrentHealth := CharacterToHeal.GetHealth() if(CurrentHealth + HealingAmount > HealingThreshold): if (CurrentHealth < HealingThreshold): CharacterToHeal.SetHealth(HealingThreshold) PrintNPCB("Character has reached HealingThreshold, stopping healing") break else: CharacterToHeal.SetHealth(CurrentHealth + HealingAmount) Sleep(HealingDelay) HealVolume.AgentExitsEvent.Await()
Back in OnBegin(), in the then expression inside of your loop, call HealCharacter() by passing the AgentToHeal, the Navigable interface, and the Focusable interface.

Verse
     if:
         DequeueResult := AgentsToHeal.Dequeue[]
         set AgentsToHeal = DequeueResult(0)
         AgentToHeal := DequeueResult(1)
     then:
         Print("Dequeued the next agent to heal")
         HealCharacter(AgentToHeal, Navigatable, Focusable)
if: DequeueResult := AgentsToHeal.Dequeue[] set AgentsToHeal = DequeueResult(0) AgentToHeal := DequeueResult(1) then: Print(&quot;Dequeued the next agent to heal&quot;) HealCharacter(AgentToHeal, Navigatable, Focusable)
Your medic will not always have a character to heal near them, and the Dequeue[] function will fail if there are no agents in the AgentsToHeal queue. To handle this, add an else statement to the end of the loop. Inside this if statement, call Sleep() for a HealingDelay amount of time, then Await() the HealVolume.AgentEntersEvent. This way your medic character will not endlessly call Dequeue[] on the AgentsToHeal queue, and will instead wait for a new character to enter the `HealVolume before restarting the loop. Your completed loop should look like the following.

Verse
     loop:
         # Get the next agent in the queue to heal. If there is an agent to heal, heal them by calling AgentToHeal.
         # If there are no agents to heal, wait until an agent enters the HealVolume
         if:
             DequeueResult := AgentsToHeal.Dequeue[]
             set AgentsToHeal = DequeueResult(0)
             AgentToHeal := DequeueResult(1)
         then:
             Print("Dequeued the next agent to heal")
             HealCharacter(AgentToHeal, Navigatable, Focusable)
         else:
             Print("AgentsToHeal is empty!")
             Sleep(HealingDelay)
             HealVolume.AgentEntersEvent.Await()
loop: # Get the next agent in the queue to heal. If there is an agent to heal, heal them by calling AgentToHeal. # If there are no agents to heal, wait until an agent enters the HealVolume if: DequeueResult := AgentsToHeal.Dequeue[] set AgentsToHeal = DequeueResult(0) AgentToHeal := DequeueResult(1) then: Print("Dequeued the next agent to heal") HealCharacter(AgentToHeal, Navigatable, Focusable) else: Print("AgentsToHeal is empty!") Sleep(HealingDelay) HealVolume.AgentEntersEvent.Await()
Tracking when Characters are in the Heal Volume
To know when characters enter or exit the HealVolume, you'll subscribe both the HealVolume's AgentEntersEvent and AgentExitsEvent to new functions.

Add a new function named OnAgentEnters() to the medic_example class definition. This function takes the agent who just entered the HealVolume, and enqueues them in the AgentsToHeal queue.

Verse
     OnAgentEnters(EnteredAgent:agent):void=
             Print("Agent entered the heal volume")
OnAgentEnters(EnteredAgent:agent):void= Print(&quot;Agent entered the heal volume&quot;)
In OnAgentEnters(), check that the agent in the volume is not the medic character. If so, set the AgentsToHeal queue to the result of calling Enqueue[] with the EnteredAgent. Your completed OnAgentEnters() function should look like the following:

Verse
    OnAgentEnters(EnteredAgent:agent):void=
        Print("Agent entered the heal volume")
        if (EnteredAgent <> GetAgent[]):
            set AgentsToHeal = AgentsToHeal.Enqueue(EnteredAgent)
OnAgentEnters(EnteredAgent:agent):void= Print(&quot;Agent entered the heal volume&quot;) if (EnteredAgent &lt;&gt; GetAgent[]): set AgentsToHeal = AgentsToHeal.Enqueue(EnteredAgent)
When an agent exits the HealVolume, you don't need to remove them from the AgentsToHeal queue. This is because the loop in OnBegin() already calls Dequeue[] in a loop. However, you may want to run code when an agent exits the volume in your examples, so you'll set up a function for this now. Add a new function named OnAgentExits() to the medic_example class definition.

Verse
     OnAgentExits(ExitAgent:agent):void=
         Print("Agent exited the heal volume")
OnAgentExits(ExitAgent:agent):void= Print(&quot;Agent exited the heal volume&quot;)
In OnBegin(), subscribe the HealVolume's AgentEntersEvent and AgentExitsEvent to OnAgentEnters and OnAgentExits respectively. Since it should start disabled, this is a good place to call Disable() on the character spawner.

Verse
     OnBegin<override>()<suspends>:void=
         Print("Hello, AI!")
         VFXSpawner.Disable()
         HealVolume.AgentEntersEvent.Subscribe(OnAgentEnters)
         HealVolume.AgentExitsEvent.Subscribe(OnAgentExits)
OnBegin&lt;override&gt;()&lt;suspends&gt;:void= Print(&quot;Hello, AI!&quot;) VFXSpawner.Disable() HealVolume.AgentEntersEvent.Subscribe(OnAgentEnters) HealVolume.AgentExitsEvent.Subscribe(OnAgentExits)
Moving the Heal Volume with the Medic
When the medic character moves, the HealVolume needs to move with them to match their current position. The same is true for the VFXSpawner. To do this you'll use a new function DeviceFollowCharacter().

Add a new function named DeviceFollowCharacter() to the medic_example class definition. This function needs to run asynchronously to continuously update the device positions, so add the <suspends> modifier to it.

Verse
     DeviceFollowCharacter()<suspends>:void=
DeviceFollowCharacter()&lt;suspends&gt;:void=
Inside the DeviceFollowCharacter() function, get the fort_character of the medic by first getting the agent using GetAgent[], then calling GetFortCharater[].

Verse
     DeviceFollowCharacter()<suspends>:void=
         if:
             # Get the agent (AI Character) this behavior is associated with.
             Agent := GetAgent[]
             # Get the fort_character interface of the agent to access Fortnite character-specific behaviors, events, functions, and interfaces.
             Character := Agent.GetFortCharacter[]
DeviceFollowCharacter()&lt;suspends&gt;:void= if: # Get the agent (AI Character) this behavior is associated with. Agent := GetAgent[] # Get the fort_character interface of the agent to access Fortnite character-specific behaviors, events, functions, and interfaces. Character := Agent.GetFortCharacter[]
Now you need to continuously move the HealVolume and VFXSpawner to the Character's position. You'll do this by looping a MoveTo() on both devices. Start a loop and get the Character's transform and save it in a variable CharacterTransform.

Verse
     if:
         # Get the agent (AI Character) this behavior is associated with.
         Agent := GetAgent[]
         # Get the fort_character interface of the agent to access Fortnite character-specific behaviors, events, functions, and interfaces.
         Character := Agent.GetFortCharacter[]
     then:
         loop:
             CharacterTransform := Character.GetTransform()
if: # Get the agent (AI Character) this behavior is associated with. Agent := GetAgent[] # Get the fort_character interface of the agent to access Fortnite character-specific behaviors, events, functions, and interfaces. Character := Agent.GetFortCharacter[] then: loop: CharacterTransform := Character.GetTransform()
Call MoveTo() on both the VFXSpawner and the HealVolume, moving them to the CharacterTransform.Translation and CharacterTransform.Rotation. Set the duration to UpdateRateSeconds seconds. Finally, call Sleep() for an UpdateRateSeconds amount of time to prevent the devices from updating their position every simulation update. Updating the device position every simulation update can cause jittery movement on your devices. Your completed DeviceFollowCharacter() code should look like the following.

Verse
     DeviceFollowCharacter()<suspends>:void=
         if:
             # Get the agent (AI Character) this behavior is associated with.
             Agent := GetAgent[]
             # Get the fort_character interface of the agent to access Fortnite character-specific behaviors, events, functions, and interfaces.
             Character := Agent.GetFortCharacter[]
             then:
                 loop:
                     CharacterTransform := Character.GetTransform()
                     VFXSpawner.MoveTo(CharacterTransform.Translation, CharacterTransform.Rotation, UpdateRateSeconds)
                     HealVolume.MoveTo(CharacterTransform.Translation, CharacterTransform.Rotation, UpdateRateSeconds)
                     Sleep(UpdateRateSeconds)
DeviceFollowCharacter()<suspends>:void= if: # Get the agent (AI Character) this behavior is associated with. Agent := GetAgent[] # Get the fort_character interface of the agent to access Fortnite character-specific behaviors, events, functions, and interfaces. Character := Agent.GetFortCharacter[] then: loop: CharacterTransform := Character.GetTransform() VFXSpawner.MoveTo(CharacterTransform.Translation, CharacterTransform.Rotation, UpdateRateSeconds) HealVolume.MoveTo(CharacterTransform.Translation, CharacterTransform.Rotation, UpdateRateSeconds) Sleep(UpdateRateSeconds)
In OnBegin(), after the if statement where you save your character interfaces but before the loop, spawn an instance of DeviceFollowCharacter().

Adding your Character to the Level
Create a new NPC Character Definition named Medic. Click your new NPC character definition to open the NPC Character Definition screen.

In the NPC Character Definition screen, modify the following properties:

Under NPC Character Type, set Type to Guard. The guard interface lets you access guard-specific character functionality, such as events for when the guard is alerted or suspicious, and lets you hire guards to use as allies. Guards may also equip weapons, while Custom and Wildlife-type characters currently cannot. You can also change the name of your character under the Name tab.

Under NPC Character Behavior, set Behavior to Verse Behavior. Then set the NPC Behavior Script to medic_example. Your character will still have access to functionality from the guard interface, but will use your Verse script to decide what to do during OnBegin and OnEnd.

In the Modifiers tab, under Guard Spawn Modifier, click the Cosmetic tab to change your character's cosmetic appearance. You can choose from a preexisting cosmetic, or enable Character Cosmetic Retargeting to use a custom model. Note that only guards and Custom-type characters can use character cosmetic retargeting, while wildlife cannot. For more information on character modifiers and which ones apply to different character types, see the Character Definition page.

Save your NPC character definition. In the Content Browser, drag your NPC character definition into the level. This will automatically create a new character spawner and assign your NPC character definition to it.


Drag one mutator zone and one VFX spawner device into the level.

Select your character spawner. In the Outliner, under User Options:

Set AIBehavior Script override to your medic_example script. Overriding the `AIBehavior Script in the outliner allows you to reference devices in the level, and you'll need this functionality to assign your HealVolume and VFXSpawner.

Set HealVolume to the mutator zone, and VFXSpawner to the VFX spawner you placed in the level.

Character Spawner Settings
Select your mutator zone. In the Outliner, under User Options, set Zone Visible During Game to True. This will help you visualize where the HealVolume is, and how it moves with the medic character.

Select your VFX Spawner. In the Outliner, under User Options, set Visual Effect to an effect of your choice. This example uses the Bubbles effect to convey healing, but you might want to use something different, such as fireworks or sparks. Change the visual effect to suit the needs of your character.

Click Launch Session in the UEFN toolbar to playtest your level. When you playtest, your character should heal injured characters who enter the mutator zone. When healing a character, VFX should play and the medic should follow and focus on the character being healed.


Complete Script
The following is a complete script for an NPC Character that heals characters whose HP is under a certain threshold.

medic_example.verse
Verse
using { /Fortnite.com/AI }
using { /Fortnite.com/Characters }
using { /Fortnite.com/Devices }
using { /Verse.org/Colors }
using { /Verse.org/Random }
using { /Verse.org/Simulation }
using { /UnrealEngine.com/Temporary/Diagnostics }
using { /UnrealEngine.com/Temporary/SpatialMath }
 
# A Verse-authored NPC Behavior that can be used within an NPC Definition or a Character Spawner device's Behavior Script Override.
medic_example<public> := class(npc_behavior):
    # The HP threshold a character must be at before healing them.
    @editable
    HealingThreshold:float = 50.0
 
    # How long to wait before healing characters
    @editable
    HealingDelay:float = 1.5
 
    # How much to heal characters per healing instance
    @editable
    HealingAmount:float = 5.0
 
    # The volume characters enter to receive healing.
    @editable
    HealVolume:mutator_zone_device = mutator_zone_device{}
 
    # The VFX spawner to play VFX as characters are being healed.
    @editable
    VFXSpawner:vfx_spawner_device = vfx_spawner_device {}
 
    # The agent to follow while they're being healed
    var AgentToFollow:?agent = false
 
    # The queue of agents to heal in the case of multiple agents entering the heal volume.
    var AgentsToHeal<public>:queue(agent) = queue(agent){}
 
    # Used to specify how quickly to update the position of the HealVolume and VFXSpawner
    UpdateRateSeconds<private>:float = 0.1
 
    OnBegin<override>()<suspends>:void=
        VFXSpawner.Disable()
        HealVolume.AgentEntersEvent.Subscribe(OnAgentEnters)
        HealVolume.AgentExitsEvent.Subscribe(OnAgentExits)
 
        if:
 
            # Get the agent (AI Character) this behavior is associated with.
            Agent := GetAgent[]
 
            # Get the fort_character interface of the agent to access Fortnite character-specific behaviors, events, functions, and interfaces.
            Character := Agent.GetFortCharacter[]
 
            # Get the navigatable interface of the character to set specific targets for the character to travel to.
            Navigatable := Character.GetNavigatable[]
 
            # Get the focus_interface of the character to set specific targets to focus on after traveling to them.
            Focusable := Character.GetFocusInterface[]
 
        then:
            # Set the HealVolume and VFXSpawner to continuously follow the NPC Character
            spawn{DeviceFollowCharacter()}
            loop:
                # Get the next agent in the queue to heal. If there is an agent to heal, heal them by calling AgentToHeal.
                # If there are no agents to heal, wait until an agent enters the HealVolume
                if:
                    DequeueResult := AgentsToHeal.Dequeue[]
                    set AgentsToHeal = DequeueResult(0)
                    AgentToHeal := DequeueResult(1)
                then:
                    PrintNPCB("Dequeued the next agent to heal")
                    HealCharacter(AgentToHeal, Navigatable, Focusable)
                else:
                    PrintNPCB("AgentsToHeal is empty!")
                    Sleep(HealingDelay)
                    HealVolume.AgentEntersEvent.Await()
        else:
            # If code falls here something failed when gathering the agent and its interfaces
            PrintNPCB( "Error in NPC Behavior Script on NPC Setup",
                ?Duration := 6.0,
                ?TextColor := NamedColors.Red )
 
    # Heal the character, then wait a HealingDelayAmount of time.
    # Ends when the character's health reaches the HealingThreshold
    # or the character leaves the HealVolume.
    HealCharacter(AgentToHeal:agent, Navigatable:navigatable, Focusable:focus_interface)<suspends>:void=
 
        # Only heal the character if they are inside the HealVolume
        if:
            HealVolume.IsInVolume[AgentToHeal]
            CharacterToHeal := AgentToHeal.GetFortCharacter[]
        then:
            PrintNPCB("Character is in volume, starting healing")
            NavigationTarget := MakeNavigationTarget(AgentToHeal)
            branch:
                Navigatable.NavigateTo(NavigationTarget)
                Focusable.MaintainFocus(AgentToHeal)
            VFXSpawner.Enable()
            defer:
                VFXSpawner.Disable()
            race:
                loop:
                    CurrentHealth := CharacterToHeal.GetHealth()
                    if(CurrentHealth + HealingAmount > HealingThreshold):
                        if (CurrentHealth < HealingThreshold):
                            CharacterToHeal.SetHealth(HealingThreshold)
                        PrintNPCB("Character has reached HealingThreshold, stopping healing")
                        break
                    else:
                        CharacterToHeal.SetHealth(CurrentHealth + HealingAmount)
                    Sleep(HealingDelay)
                HealVolume.AgentExitsEvent.Await()
 
    # Sets the HealVolume and VFXSpawner to continuously follow the character by looping
    # MoveTo onto the character's position.
    DeviceFollowCharacter()<suspends>:void=
        if:
            # Get the agent (AI Character) this behavior is associated with.
            Agent := GetAgent[]
 
            # Get the fort_character interface of the agent to access Fortnite character-specific behaviors, events, functions, and interfaces.
            Character := Agent.GetFortCharacter[]
        then:
            # Loop MoveTo on the HealVolume and VFXSpawner to match their position to the
            # NPC Character
            loop:
                CharacterTransform := Character.GetTransform()
                VFXSpawner.MoveTo(CharacterTransform.Translation, CharacterTransform.Rotation, UpdateRateSeconds)
                HealVolume.MoveTo(CharacterTransform.Translation, CharacterTransform.Rotation, UpdateRateSeconds)
                Sleep(UpdateRateSeconds)
 
    # When an agent enters the HealVolume, add them to the
    # AgentsToHeal queue if they are not the NPC Character.
    OnAgentEnters(EnteredAgent:agent):void=
        PrintNPCB("Agent entered the heal volume")
        if (EnteredAgent <> GetAgent[]):
            set AgentsToHeal = AgentsToHeal.Enqueue(EnteredAgent)
 
    # When an agent exits the HealVolume, PrintNPCB to the log
    OnAgentExits(ExitAgent:agent):void=
        PrintNPCB("Agent exited the heal volume")
 
    # Custom wrapper that provides a default duration and color.
    PrintNPCB(Msg:string,?Duration:float = 3.0, ?TextColor:color = NamedColors.Green):void =
        Print("[new_npc_behavior] {Msg}", ?Color := TextColor, ?Duration := Duration)
 
    # This function runs when the NPC is despawned or eliminated from the world.
    OnEnd<override>():void =
        if(Agent := GetAgent[]):
            Print(medic_example_message_module.OnEndMessage(Agent))
        else:
            PrintNPCB("OnEnd")
using { /Fortnite.com/AI } using { /Fortnite.com/Characters } using { /Fortnite.com/Devices } using { /Verse.org/Colors } using { /Verse.org/Random } using { /Verse.org/Simulation } using { /UnrealEngine.com/Temporary/Diagnostics } using { /UnrealEngine.com/Temporary/SpatialMath } # A Verse-authored NPC Behavior that can be used within an NPC Definition or a Character Spawner device's Behavior Script Override. medic_example<public> := class(npc_behavior): # The HP threshold a character must be at before healing them. @editable HealingThreshold:float = 50.0 # How long to wait before healing characters @editable HealingDelay:float = 1.5 # How much to heal characters per healing instance @editable HealingAmount:float = 5.0 # The volume characters enter to receive healing. @editable HealVolume:mutator_zone_device = mutator_zone_device{} # The VFX spawner to play VFX as characters are being healed. @editable VFXSpawner:vfx_spawner_device = vfx_spawner_device {} # The agent to follow while they're being healed var AgentToFollow:?agent = false # The queue of agents to heal in the case of multiple agents entering the heal volume. var AgentsToHeal<public>:queue(agent) = queue(agent){} # Used to specify how quickly to update the position of the HealVolume and VFXSpawner UpdateRateSeconds<private>:float = 0.1 OnBegin<override>()<suspends>:void= VFXSpawner.Disable() HealVolume.AgentEntersEvent.Subscribe(OnAgentEnters) HealVolume.AgentExitsEvent.Subscribe(OnAgentExits) if: # Get the agent (AI Character) this behavior is associated with. Agent := GetAgent[] # Get the fort_character interface of the agent to access Fortnite character-specific behaviors, events, functions, and interfaces. Character := Agent.GetFortCharacter[] # Get the navigatable interface of the character to set specific targets for the character to travel to. Navigatable := Character.GetNavigatable[] # Get the focus_interface of the character to set specific targets to focus on after traveling to them. Focusable := Character.GetFocusInterface[] then: # Set the HealVolume and VFXSpawner to continuously follow the NPC Character spawn{DeviceFollowCharacter()} loop: # Get the next agent in the queue to heal. If there is an agent to heal, heal them by calling AgentToHeal. # If there are no agents to heal, wait until an agent enters the HealVolume if: DequeueResult := AgentsToHeal.Dequeue[] set AgentsToHeal = DequeueResult(0) AgentToHeal := DequeueResult(1) then: PrintNPCB("Dequeued the next agent to heal") HealCharacter(AgentToHeal, Navigatable, Focusable) else: PrintNPCB("AgentsToHeal is empty!") Sleep(HealingDelay) HealVolume.AgentEntersEvent.Await() else: # If code falls here something failed when gathering the agent and its interfaces PrintNPCB( "Error in NPC Behavior Script on NPC Setup", ?Duration := 6.0, ?TextColor := NamedColors.Red ) # Heal the character, then wait a HealingDelayAmount of time. # Ends when the character's health reaches the HealingThreshold # or the character leaves the HealVolume. HealCharacter(AgentToHeal:agent, Navigatable:navigatable, Focusable:focus_interface)<suspends>:void= # Only heal the character if they are inside the HealVolume if: HealVolume.IsInVolume[AgentToHeal] CharacterToHeal := AgentToHeal.GetFortCharacter[] then: PrintNPCB("Character is in volume, starting healing") NavigationTarget := MakeNavigationTarget(AgentToHeal) branch: Navigatable.NavigateTo(NavigationTarget) Focusable.MaintainFocus(AgentToHeal) VFXSpawner.Enable() defer: VFXSpawner.Disable() race: loop: CurrentHealth := CharacterToHeal.GetHealth() if(CurrentHealth + HealingAmount > HealingThreshold): if (CurrentHealth < HealingThreshold): CharacterToHeal.SetHealth(HealingThreshold) PrintNPCB("Character has reached HealingThreshold, stopping healing") break else: CharacterToHeal.SetHealth(CurrentHealth + HealingAmount) Sleep(HealingDelay) HealVolume.AgentExitsEvent.Await() # Sets the HealVolume and VFXSpawner to continuously follow the character by looping # MoveTo onto the character's position. DeviceFollowCharacter()<suspends>:void= if: # Get the agent (AI Character) this behavior is associated with. Agent := GetAgent[] # Get the fort_character interface of the agent to access Fortnite character-specific behaviors, events, functions, and interfaces. Character := Agent.GetFortCharacter[] then: # Loop MoveTo on the HealVolume and VFXSpawner to match their position to the # NPC Character loop: CharacterTransform := Character.GetTransform() VFXSpawner.MoveTo(CharacterTransform.Translation, CharacterTransform.Rotation, UpdateRateSeconds) HealVolume.MoveTo(CharacterTransform.Translation, CharacterTransform.Rotation, UpdateRateSeconds) Sleep(UpdateRateSeconds) # When an agent enters the HealVolume, add them to the # AgentsToHeal queue if they are not the NPC Character. OnAgentEnters(EnteredAgent:agent):void= PrintNPCB("Agent entered the heal volume") if (EnteredAgent <> GetAgent[]): set AgentsToHeal = AgentsToHeal.Enqueue(EnteredAgent) # When an agent exits the HealVolume, PrintNPCB to the log OnAgentExits(ExitAgent:agent):void= PrintNPCB("Agent exited the heal volume") # Custom wrapper that provides a default duration and color. PrintNPCB(Msg:string,?Duration:float = 3.0, ?TextColor:color = NamedColors.Green):void = Print("[new_npc_behavior] {Msg}", ?Color := TextColor, ?Duration := Duration) # This function runs when the NPC is despawned or eliminated from the world. OnEnd<override>():void = if(Agent := GetAgent[]): Print(medic_example_message_module.OnEndMessage(Agent)) else: PrintNPCB("OnEnd")
queue.verse
Verse
list(t:type) := class:
    Data:t
    Next:?list(t)
 
queue<public>(t:type) := class<internal>:
    Elements<internal>:?list(t) = false
    Size<public>:int = 0
 
    Enqueue<public>(NewElement:t):queue(t) =
        queue(t):
            Elements := option:
                list(t):
                    Data := NewElement
                    Next := Elements
            Size := Size + 1
 
    Dequeue<public>()<decides><transacts>:tuple(queue(t), t) =
        List := Elements?
        (queue(t){Elements := List.Next, Size := Size - 1}, List.Data)
 
    Front<public>()<decides><transacts>:t = Elements?.Data
 
CreateQueue<public><constructor>(InData:t where t:type) := queue(t):
    Elements := option:
        list(t):
            Data := InData
            Next := false
    Size := 1
list(t:type) := class: Data:t Next:?list(t) queue<public>(t:type) := class<internal>: Elements<internal>:?list(t) = false Size<public>:int = 0 Enqueue<public>(NewElement:t):queue(t) = queue(t): Elements := option: list(t): Data := NewElement Next := Elements Size := Size + 1 Dequeue<public>()<decides><transacts>:tuple(queue(t), t) = List := Elements? (queue(t){Elements := List.Next, Size := Size - 1}, List.Data) Front<public>()<decides><transacts>:t = Elements?.Data CreateQueue<public><constructor>(InData:t where t:type) := queue(t): Elements := option: list(t): Data := InData Next := false Size := 1
On Your Own
By completing this guide, you've learned how to create a medic character that automatically heals characters under a certain threshold. Using what you've learned, try to create your own medic character with their own special behaviors.

Can you create a medic who swaps between damaging and healing volumes based on whether an enemy is in the volume?

How about a medic who uses a depletable resource to heal characters? How would the medic restore this resource? Could they restore it over time, or could they restore it by attacking enemies?

NPC Types
Learn about the different types of NPCs and how each of them works.

NPC Types
NPCs in UEFN fall into several groups, each with their own rules and behaviors that are native to their character type. All fortnite characters implement the fort_character interface which grants them bespoke base behaviors, such as the ability to be damaged and healed.

When creating your own NPCs using the NPC Definition, selecting an NPC Type will grant the NPCs the base behaviors from that character type. As a base, all NPC Types inherit the fort_character and AI behaviors. Guard-type NPCs will inherit behaviors from the guard class, and Wildlife-type NPCs will inherit from the wildlife class. Custom-type NPCs do not inherit any extra behaviors.

NPC Types
This section covers the various types of NPCs, and the behaviors native to each type.

Guard
Guard-type NPCs are humanoid NPCs that all share common rules. Guards may be assigned to teams, and patrol an area or a patrol path. Guards coordinate to attack enemies and spread info about enemy locations to other guards. Guards may be hired and will leash and protect players who hire them. Guards use the perception system, which allows you to control how well guards can perceive targets in the world around them using sight, sound, and touch.

When a guard spawns, it either begins idle or starts patrolling if the patrol option is enabled. When the guard detects a target, it begins to fill the suspicion meter. If the meter is filled, the guard enters the alert phase, otherwise, it returns to patrolling. While alert, the guard will continuously navigate to their target, attacking them if they’re in range. If the target is eliminated or escapes the guard, the guard will return to patrolling.

State	Description	Gif
Idle

Guard will stand idle. Guards are only idle when the patrol option is disabled.


Patrolling

Guard patrols randomly in a set area. If patrol paths are enabled, the guard will patrol along an assigned patrol path.


Hired

The guard will leash to the player who hired them and attempt to stay within a certain distance from them. While hired and within the leash radius, the guard will continue to detect and attack enemy targets.


Suspicious

When a target is in range, the guard begins to fill the suspicion meter, represented by the question mark (?) symbol above their head. The guard moves to the Alert stage when the suspicion meter is filled.


Alert

The guard has detected a target, indicated by the exclamation mark (!) symbol above their head. The guard will attempt to chase the target and attack when the target is in range.


Attacking

The guard actively attacks a target and will attempt to maneuver to avoid being hit.


Guards are a highly flexible NPC type that lend themselves to a ton of different gameplay situations. For example:

Guarding a capture point in a control point gamemode.

Escorting a VIP NPC or player.

Spawning waves of guards as part of a tower defense game.

Companions or quest-givers that can defend themselves as part of an RPG.

If you want NPCs that can fight, patrol, and work with the player, guards are a solid choice for your experiences.

Wildlife
Wildlife-type NPCs are non-humanoid NPCs that default to the Wildlife & Creatures team. Wildlife NPCs have significant differences between their types. For example, Wolves, Boars, and Raptors can be tamed and mounted, while Chickens cannot. Frogs and Chickens run away from enemies, while Raptors attack them.

When wildlife spawn, they begin to patrol an area around their spawn point. When wildlife detect a target, the action they take depends on their wildlife type. Different wildlife have both actions unique to each type and have general actions depending on whether the wildlife is predator or prey. Predators, such as the Raptor and Wolf, will charge their target and begin attacking them. Prey animals ,such as the Frog and Chicken, will generally run away from the target. Certain wildlife (the Raptor, Wolf, and Boar) can be tamed either by interacting with them while they are eating or by jumping onto their backs. When tamed, wildlife will join the team of the player who tamed them and follow them around. A maximum of three wildlife may be tamed by a player at any time.

The Raptor, Wolf, and Boar can also be mounted. When mounted, these NPCs act as vehicles for the player and will not take independent action. They will use the player's inputs for movement and only act independently when dismounted.

State	Description	Gif
Idle

The wildlife will patrol randomly in a set area.


Tamed

The wildlife will follow the player who tamed them and attempt to stay within a certain distance from them. While hired and within the follow radius, the wildlife will continue to detect and attack enemy targets.


Mounted

The wildlife will not take independent action and will use the player’s input for movement until dismounted.


Out of Energy

The wildlife is out of energy and cannot move or attack. After regenerating energy through waiting or being fed, the wildlife can move again.


Attacking

The wildlife is actively attacking a target and will attempt to find the quickest path to them.


Wildlife-type NPCs are useful when you want to populate your world with creatures, create animal companions for your players, or make open-world exploration more exciting through mounted riding and combat.

Custom
Custom-type NPCs do not implement base behavior and instead are reliant on NPC behavior scripts to drive their actions. This gives them a large amount of flexibility, and you can customize these NPCs to suit your game’s needs. For more information on NPC Behavior scripts and to learn how to create your own, check out NPC Behavior scripts.

AI module
Learn technical details about the AI module.

Module import path: /Fortnite.com/AI

Fortnite.com

AI

movement_types
Classes and Structs
Name	Description
navigation_target	
movement_type	
npc_behavior	
Inherit from this to create a custom NPC behavior. The npc_behavior can be defined for a character in a CharacterDefinition asset, or in a npc_spawner_device.

fort_target_info	
Information about a perceived target.

Interfaces
Name	Description
focus_interface	
fort_guard_actions	
Fortnite Guards AI actions management

fort_guard_perception	
Fortnite NPC perception management

fort_leashable	
fort_npc_actions	
Fortnite NPC AI actions management

fort_npc_perception	
Fortnite NPC perception management

navigatable	
Functions
Name	Description
MakeNavigationTarget	
Generate a navigation_target from any position

MakeNavigationTarget	
Generate a navigation_target from an agent

MakeNavigationTarget	
Generate a navigation_target from an entity

MakeNavigationTarget	
Create a navigation_target from a fort_target_info.

Enumerations
Name	Description
ai_action_result	
Result of an AI action

navigation_result	
Result of a navigation request

fort_guard_alert_level	
The different alert levels of a guard.

ai_action_result enumeration
Learn technical details about the ai_action_result enumeration.

Result of an AI action

 	 
Verse using statement	using { /Fortnite.com/AI }
Enumerators
The ai_action_result enumeration includes the following enumerators:

Name	Description
Success	
The action has been successfully executed

Failure	
The action has failed during its execution

Canceled	
The action has been canceled before completion

Disallowed	
The action was not allowed to start

focus_interface interface
Learn technical details about the focus_interface interface.

 	 
Verse using statement	using { /Fortnite.com/AI }
Members
This interface has functions, but no data members.

Functions
Function Name	Description
MaintainFocus	
Look At specified location. Will never complete unless interrupted.

MaintainFocus	
Look At specified Agent. Will never complete unless interrupted.

MaintainFocus function
Learn technical details about the MaintainFocus function.

Look At specified location. Will never complete unless interrupted.

 	 
Verse using statement	using { /Fortnite.com/AI }
MaintainFocus<public>(Location:vector3)<suspends>:void

Parameters
MaintainFocus takes the following parameters:

Name	Type	Description
Location	vector3	 
Attributes and Effects
The following attributes and effects determine how MaintainFocus behaves and how you can use it in your programs. For the complete list of attribute and effect specifiers, see the Specifiers Page.

Attribute	Meaning
public	The identifier is universally accessible. You can use this on modules, classes, interfaces, structs, enums, methods, and data.
Effect	Meaning
suspends	Indicates that the function is async. Creates an async context for the body of the function.

MaintainFocus function
Learn technical details about the MaintainFocus function.

Look At specified Agent. Will never complete unless interrupted.

 	 
Verse using statement	using { /Fortnite.com/AI }
MaintainFocus<public>(Agent:agent)<suspends>:void

Parameters
MaintainFocus takes the following parameters:

Name	Type	Description
Agent	agent	 
Attributes and Effects
The following attributes and effects determine how MaintainFocus behaves and how you can use it in your programs. For the complete list of attribute and effect specifiers, see the Specifiers Page.

Attribute	Meaning
public	The identifier is universally accessible. You can use this on modules, classes, interfaces, structs, enums, methods, and data.
Effect	Meaning
suspends	Indicates that the function is async. Creates an async context for the body of the function.

fort_guard_actions interface
Learn technical details about the fort_guard_actions interface.

Fortnite Guards AI actions management

 	 
Verse using statement	using { /Fortnite.com/AI }
Exposed Interfaces
This interface exposes the following interfaces:

Name	Description
fort_npc_actions	
Fortnite NPC AI actions management

Members
This interface has functions, but no data members.

Functions
Function Name	Description
RoamAround	
Roam around the current position. Use the fort_leashable_component to specify the radius, else will roam anywhere.

MoveInRangeToAttack	
Move in range to attack the current target

PlayRandomEmote	
Play a random emote from the character emotes bank

Revive	
Revive the specified target

Attack	
Attack the target

Attack function
Learn technical details about the Attack function.

Attack the target

 	 
Verse using statement	using { /Fortnite.com/AI }
Attack<public>(Target:fort_target_info)<suspends>:ai_action_result

Parameters
Attack takes the following parameters:

Name	Type	Description
Target	fort_target_info	 
Attributes and Effects
The following attributes and effects determine how Attack behaves and how you can use it in your programs. For the complete list of attribute and effect specifiers, see the Specifiers Page.

Attribute	Meaning
public	The identifier is universally accessible. You can use this on modules, classes, interfaces, structs, enums, methods, and data.
Effect	Meaning
suspends	Indicates that the function is async. Creates an async context for the body of the function.

MoveInRangeToAttack function
Learn technical details about the MoveInRangeToAttack function.

Move in range to attack the current target

 	 
Verse using statement	using { /Fortnite.com/AI }
MoveInRangeToAttack<public>()<suspends>:ai_action_result

Parameters
MoveInRangeToAttack does not take any parameters.

Attributes and Effects
The following attributes and effects determine how MoveInRangeToAttack behaves and how you can use it in your programs. For the complete list of attribute and effect specifiers, see the Specifiers Page.

Attribute	Meaning
public	The identifier is universally accessible. You can use this on modules, classes, interfaces, structs, enums, methods, and data.
Effect	Meaning
suspends	Indicates that the function is async. Creates an async context for the body of the function.

PlayRandomEmote function
Learn technical details about the PlayRandomEmote function.

Play a random emote from the character emotes bank

 	 
Verse using statement	using { /Fortnite.com/AI }
PlayRandomEmote<public>()<suspends>:ai_action_result

Parameters
PlayRandomEmote does not take any parameters.

Attributes and Effects
The following attributes and effects determine how PlayRandomEmote behaves and how you can use it in your programs. For the complete list of attribute and effect specifiers, see the Specifiers Page.

Attribute	Meaning
public	The identifier is universally accessible. You can use this on modules, classes, interfaces, structs, enums, methods, and data.
Effect	Meaning
suspends	Indicates that the function is async. Creates an async context for the body of the function.

Revive function
Learn technical details about the Revive function.

Revive the specified target

 	 
Verse using statement	using { /Fortnite.com/AI }
Revive<public>(Target:agent)<suspends>:ai_action_result

Parameters
Revive takes the following parameters:

Name	Type	Description
Target	agent	 
Attributes and Effects
The following attributes and effects determine how Revive behaves and how you can use it in your programs. For the complete list of attribute and effect specifiers, see the Specifiers Page.

Attribute	Meaning
public	The identifier is universally accessible. You can use this on modules, classes, interfaces, structs, enums, methods, and data.
Effect	Meaning
suspends	Indicates that the function is async. Creates an async context for the body of the function.

RoamAround function
Learn technical details about the RoamAround function.

Roam around the current position. Use the fort_leashable_component to specify the radius, else will roam anywhere.

 	 
Verse using statement	using { /Fortnite.com/AI }
RoamAround<public>(MovementType:movement_type)<suspends>:navigation_result

Parameters
RoamAround takes the following parameters:

Name	Type	Description
MovementType	movement_type	 
Attributes and Effects
The following attributes and effects determine how RoamAround behaves and how you can use it in your programs. For the complete list of attribute and effect specifiers, see the Specifiers Page.

Attribute	Meaning
public	The identifier is universally accessible. You can use this on modules, classes, interfaces, structs, enums, methods, and data.
Effect	Meaning
suspends	Indicates that the function is async. Creates an async context for the body of the function.

fort_guard_alert_level enumeration
Learn technical details about the fort_guard_alert_level enumeration.

The different alert levels of a guard.

 	 
Verse using statement	using { /Fortnite.com/AI }
Enumerators
The fort_guard_alert_level enumeration includes the following enumerators:

Name	Description
Unaware	
The guard has not detected any hostile target.

Suspicious	
The guard has seen a hostile target but hasn't identified it yet.

LostTarget	
The guard has identified a hostile target but can't see it any more.

Alerted	
The guard has identified a hostile target.

fort_guard_perception interface
Learn technical details about the fort_guard_perception interface.

Fortnite NPC perception management

 	 
Verse using statement	using { /Fortnite.com/AI }
Exposed Interfaces
This interface exposes the following interfaces:

Name	Description
fort_npc_perception	
Fortnite NPC perception management

Members
This interface has both data members and functions.

Data
Data Member Name	Type	Description
AlertLevelChangedEvent	listenable(payload)	
Event when the alert level of the guard has changed.

CurrentTargetChangedEvent	listenable(payload)	
Event when the current target has changed.

Functions
Function Name	Description
GetCurrentTargetInfo	
Get information about the current target.

GetAlertLevel	
Get the current alert level of the guard.

GetAlertLevel	
Get the current alert level of a target for the guard.

GetAlertLevel function
Learn technical details about the GetAlertLevel function.

Get the current alert level of the guard.

 	 
Verse using statement	using { /Fortnite.com/AI }
GetAlertLevel<public><experimental>()<reads>:fort_guard_alert_level

Parameters
GetAlertLevel does not take any parameters.

Attributes and Effects
The following attributes and effects determine how GetAlertLevel behaves and how you can use it in your programs. For the complete list of attribute and effect specifiers, see the Specifiers Page.

Attribute	Meaning
public	The identifier is universally accessible. You can use this on modules, classes, interfaces, structs, enums, methods, and data.
Effect	Meaning
reads	This effect indicates that the same inputs to the function may not always produce the same output. The behavior depends on factors external to the specified inputs, such as memory or the containing package version.

GetAlertLevel function
Learn technical details about the GetAlertLevel function.

Get the current alert level of a target for the guard.

 	 
Verse using statement	using { /Fortnite.com/AI }
GetAlertLevel<public><experimental>(Target:entity)<reads><decides>:fort_guard_alert_level

Parameters
GetAlertLevel takes the following parameters:

Name	Type	Description
Target	entity	 
Attributes and Effects
The following attributes and effects determine how GetAlertLevel behaves and how you can use it in your programs. For the complete list of attribute and effect specifiers, see the Specifiers Page.

Attribute	Meaning
public	The identifier is universally accessible. You can use this on modules, classes, interfaces, structs, enums, methods, and data.
Effect	Meaning
reads	This effect indicates that the same inputs to the function may not always produce the same output. The behavior depends on factors external to the specified inputs, such as memory or the containing package version.
decides	Indicates that the function can fail, and that calling this function is a failable expression. Function definitions with the decides effect must also have the transacts effect, which means the actions performed by this function can be rolled back (as if the actions were never performed), if there’s a failure anywhere in the function.

GetCurrentTargetInfo function
Learn technical details about the GetCurrentTargetInfo function.

Get information about the current target.

 	 
Verse using statement	using { /Fortnite.com/AI }
GetCurrentTargetInfo<public><experimental>()<reads><decides>:fort_target_info

Parameters
GetCurrentTargetInfo does not take any parameters.

Attributes and Effects
The following attributes and effects determine how GetCurrentTargetInfo behaves and how you can use it in your programs. For the complete list of attribute and effect specifiers, see the Specifiers Page.

Attribute	Meaning
public	The identifier is universally accessible. You can use this on modules, classes, interfaces, structs, enums, methods, and data.
Effect	Meaning
reads	This effect indicates that the same inputs to the function may not always produce the same output. The behavior depends on factors external to the specified inputs, such as memory or the containing package version.
decides	Indicates that the function can fail, and that calling this function is a failable expression. Function definitions with the decides effect must also have the transacts effect, which means the actions performed by this function can be rolled back (as if the actions were never performed), if there’s a failure anywhere in the function.

fort_leashable interface
Learn technical details about the fort_leashable interface.

 	 
Verse using statement	using { /Fortnite.com/AI }
Members
This interface has functions, but no data members.

Functions
Function Name	Description
SetLeashPosition	
Set custom leash position. 'InnerRadius' ranges from 0.0 to 20000.0 (in centimeters). 'OuterRadius' ranges from 0.0 to 20000.0 (in centimeters) and no less than 'InnerRadius'.

SetLeashAgent	
Set the agent to be the new center of the leash. 'InnerRadius' ranges from 0.0 to 20000.0 (in centimeters). 'OuterRadius' ranges from 0.0 to 20000.0 (in centimeters) and no less than 'InnerRadius'.

ClearLeash	
Removes the current leash.

ClearLeash function
Learn technical details about the ClearLeash function.

Removes the current leash.

 	 
Verse using statement	using { /Fortnite.com/AI }
ClearLeash<public>():void

Parameters
ClearLeash does not take any parameters.

Attributes and Effects
The following attributes determine how ClearLeash behaves and how you can use it in your programs. For the complete list of attribute and effect specifiers, see the Specifiers Page.

Attribute	Meaning
public	The identifier is universally accessible. You can use this on modules, classes, interfaces, structs, enums, methods, and data.

SetLeashAgent function
Learn technical details about the SetLeashAgent function.

Set the agent to be the new center of the leash. 'InnerRadius' ranges from 0.0 to 20000.0 (in centimeters). 'OuterRadius' ranges from 0.0 to 20000.0 (in centimeters) and no less than 'InnerRadius'.

 	 
Verse using statement	using { /Fortnite.com/AI }
SetLeashAgent<public>(Agent:agent, InnerRadius:float, OuterRadius:float):void

Parameters
SetLeashAgent takes the following parameters:

Name	Type	Description
Agent	agent	 
InnerRadius	float	 
OuterRadius	float	 
Attributes and Effects
The following attributes determine how SetLeashAgent behaves and how you can use it in your programs. For the complete list of attribute and effect specifiers, see the Specifiers Page.

Attribute	Meaning
public	The identifier is universally accessible. You can use this on modules, classes, interfaces, structs, enums, methods, and data.

SetLeashPosition function
Learn technical details about the SetLeashPosition function.

Set custom leash position. 'InnerRadius' ranges from 0.0 to 20000.0 (in centimeters). 'OuterRadius' ranges from 0.0 to 20000.0 (in centimeters) and no less than 'InnerRadius'.

 	 
Verse using statement	using { /Fortnite.com/AI }
SetLeashPosition<public>(Location:vector3, InnerRadius:float, OuterRadius:float):void

Parameters
SetLeashPosition takes the following parameters:

Name	Type	Description
Location	vector3	 
InnerRadius	float	 
OuterRadius	float	 
Attributes and Effects
The following attributes determine how SetLeashPosition behaves and how you can use it in your programs. For the complete list of attribute and effect specifiers, see the Specifiers Page.

Attribute	Meaning
public	The identifier is universally accessible. You can use this on modules, classes, interfaces, structs, enums, methods, and data.

fort_npc_actions interface
Learn technical details about the fort_npc_actions interface.

Fortnite NPC AI actions management

 	 
Verse using statement	using { /Fortnite.com/AI }
Exposed Interfaces
This interface exposes the following interfaces:

Name	Description
navigatable	
focus_interface	
Members
This interface has no members.

fort_npc_perception interface
Learn technical details about the fort_npc_perception interface.

Fortnite NPC perception management

 	 
Verse using statement	using { /Fortnite.com/AI }
Members
This interface has both data members and functions.

Data
Data Member Name	Type	Description
TargetAddedEvent	listenable(payload)	
Event when a target is added.

TargetInfoUpdatedEvent	listenable(payload)	
Event when the info about a target has been updated.

TargetRemovedEvent	listenable(payload)	
Event when a target was removed.

TargetSeenEvent	listenable(payload)	
Event when a target is seen. Sight sense must be active.

TargetHeardEvent	listenable(payload)	
Event when a target is heard. Hearing sense must be active.

TargetTouchedEvent	listenable(payload)	
Event when a target is touched. Touch sense must be active.

DetectedTargets	?[]fort_target_info	
Information about all detected targets.

Functions
Function Name	Description
GetLastKnownPosition	
Get the last known position of a target.

GetLastKnownPosition function
Learn technical details about the GetLastKnownPosition function.

Get the last known position of a target.

 	 
Verse using statement	using { /Fortnite.com/AI }
GetLastKnownPosition<public><experimental>(Target:entity)<reads><decides>:vector3

Parameters
GetLastKnownPosition takes the following parameters:

Name	Type	Description
Target	entity	 
Attributes and Effects
The following attributes and effects determine how GetLastKnownPosition behaves and how you can use it in your programs. For the complete list of attribute and effect specifiers, see the Specifiers Page.

Attribute	Meaning
public	The identifier is universally accessible. You can use this on modules, classes, interfaces, structs, enums, methods, and data.
Effect	Meaning
reads	This effect indicates that the same inputs to the function may not always produce the same output. The behavior depends on factors external to the specified inputs, such as memory or the containing package version.
decides	Indicates that the function can fail, and that calling this function is a failable expression. Function definitions with the decides effect must also have the transacts effect, which means the actions performed by this function can be rolled back (as if the actions were never performed), if there’s a failure anywhere in the function.

fort_target_info class
Learn technical details about the fort_target_info class.

Information about a perceived target.

 	 
Verse using statement	using { /Fortnite.com/AI }
Members
This class has data members, but no functions.

Data
Data Member Name	Type	Description
Target	entity	
The source of the detection stimuli.

HasLineOfSight	logic	
True if the target can be seen.

Attitude	team_attitude	
Attitude toward this target.

(InNPCBehavior:npc_behavior).GetEntity extension
Learn technical details about the (InNPCBehavior:npc_behavior).GetEntity extension.

Returns the entity for InNPCBehavior.

 	 
Verse using statement	using { /Fortnite.com/AI }
(InNPCBehavior:npc_behavior).GetEntity<native><public><experimental>()<reads><decides>:entity

Parameters
GetEntity takes the following parameters:

Name	Type	Description
InNPCBehavior	npc_behavior	 
Attributes and Effects
The following attributes and effects determine how GetEntity behaves and how you can use it in your programs. For the complete list of attribute and effect specifiers, see the Specifiers Page.

Attribute	Meaning
native	Indicates that the definition details of the element are implemented in C++. Verse definitions with the native specifier auto-generate C++ definitions that a developer can then fill out its implementation. You can use this specifier on classes, interfaces, enums, methods, and data.
public	The identifier is universally accessible. You can use this on modules, classes, interfaces, structs, enums, methods, and data.
Effect	Meaning
reads	This effect indicates that the same inputs to the function may not always produce the same output. The behavior depends on factors external to the specified inputs, such as memory or the containing package version.
decides	Indicates that the function can fail, and that calling this function is a failable expression. Function definitions with the decides effect must also have the transacts effect, which means the actions performed by this function can be rolled back (as if the actions were never performed), if there’s a failure anywhere in the function.

(InCharacter:fort_character).GetFocusInterface extension
Learn technical details about the (InCharacter:fort_character).GetFocusInterface extension.

Get the focus_interface interface for the specified character.

 	 
Verse using statement	using { /Fortnite.com/AI }
(InCharacter:fort_character).GetFocusInterface<native><public>()<transacts><decides>:focus_interface

Parameters
GetFocusInterface takes the following parameters:

Name	Type	Description
InCharacter	fort_character	 
Attributes and Effects
The following attributes and effects determine how GetFocusInterface behaves and how you can use it in your programs. For the complete list of attribute and effect specifiers, see the Specifiers Page.

Attribute	Meaning
native	Indicates that the definition details of the element are implemented in C++. Verse definitions with the native specifier auto-generate C++ definitions that a developer can then fill out its implementation. You can use this specifier on classes, interfaces, enums, methods, and data.
public	The identifier is universally accessible. You can use this on modules, classes, interfaces, structs, enums, methods, and data.
Effect	Meaning
transacts	This effect indicates that any actions performed by the function can be rolled back. The transacts effect is required any time a mutable variable (var) is written. You’ll be notified when you compile your code if the transacts effect was added to a function that can’t be rolled back. Note that this check is not done for functions with the native specifier.
decides	Indicates that the function can fail, and that calling this function is a failable expression. Function definitions with the decides effect must also have the transacts effect, which means the actions performed by this function can be rolled back (as if the actions were never performed), if there’s a failure anywhere in the function.

(InCharacter:fort_character).GetFortGuardActions extension
Learn technical details about the (InCharacter:fort_character).GetFortGuardActions extension.

Get the current fort_guard_actions interface for the specified character.

 	 
Verse using statement	using { /Fortnite.com/AI }
(InCharacter:fort_character).GetFortGuardActions<native><public><experimental>()<transacts><decides>:fort_guard_actions

Parameters
GetFortGuardActions takes the following parameters:

Name	Type	Description
InCharacter	fort_character	 
Attributes and Effects
The following attributes and effects determine how GetFortGuardActions behaves and how you can use it in your programs. For the complete list of attribute and effect specifiers, see the Specifiers Page.

Attribute	Meaning
native	Indicates that the definition details of the element are implemented in C++. Verse definitions with the native specifier auto-generate C++ definitions that a developer can then fill out its implementation. You can use this specifier on classes, interfaces, enums, methods, and data.
public	The identifier is universally accessible. You can use this on modules, classes, interfaces, structs, enums, methods, and data.
Effect	Meaning
transacts	This effect indicates that any actions performed by the function can be rolled back. The transacts effect is required any time a mutable variable (var) is written. You’ll be notified when you compile your code if the transacts effect was added to a function that can’t be rolled back. Note that this check is not done for functions with the native specifier.
decides	Indicates that the function can fail, and that calling this function is a failable expression. Function definitions with the decides effect must also have the transacts effect, which means the actions performed by this function can be rolled back (as if the actions were never performed), if there’s a failure anywhere in the function.

(InCharacter:fort_character).GetFortGuardPerception extension
Learn technical details about the (InCharacter:fort_character).GetFortGuardPerception extension.

Get the current fort_guard_perception interface for the specified character.

 	 
Verse using statement	using { /Fortnite.com/AI }
(InCharacter:fort_character).GetFortGuardPerception<native><public><experimental>()<transacts><decides>:fort_guard_perception

Parameters
GetFortGuardPerception takes the following parameters:

Name	Type	Description
InCharacter	fort_character	 
Attributes and Effects
The following attributes and effects determine how GetFortGuardPerception behaves and how you can use it in your programs. For the complete list of attribute and effect specifiers, see the Specifiers Page.

Attribute	Meaning
native	Indicates that the definition details of the element are implemented in C++. Verse definitions with the native specifier auto-generate C++ definitions that a developer can then fill out its implementation. You can use this specifier on classes, interfaces, enums, methods, and data.
public	The identifier is universally accessible. You can use this on modules, classes, interfaces, structs, enums, methods, and data.
Effect	Meaning
transacts	This effect indicates that any actions performed by the function can be rolled back. The transacts effect is required any time a mutable variable (var) is written. You’ll be notified when you compile your code if the transacts effect was added to a function that can’t be rolled back. Note that this check is not done for functions with the native specifier.
decides	Indicates that the function can fail, and that calling this function is a failable expression. Function definitions with the decides effect must also have the transacts effect, which means the actions performed by this function can be rolled back (as if the actions were never performed), if there’s a failure anywhere in the function.

(InCharacter:fort_character).GetFortLeashable extension
Learn technical details about the (InCharacter:fort_character).GetFortLeashable extension.

Get the current fort_leashable interface for the specified character.

 	 
Verse using statement	using { /Fortnite.com/AI }
(InCharacter:fort_character).GetFortLeashable<native><public>()<transacts><decides>:fort_leashable

Parameters
GetFortLeashable takes the following parameters:

Name	Type	Description
InCharacter	fort_character	 
Attributes and Effects
The following attributes and effects determine how GetFortLeashable behaves and how you can use it in your programs. For the complete list of attribute and effect specifiers, see the Specifiers Page.

Attribute	Meaning
native	Indicates that the definition details of the element are implemented in C++. Verse definitions with the native specifier auto-generate C++ definitions that a developer can then fill out its implementation. You can use this specifier on classes, interfaces, enums, methods, and data.
public	The identifier is universally accessible. You can use this on modules, classes, interfaces, structs, enums, methods, and data.
Effect	Meaning
transacts	This effect indicates that any actions performed by the function can be rolled back. The transacts effect is required any time a mutable variable (var) is written. You’ll be notified when you compile your code if the transacts effect was added to a function that can’t be rolled back. Note that this check is not done for functions with the native specifier.
decides	Indicates that the function can fail, and that calling this function is a failable expression. Function definitions with the decides effect must also have the transacts effect, which means the actions performed by this function can be rolled back (as if the actions were never performed), if there’s a failure anywhere in the function.

(InCharacter:fort_character).GetFortNPCActions extension
Learn technical details about the (InCharacter:fort_character).GetFortNPCActions extension.

Get the current fort_npc_actions interface for the specified character.

 	 
Verse using statement	using { /Fortnite.com/AI }
(InCharacter:fort_character).GetFortNPCActions<native><public><experimental>()<transacts><decides>:fort_npc_actions

Parameters
GetFortNPCActions takes the following parameters:

Name	Type	Description
InCharacter	fort_character	 
Attributes and Effects
The following attributes and effects determine how GetFortNPCActions behaves and how you can use it in your programs. For the complete list of attribute and effect specifiers, see the Specifiers Page.

Attribute	Meaning
native	Indicates that the definition details of the element are implemented in C++. Verse definitions with the native specifier auto-generate C++ definitions that a developer can then fill out its implementation. You can use this specifier on classes, interfaces, enums, methods, and data.
public	The identifier is universally accessible. You can use this on modules, classes, interfaces, structs, enums, methods, and data.
Effect	Meaning
transacts	This effect indicates that any actions performed by the function can be rolled back. The transacts effect is required any time a mutable variable (var) is written. You’ll be notified when you compile your code if the transacts effect was added to a function that can’t be rolled back. Note that this check is not done for functions with the native specifier.
decides	Indicates that the function can fail, and that calling this function is a failable expression. Function definitions with the decides effect must also have the transacts effect, which means the actions performed by this function can be rolled back (as if the actions were never performed), if there’s a failure anywhere in the function.

(InCharacter:fort_character).GetFortNPCPerception extension
Learn technical details about the (InCharacter:fort_character).GetFortNPCPerception extension.

Get the current fort_npc_perception interface for the specified character.

 	 
Verse using statement	using { /Fortnite.com/AI }
(InCharacter:fort_character).GetFortNPCPerception<native><public><experimental>()<transacts><decides>:fort_npc_perception

Parameters
GetFortNPCPerception takes the following parameters:

Name	Type	Description
InCharacter	fort_character	 
Attributes and Effects
The following attributes and effects determine how GetFortNPCPerception behaves and how you can use it in your programs. For the complete list of attribute and effect specifiers, see the Specifiers Page.

Attribute	Meaning
native	Indicates that the definition details of the element are implemented in C++. Verse definitions with the native specifier auto-generate C++ definitions that a developer can then fill out its implementation. You can use this specifier on classes, interfaces, enums, methods, and data.
public	The identifier is universally accessible. You can use this on modules, classes, interfaces, structs, enums, methods, and data.
Effect	Meaning
transacts	This effect indicates that any actions performed by the function can be rolled back. The transacts effect is required any time a mutable variable (var) is written. You’ll be notified when you compile your code if the transacts effect was added to a function that can’t be rolled back. Note that this check is not done for functions with the native specifier.
decides	Indicates that the function can fail, and that calling this function is a failable expression. Function definitions with the decides effect must also have the transacts effect, which means the actions performed by this function can be rolled back (as if the actions were never performed), if there’s a failure anywhere in the function.

(InCharacter:fort_character).GetNavigatable extension
Learn technical details about the (InCharacter:fort_character).GetNavigatable extension.

Get the navigatable interface for the specified character

 	 
Verse using statement	using { /Fortnite.com/AI }
(InCharacter:fort_character).GetNavigatable<native><public>()<transacts><decides>:navigatable

Parameters
GetNavigatable takes the following parameters:

Name	Type	Description
InCharacter	fort_character	 
Attributes and Effects
The following attributes and effects determine how GetNavigatable behaves and how you can use it in your programs. For the complete list of attribute and effect specifiers, see the Specifiers Page.

Attribute	Meaning
native	Indicates that the definition details of the element are implemented in C++. Verse definitions with the native specifier auto-generate C++ definitions that a developer can then fill out its implementation. You can use this specifier on classes, interfaces, enums, methods, and data.
public	The identifier is universally accessible. You can use this on modules, classes, interfaces, structs, enums, methods, and data.
Effect	Meaning
transacts	This effect indicates that any actions performed by the function can be rolled back. The transacts effect is required any time a mutable variable (var) is written. You’ll be notified when you compile your code if the transacts effect was added to a function that can’t be rolled back. Note that this check is not done for functions with the native specifier.
decides	Indicates that the function can fail, and that calling this function is a failable expression. Function definitions with the decides effect must also have the transacts effect, which means the actions performed by this function can be rolled back (as if the actions were never performed), if there’s a failure anywhere in the function.

(InAgent:agent).GetNPCBehavior extension
Learn technical details about the (InAgent:agent).GetNPCBehavior extension.

Returns the npc_behavior for InAgent.

 	 
Verse using statement	using { /Fortnite.com/AI }
(InAgent:agent).GetNPCBehavior<native><public>()<transacts><decides>:npc_behavior

Parameters
GetNPCBehavior takes the following parameters:

Name	Type	Description
InAgent	agent	 
Attributes and Effects
The following attributes and effects determine how GetNPCBehavior behaves and how you can use it in your programs. For the complete list of attribute and effect specifiers, see the Specifiers Page.

Attribute	Meaning
native	Indicates that the definition details of the element are implemented in C++. Verse definitions with the native specifier auto-generate C++ definitions that a developer can then fill out its implementation. You can use this specifier on classes, interfaces, enums, methods, and data.
public	The identifier is universally accessible. You can use this on modules, classes, interfaces, structs, enums, methods, and data.
Effect	Meaning
transacts	This effect indicates that any actions performed by the function can be rolled back. The transacts effect is required any time a mutable variable (var) is written. You’ll be notified when you compile your code if the transacts effect was added to a function that can’t be rolled back. Note that this check is not done for functions with the native specifier.
decides	Indicates that the function can fail, and that calling this function is a failable expression. Function definitions with the decides effect must also have the transacts effect, which means the actions performed by this function can be rolled back (as if the actions were never performed), if there’s a failure anywhere in the function.

MakeNavigationTarget function
Learn technical details about the MakeNavigationTarget function.

Generate a navigation_target from any position

 	 
Verse using statement	using { /Fortnite.com/AI }
MakeNavigationTarget<native><public>(Position:vector3):navigation_target

Parameters
MakeNavigationTarget takes the following parameters:

Name	Type	Description
Position	vector3	 
Attributes and Effects
The following attributes determine how MakeNavigationTarget behaves and how you can use it in your programs. For the complete list of attribute and effect specifiers, see the Specifiers Page.

Attribute	Meaning
native	Indicates that the definition details of the element are implemented in C++. Verse definitions with the native specifier auto-generate C++ definitions that a developer can then fill out its implementation. You can use this specifier on classes, interfaces, enums, methods, and data.
public	The identifier is universally accessible. You can use this on modules, classes, interfaces, structs, enums, methods, and data.

MakeNavigationTarget function
Learn technical details about the MakeNavigationTarget function.

Generate a navigation_target from an agent

 	 
Verse using statement	using { /Fortnite.com/AI }
MakeNavigationTarget<native><public>(Target:agent):navigation_target

Parameters
MakeNavigationTarget takes the following parameters:

Name	Type	Description
Target	agent	 
Attributes and Effects
The following attributes determine how MakeNavigationTarget behaves and how you can use it in your programs. For the complete list of attribute and effect specifiers, see the Specifiers Page.

Attribute	Meaning
native	Indicates that the definition details of the element are implemented in C++. Verse definitions with the native specifier auto-generate C++ definitions that a developer can then fill out its implementation. You can use this specifier on classes, interfaces, enums, methods, and data.
public	The identifier is universally accessible. You can use this on modules, classes, interfaces, structs, enums, methods, and data.

MakeNavigationTarget function
Learn technical details about the MakeNavigationTarget function.

Generate a navigation_target from an entity

 	 
Verse using statement	using { /Fortnite.com/AI }
MakeNavigationTarget<native><public><experimental>(Entity:entity)<decides>:navigation_target

Parameters
MakeNavigationTarget takes the following parameters:

Name	Type	Description
Entity	entity	 
Attributes and Effects
The following attributes and effects determine how MakeNavigationTarget behaves and how you can use it in your programs. For the complete list of attribute and effect specifiers, see the Specifiers Page.

Attribute	Meaning
native	Indicates that the definition details of the element are implemented in C++. Verse definitions with the native specifier auto-generate C++ definitions that a developer can then fill out its implementation. You can use this specifier on classes, interfaces, enums, methods, and data.
public	The identifier is universally accessible. You can use this on modules, classes, interfaces, structs, enums, methods, and data.
Effect	Meaning
decides	Indicates that the function can fail, and that calling this function is a failable expression. Function definitions with the decides effect must also have the transacts effect, which means the actions performed by this function can be rolled back (as if the actions were never performed), if there’s a failure anywhere in the function.

MakeNavigationTarget function
Learn technical details about the MakeNavigationTarget function.

Create a navigation_target from a fort_target_info.

 	 
Verse using statement	using { /Fortnite.com/AI }
MakeNavigationTarget<native><public><experimental>(TargetInfo:fort_target_info):navigation_target

Parameters
MakeNavigationTarget takes the following parameters:

Name	Type	Description
TargetInfo	fort_target_info	 
Attributes and Effects
The following attributes determine how MakeNavigationTarget behaves and how you can use it in your programs. For the complete list of attribute and effect specifiers, see the Specifiers Page.

Attribute	Meaning
native	Indicates that the definition details of the element are implemented in C++. Verse definitions with the native specifier auto-generate C++ definitions that a developer can then fill out its implementation. You can use this specifier on classes, interfaces, enums, methods, and data.
public	The identifier is universally accessible. You can use this on modules, classes, interfaces, structs, enums, methods, and data.

movement_type class
Learn technical details about the movement_type class.

 	 
Verse using statement	using { /Fortnite.com/AI }
Members
This class has no members.

movement_types module
Learn technical details about the movement_types module.

Module import path: /Fortnite.com/AI/movement_types

Fortnite.com

AI

movement_types

Data
Name	Description
Walking	 
Running

navigatable interface
Learn technical details about the navigatable interface.

 	 
Verse using statement	using { /Fortnite.com/AI }
Members
This interface has functions, but no data members.

Functions
Function Name	Description
GetCurrentDestination	
Return the current destination of the character

NavigateTo	
Navigate toward the specified target

StopNavigation	
Stop navigation

Wait	
Wait for a specific duration

SetMovementSpeedMultiplier	
Apply a multiplier on the movement speed (Multiplier is clamped between 0.5 and 2)

GetCurrentDestination function
Learn technical details about the GetCurrentDestination function.

Return the current destination of the character

 	 
Verse using statement	using { /Fortnite.com/AI }
GetCurrentDestination<public>()<transacts><decides>:vector3

Parameters
GetCurrentDestination does not take any parameters.

Attributes and Effects
The following attributes and effects determine how GetCurrentDestination behaves and how you can use it in your programs. For the complete list of attribute and effect specifiers, see the Specifiers Page.

Attribute	Meaning
public	The identifier is universally accessible. You can use this on modules, classes, interfaces, structs, enums, methods, and data.
Effect	Meaning
transacts	This effect indicates that any actions performed by the function can be rolled back. The transacts effect is required any time a mutable variable (var) is written. You’ll be notified when you compile your code if the transacts effect was added to a function that can’t be rolled back. Note that this check is not done for functions with the native specifier.
decides	Indicates that the function can fail, and that calling this function is a failable expression. Function definitions with the decides effect must also have the transacts effect, which means the actions performed by this function can be rolled back (as if the actions were never performed), if there’s a failure anywhere in the function.

NavigateTo function
Learn technical details about the NavigateTo function.

Navigate toward the specified target

 	 
Verse using statement	using { /Fortnite.com/AI }
NavigateTo<public>(Target:navigation_target, MovementType:movement_type, ReachRadius:float, AllowPartialPath:logic)<suspends>:navigation_result

Parameters
NavigateTo takes the following parameters:

Name	Type	Description
Target	navigation_target	 
MovementType	movement_type	 
ReachRadius	float	 
AllowPartialPath	logic	 
Attributes and Effects
The following attributes and effects determine how NavigateTo behaves and how you can use it in your programs. For the complete list of attribute and effect specifiers, see the Specifiers Page.

Attribute	Meaning
public	The identifier is universally accessible. You can use this on modules, classes, interfaces, structs, enums, methods, and data.
Effect	Meaning
suspends	Indicates that the function is async. Creates an async context for the body of the function.

SetMovementSpeedMultiplier function
Learn technical details about the SetMovementSpeedMultiplier function.

Apply a multiplier on the movement speed (Multiplier is clamped between 0.5 and 2)

 	 
Verse using statement	using { /Fortnite.com/AI }
SetMovementSpeedMultiplier<public>(Multiplier:float):void

Parameters
SetMovementSpeedMultiplier takes the following parameters:

Name	Type	Description
Multiplier	float	 
Attributes and Effects
The following attributes determine how SetMovementSpeedMultiplier behaves and how you can use it in your programs. For the complete list of attribute and effect specifiers, see the Specifiers Page.

Attribute	Meaning
public	The identifier is universally accessible. You can use this on modules, classes, interfaces, structs, enums, methods, and data.

StopNavigation function
Learn technical details about the StopNavigation function.

Stop navigation

 	 
Verse using statement	using { /Fortnite.com/AI }
StopNavigation<public>():void

Parameters
StopNavigation does not take any parameters.

Attributes and Effects
The following attributes determine how StopNavigation behaves and how you can use it in your programs. For the complete list of attribute and effect specifiers, see the Specifiers Page.

Attribute	Meaning
public	The identifier is universally accessible. You can use this on modules, classes, interfaces, structs, enums, methods, and data.

Wait function
Learn technical details about the Wait function.

Wait for a specific duration

 	 
Verse using statement	using { /Fortnite.com/AI }
Wait<public>(Duration:float)<suspends>:void

Parameters
Wait takes the following parameters:

Name	Type	Description
Duration	float	 
Attributes and Effects
The following attributes and effects determine how Wait behaves and how you can use it in your programs. For the complete list of attribute and effect specifiers, see the Specifiers Page.

Attribute	Meaning
public	The identifier is universally accessible. You can use this on modules, classes, interfaces, structs, enums, methods, and data.
Effect	Meaning
suspends	Indicates that the function is async. Creates an async context for the body of the function.

navigation_result enumeration
Learn technical details about the navigation_result enumeration.

Result of a navigation request

 	 
Verse using statement	using { /Fortnite.com/AI }
Enumerators
The navigation_result enumeration includes the following enumerators:

Name	Description
Reached	
The destination has been reached

PartiallyReached	
The destination has been partially reached (AllowPartialPath was used)

Interrupted	
Navigation has been interrupted before completion

Blocked	
The navigating agent is blocked

Unreachable	
The destination cannot be reached

navigation_target class
Learn technical details about the navigation_target class.

 	 
Verse using statement	using { /Fortnite.com/AI }
Members
This class has no members.

npc_behavior class
Learn technical details about the npc_behavior class.

Inherit from this to create a custom NPC behavior. The npc_behavior can be defined for a character in a CharacterDefinition asset, or in a npc_spawner_device.

 	 
Verse using statement	using { /Fortnite.com/AI }
Members
This class has functions, but no data members.

Functions
Function Name	Description
OnBegin	
This function is called when the NPC is added to the simulation.

OnEnd	
This function is called when the NPC is removed from the simulation.

GetAgent	
Returns the agent associated with this behavior.

GetAgent function
Learn technical details about the GetAgent function.

Returns the agent associated with this behavior.

 	 
Verse using statement	using { /Fortnite.com/AI }
GetAgent<native><public>()<transacts><decides>:agent

Parameters
GetAgent does not take any parameters.

Attributes and Effects
The following attributes and effects determine how GetAgent behaves and how you can use it in your programs. For the complete list of attribute and effect specifiers, see the Specifiers Page.

Attribute	Meaning
native	Indicates that the definition details of the element are implemented in C++. Verse definitions with the native specifier auto-generate C++ definitions that a developer can then fill out its implementation. You can use this specifier on classes, interfaces, enums, methods, and data.
public	The identifier is universally accessible. You can use this on modules, classes, interfaces, structs, enums, methods, and data.
Effect	Meaning
transacts	This effect indicates that any actions performed by the function can be rolled back. The transacts effect is required any time a mutable variable (var) is written. You’ll be notified when you compile your code if the transacts effect was added to a function that can’t be rolled back. Note that this check is not done for functions with the native specifier.
decides	Indicates that the function can fail, and that calling this function is a failable expression. Function definitions with the decides effect must also have the transacts effect, which means the actions performed by this function can be rolled back (as if the actions were never performed), if there’s a failure anywhere in the function.

OnBegin function
Learn technical details about the OnBegin function.

This function is called when the NPC is added to the simulation.

 	 
Verse using statement	using { /Fortnite.com/AI }
OnBegin<native_callable><public>()<suspends>:void

Parameters
OnBegin does not take any parameters.

Attributes and Effects
The following attributes and effects determine how OnBegin behaves and how you can use it in your programs. For the complete list of attribute and effect specifiers, see the Specifiers Page.

Attribute	Meaning
native_callable	Indicates that an instance method is both native (implemented in C++) and may be called by other C++ code. You can see this specifier used on an instance method. This specifier doesn’t propagate to subclasses and so you don’t need to add it to a definition when overriding a method that has this specifier.
public	The identifier is universally accessible. You can use this on modules, classes, interfaces, structs, enums, methods, and data.
Effect	Meaning
suspends	Indicates that the function is async. Creates an async context for the body of the function.

OnEnd function
Learn technical details about the OnEnd function.

This function is called when the NPC is removed from the simulation.

 	 
Verse using statement	using { /Fortnite.com/AI }
OnEnd<native_callable><public>():void

Parameters
OnEnd does not take any parameters.

Attributes and Effects
The following attributes determine how OnEnd behaves and how you can use it in your programs. For the complete list of attribute and effect specifiers, see the Specifiers Page.

Attribute	Meaning
native_callable	Indicates that an instance method is both native (implemented in C++) and may be called by other C++ code. You can see this specifier used on an instance method. This specifier doesn’t propagate to subclasses and so you don’t need to add it to a definition when overriding a method that has this specifier.
public	The identifier is universally accessible. You can use this on modules, classes, interfaces, structs, enums, methods, and data.

using {/Fortnite.com/Teams}
using {/Fortnite.com/Characters}
# Module import path: /Fortnite.com/AI
AI<public> := module:
    @experimental
    # Result of an AI action
    ai_action_result<native><public> := enum<open>:
        # The action has been successfully executed
        Success
        # The action has failed during its execution
        Failure
        # The action has been canceled before completion
        Canceled
        # The action was not allowed to start
        Disallowed

    focus_interface<native><public> := interface<epic_internal>:
        # Look At specified location. Will never complete unless interrupted.
        MaintainFocus<public>(Location:(/UnrealEngine.com/Temporary/SpatialMath:)vector3)<suspends>:void

        # Look At specified Agent. Will never complete unless interrupted.
        MaintainFocus<public>(Agent:agent)<suspends>:void

    # Get the focus_interface interface for the specified character.
    (InCharacter:fort_character).GetFocusInterface<native><public>()<transacts><decides>:focus_interface

    @experimental
    # Fortnite Guards AI actions management
    fort_guard_actions<native><public> := interface<epic_internal>(fort_npc_actions):
        # Roam around the current position. Use the fort_leashable_component to specify the radius, else will roam anywhere.
        RoamAround<public>(?MovementType:movement_type = external {})<suspends>:navigation_result

        # Move in range to attack the current target
        MoveInRangeToAttack<public>()<suspends>:ai_action_result

        # Play a random emote from the character emotes bank
        PlayRandomEmote<public>()<suspends>:ai_action_result

        # Revive the specified target
        Revive<public>(Target:agent)<suspends>:ai_action_result

        # Attack the target
        Attack<public>(Target:fort_target_info)<suspends>:ai_action_result

    @experimental
    # Get the current fort_guard_actions interface for the specified character.
    (InCharacter:fort_character).GetFortGuardActions<native><public>()<transacts><decides>:fort_guard_actions

    @experimental
    # Fortnite NPC perception management
    fort_guard_perception<native><public> := interface<epic_internal>(fort_npc_perception):
        @experimental
        # Get information about the current target.
        GetCurrentTargetInfo<public>()<computes><decides><reads>:fort_target_info

        @experimental
        # Get the current alert level of the guard.
        GetAlertLevel<public>()<computes><reads>:fort_guard_alert_level

        @experimental
        # Get the current alert level of a target for the guard.
        GetAlertLevel<public>(Target:entity)<computes><decides><reads>:fort_guard_alert_level

        @experimental
        # Event when the alert level of the guard has changed.
        AlertLevelChangedEvent<public>:listenable(fort_guard_alert_level)

        @experimental
        # Event when the current target has changed.
        CurrentTargetChangedEvent<public>:listenable(fort_target_info)

    @experimental
    # Get the current fort_guard_perception interface for the specified character.
    (InCharacter:fort_character).GetFortGuardPerception<native><public>()<transacts><decides>:fort_guard_perception

    fort_leashable<native><public> := interface<epic_internal>:
        # Set custom leash position.
        #  'InnerRadius' ranges from 0.0 to 20000.0 (in centimeters).
        #  'OuterRadius' ranges from 0.0 to 20000.0 (in centimeters) and no less than 'InnerRadius'.
        SetLeashPosition<public>(Location:(/UnrealEngine.com/Temporary/SpatialMath:)vector3, InnerRadius:float, OuterRadius:float):void

        # Set the agent to be the new center of the leash.
        #  'InnerRadius' ranges from 0.0 to 20000.0 (in centimeters).
        #  'OuterRadius' ranges from 0.0 to 20000.0 (in centimeters) and no less than 'InnerRadius'.
        SetLeashAgent<public>(Agent:agent, InnerRadius:float, OuterRadius:float):void

        # Removes the current leash.
        ClearLeash<public>():void

    # Get the current fort_leashable interface for the specified character.
    (InCharacter:fort_character).GetFortLeashable<native><public>()<transacts><decides>:fort_leashable

    @experimental
    # Fortnite NPC AI actions management
    fort_npc_actions<native><public> := interface<epic_internal>(navigatable, focus_interface):

    @experimental
    # Get the current fort_npc_actions interface for the specified character.
    (InCharacter:fort_character).GetFortNPCActions<native><public>()<transacts><decides>:fort_npc_actions

    @experimental
    # Fortnite NPC perception management
    fort_npc_perception<native><public> := interface<epic_internal>:
        @experimental
        # Get the last known position of a target.
        GetLastKnownPosition<public>(Target:entity)<computes><decides><reads>:(/UnrealEngine.com/Temporary/SpatialMath:)vector3

        @experimental
        # Event when a target is added.
        TargetAddedEvent<public>:listenable(fort_target_info)

        @experimental
        # Event when the info about a target has been updated.
        TargetInfoUpdatedEvent<public>:listenable(fort_target_info)

        @experimental
        # Event when a target was removed.
        TargetRemovedEvent<public>:listenable(entity)

        @experimental
        # Event when a target is seen. Sight sense must be active.
        TargetSeenEvent<public>:listenable(fort_target_info)

        @experimental
        # Event when a target is heard. Hearing sense must be active.
        TargetHeardEvent<public>:listenable(fort_target_info)

        @experimental
        # Event when a target is touched. Touch sense must be active.
        TargetTouchedEvent<public>:listenable(fort_target_info)

        @experimental
        # Information about all detected targets.
        var<epic_internal> DetectedTargets<public>:[]fort_target_info

    @experimental
    # Get the current fort_npc_perception interface for the specified character.
    (InCharacter:fort_character).GetFortNPCPerception<native><public>()<transacts><decides>:fort_npc_perception

    navigation_target<native><public> := class<epic_internal>:

    # Generate a navigation_target from any position
    MakeNavigationTarget<native><public>(Position:(/UnrealEngine.com/Temporary/SpatialMath:)vector3):navigation_target

    # Generate a navigation_target from an agent
    MakeNavigationTarget<native><public>(Target:agent):navigation_target

    @experimental
    # Generate a navigation_target from an entity
    MakeNavigationTarget<native><public>(Entity:entity)<decides>:navigation_target

    # Result of a navigation request
    navigation_result<native><public> := enum:
        # The destination has been reached
        Reached
        # The destination has been partially reached (AllowPartialPath was used)
        PartiallyReached
        # Navigation has been interrupted before completion
        Interrupted
        # The navigating agent is blocked
        Blocked
        # The destination cannot be reached
        Unreachable

    movement_type<native><public> := class<concrete><final><computes><epic_internal>:

    # Module import path: /Fortnite.com/AI/movement_types
    movement_types<public> := module:
        Walking<public>:movement_type = external {}

        Running<public>:movement_type = external {}

    navigatable<native><public> := interface<epic_internal>:
        # Return the current destination of the character
        GetCurrentDestination<public>()<transacts><decides>:(/UnrealEngine.com/Temporary/SpatialMath:)vector3

        # Navigate toward the specified target
        NavigateTo<public>(Target:navigation_target, ?MovementType:movement_type = external {}, ?ReachRadius:float = external {}, ?AllowPartialPath:logic = external {})<suspends>:navigation_result

        # Stop navigation
        StopNavigation<public>():void

        # Wait for a specific duration
        Wait<public>(?Duration:float = external {})<suspends>:void

        # Apply a multiplier on the movement speed (Multiplier is clamped between 0.5 and 2)
        SetMovementSpeedMultiplier<public>(Multiplier:float):void

    # Get the navigatable interface for the specified character
    (InCharacter:fort_character).GetNavigatable<native><public>()<transacts><decides>:navigatable

    # Inherit from this to create a custom NPC behavior.
    # The npc_behavior can be defined for a character in a CharacterDefinition asset, or in a npc_spawner_device.
    npc_behavior<native><public> := class<abstract>:
        # This function is called when the NPC is added to the simulation.
        OnBegin<native_callable><public>()<suspends>:void = external {}

        # This function is called when the NPC is removed from the simulation.
        OnEnd<native_callable><public>():void = external {}

        # Returns the agent associated with this behavior.
        GetAgent<native><public>()<transacts><decides>:agent

    # Returns the `npc_behavior` for `InAgent`.
    (InAgent:agent).GetNPCBehavior<native><public>()<transacts><decides>:npc_behavior

    @experimental
    # Returns the `entity` for `InNPCBehavior`.
    (InNPCBehavior:npc_behavior).GetEntity<native><public>()<computes><decides><reads>:entity

    @experimental
    # The different alert levels of a guard.
    fort_guard_alert_level<native><public> := enum:
        # The guard has not detected any hostile target.
        Unaware
        # The guard has seen a hostile target but hasn't identified it yet.
        Suspicious
        # The guard has identified a hostile target but can't see it any more.
        LostTarget
        # The guard has identified a hostile target.
        Alerted

    @experimental
    # Information about a perceived target.
    fort_target_info<native><public> := class<epic_internal>:
        @experimental
        # The source of the detection stimuli.
        Target<native><public>:entity

        @experimental
        # True if the target can be seen.
        HasLineOfSight<native><public>:logic

        @experimental
        # Attitude toward this target.
        Attitude<native><public>:team_attitude

    @experimental
    # Create a `navigation_target` from a `fort_target_info`.
    MakeNavigationTarget<native><public>(TargetInfo:fort_target_info):navigation_target
