Arcesium


```
2 Medium level problems in Hacker Rank.

Round 2: Exepected to write LLD and write sudocode for shortest path in board using snakes and ladder and use the shortest path to traverse from start to end .

/*
Design a multiplayer Snake and Ladder game. Maximum of 5 players can play the game at any time. All players are individual threads in the system.
The game should follow the following rules.

    A new game should be created with the board created at random.
    Upto 5 players can join the game.
    Game can only start when atleast 2 players are in the game.
    New players can join the game if only the existing players have played less than 3 moves.
    When a new player joins, freeze all other players and let the new player catchup with the moves of other players. If player 3 joins and player 1 & 2 have already played 2 moves, player 3 should play move 1&2 before all 3 players can play move 3.
    All players should play a given move parallelly at the same time. if a player has not played a move, the remaining players should not be able to proceed to the subsequent. Ex: Turn 1 can be played parallelly by all players. Turn 2 can only be played if all players have completed Turn 1.
    If a player does not play his move for more than 120 seconds, evict the player from the game.

All these controls need to be at the game level. Do not try to control the players behavior. Players are always eager to play their next turn.

Once person reaches 100th tile in the board, we declare him the winner. Since players are playing parallelly, there could be more than 1 winner and all winners are eligible for winner/bumper prize.

Winner prize - $10
Bumper Prize:

Completed in shortest moves - $1000
Completed in shortest moves + 1 - $750
Completed in shortest moves + 2 - $500
Completed in shortest moves + 3 - $250
Completed in shortest moves + 4 - $100
Completed in shortest moves + 5 - $50

Using a standard die(1-6), the board could be solved with a specific set of rolls in the quickest fashion. The number of moves it takes is considered to be the shortest number of moves. Calculate the shortest number of moves for a given board and use that in calculating if user(s) are eligible for bumper prize.
```