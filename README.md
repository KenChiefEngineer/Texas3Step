# Texas3Step
A modern twist to the classic game of tic-tac-toe for Move38's Blink arduino based platform

# Requirements
Recommended a minimum number of 9 Blinks to play, but better with 16 or more. 

# Setup
### Blink Layout
If you are playing with just 9 Blinks, it is recommended to set them up similar to a tic-tac-toe grid
for your first couple of games:
<p>O O O</p>
<p>&nbsp O O O</p>
<p>&nbsp &nbsp O O O</p>

If you have more than 9 Blinks, be creative. Just keep in mind the goal of the game is for a player to
claim three Blinks in a row, so a layout with minimal 3 in a row possibilities might not be much fun.

# How To Play

### Objective
Players alternate claiming Blinks. You should see each Blink on the board give an indication when you
claim a Blink. Be the first player to claim three Blinks in a straight line to win.

### Start Game - Random Color
* Player 1 single clicks any Blink to claim it.
* Player 2 single clicks any Blink to claim it.
* Continue alternating back and forth single clicking a blank blink to claim it

### Start Game - Choose Your Color
* Player 1 LONG clicks a blink to claim it. 
* Player 1 can then single click that same blink to change the color
* Player 1 then LONG clicks again once their preferred color is showing
* Player 2 LONG clicks a blink to claim it. 
* Player 2 can then single click that same blink to change the color
* Player 2 then LONG clicks again once their preferred color is showing
* Player 1 single clicks any unclaimed Blink to claim it.
* Player 2 single clicks any unclaimed Blink to claim it.
* Continue alternating back and forth single clicking a blank blink to claim it

### GAME OVER
* The game ends when a player claims 3 hexes in a straight line, they are the WINNER!
* There are no more Blinks to claim and no one has achieved victory
* Player agree it is a draw as neither player has the possibility to make a 3 in a row
  even though there are still unclaimed Blinks left
* LONG press any Blink to reset the board and start again

# Developer Notes
### Datagram structures
##### During Game
| A | B | C | D | E | F | Description |
|---|---|---|---|---|---| ----------- |
|   |   |   |   |   |   | Initial state or reset to initial state |
| X |   |   |   |   |   | Game over   |
|   | X |   |   |   |   | You are one of the winning Blinks! |
|   |   | X |   |   |   | Player 1 has made a move |
|   |   |   | X |   |   | Player 2 has made a move |
|   |   |   |   | X |   | Player 1 has claimed this Blink |
|   |   |   |   |   | X | Player 2 has claimed this Blink |

##### Setup
| A | B | C | D | E | F | Description |
|---|---|---|---|---|---| ----------- |
| X | X | X | X | X |   | Setup - Player 1 Color Value |
| X | X | X | X |   | X | Setup - Player 2 Color Value |

##### Breakdown of Player Color Setup Bytes and Bits
| A | B | C | D | E | F | Description |
|---|---|---|---|---|---| ----------- |
| X | X | X |   |   |   | Player Color Setup - Color 0-7 Bits  |
|   |   |   | X |   |   | Player Color Setup - Flag Bit |
|   |   |   |   | X |   | Player Color Setup - Player 1 Color Config Flag |
|   |   |   |   |   | X | Player Color Setup - Player 2 Color Config Flag |

### TODOs
* Explorer options to minimize player 1 advantage and mitigate player 1 tic tac toe cheese moves
  which are even easier to do with hexes than squares
* Implement selectable 3, 4, or more in a row options. Would require a change to my envisioned
  win detection algorithm. Would probably force a change in datagram structure and the way Blinks
  communicate with one another.
* If the above gets implemented, could even explorer options to just be consecutive blinks instead
  of the straight line requirement. Might not be feasible and make the game too "silly" 
