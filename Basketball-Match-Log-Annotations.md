## BASKETBALL MATCH LOG

Each line has the following info

    TIME, HOME SCORE, AWAY SCORE, POSSESSION TEAM, ACTIONS



* TIME is the time at the start of the possession, it is optional but for substitutions (useful to calculate Plus/Minus)
* HOME SCORE and AWAY SCORE is the match score at the end of the current possession (you could just write the possession team)
* ACTIONS is a list of shorthands separated by spaces

Example for a match between Tumminelli (Home) vs Gareganano (Away). Tumminelli is indicated with TUM and Garegnano with GAR.

Here an example with after the line a comment to explain the action. 


```
10:00, 0, 0, -, HOME(TUM) 21* 24* 07* 13* 06* 18 09 45 72 10 12 43
10:00, 0, 0, -, AWAY(GAR) 07* 66* 25* 87* 16* 61 59 58 27 13 31 32
```


“These 2 rows contain the numbers of the players for the home and away teams. The players followed by a * are the players in the starting 5”


```
10:00, 0, 0, -, Q1 21JMP07 
```


"The match starts with jump ball between Tumminelli #21 against Garegnano #7. Possession is - because is at the moment not assigned"


```
, 2, 0, TUM, ZONE23 24AST 21FG+02HK
```


"The time is optional, so it is not set. The jump ball was won by Tummninelli so the possession is set to TUM. Garegnao sets up a 2-3 defensive zone. Tumminelli #24 gives an assist to #21 that scores 2 points with a hook shot from zone 02 (straight under the rim)"


```
, 2, 0, GAR, M2M 07FG-14
```


"Garegnano has the possession, Tumminelli sets up a man to man defense. The #7 attempts a 3-points shot from the left wing but misses"


```
, 5, 0, TUM, 24AST 21SCR 07FG-06JMP 66F07 07FT+- 21RB 24FG+05FD
```


"Garegnano is still using a 2-3 defensive zone, so there is no need to annotate it. Tumminelli #24 creates a chance for #7 with the help of #21's screen. #7 attempts a jump shot from mid range but he is fould by Garegnano's #66. #7 does the first free throw and misses the second. Tumminelli's #21 grabs the rebound. Tumminelli's 24 scores a 2-points fade away from the right wing."


## ACTIONS

{##} is the player number, if the action has 2 ##’s then the first one represents the player that does the action while the second one is the one that suffers it.

{NNN} it is the 3-letters that represents a team


### FLOW ACTIONS

Represents the flow of the match.



* **HOME({NNN})** It is the shorthand to indicate the 3-letters code for the home team. It is followed by the number of the players. The number is followed by a * if the player is in the starting five.
    * Examples:
        * `HOME(TUM) 21* 24* 07* 13* 06* 18 09 45 72 10 12 43`
* **AWAY({NNN})** It is the shorthand to indicate the 3-letters code for the home team. It is followed by the number of the players. The number is followed by a * if the player is in the starting five.
    * Examples:
        * `AWAY(GAR) 07* 66* 25* 87* 16* 61 59 58 27 13 31 32`
* **Q#** represents the beginning of the quarter 
    * Examples:
        * Q1 “The first quarter begins”
* **##JMP##** represents the jump at the beginning of the game. The first ## is the home player, the second one is the away team player. The player that wins the jump determines the frist possession.
* **{NNN}TO** A team calls timeout
    * Examples:
        * `TUMTO` “Tumminelli calls a time out”


### BASIC SHORTHANDS



* **{##}FG(+/-){zone}{type}** Field Goal
    * plus means  shot done, minus means shot missed
    * {zone} is a number that represents the field zone (see attached chart)
        * 01 to 08 are 2 points shot
        * 09 to 15 are 3-points shots
    * Type is optional and can be one of the following:
        * RLAY: Reverse Layup
        * LAY: Layup.
        * DNK: Dunk.
        * JMP: Jump Shot
        * HK: Hook Shot
        * FD: Fadeaway
        * TP: Tip-In
        * BNK: Bank Shot
        * AO: Alley-Oop
        * FLT: Floater
        * SET: Set Shot
    * Examples:
        * `07FG+02TIP` “Player #7 scores a 2-points by tipping in from zone 2 (straight under the rim)”
        * `23FG-10` “Player #23 attempts a 3 pointer from right wing”
* **{##}FT(+/-)** Free Throw
    * Repeat + or - for each free throws
    *  Examples:
        * `02FT+- `“Player #02 scores the first one and misses the next one”
* **{##}RB** Rebound (if it is a defensive rebound you have to change row and start a new possession)
* **{##}AST** It represents a decisive passage for a shot
    * Examples:
        * `24AST 31FG+07` “#24 passes to #31 that scores 2 points from the left wing”
* **{##}TO{type**} it represents a player losing the ball. {type} is the optional type of violation.
    * Types of violation:
        * L A turnover for lane violation (3 seconds in the key)
        * S Shot clock violation
        * B Backcourt violation
        * T Traveling violation
    * Examples:
        * `12TO` “Player #12 misses the pass and loses the ball”
        * `01TOS` “Player #1 has the ball when the time for the action ends”
* **{##}STL{##}** Represents a defensive player that steals the ball (change row to indicates the possession changed)
    * Examples:
        * `12STL02` “Player #12 steals the ball from #02”
* **{##}BLK** A defensive player blocks a shot 
    * Examples:
        * `07FG-2DNK 13BLK 09RB` “Player #7 tries a dunk staring in front of the rim, #13 blocks and offensive player #09 takes the rebound” 


### FOULS AND INJURY SHORTHANDS



* **{##}OF/DF{type}{##}** A player commits a foul. OF is offensive foul (done by the player of the team in possession). DF is a defensive foul committed by a defensive player. (if the one who commits foul is in the possession team change row (possession) bfore annotate it otherwise continue on the same row)
    * Type is optional (if it is omitted it means personal foul):
        * P personal foul
        * F Flagrant foul (antisportivo)
        * T Technical foul  (if it is the bench instead of {##} use {NNN} to indicate the team)
    * Examples:
        * `16FO09` “Player #16 commits a personal foul on player #9”
        * `16FOP09` “Player #16 commits a personal foul on player #9”
        * `16FOF09` “Player #16 commits a flagrant foul on player #9”
        * `TUMFOT` “Tumminelli's Coach gets a technical foul for excessive talking”
* **{NNN}/{##}EJ** Ejection of a player (use {NNN} instead of {##} if the coach is ejected). If the ejection is immediately after a foul you can omit {NNN} or {##}    
* **{NNN}{##}SUB{##}** Represents a bench player entering the field in substitution of an another player
    * Examples:
        * `TUM01SUB87` “Tumminelli’s Player #87 leaves for player #1”  
* **{NNN}{##}INJ** The player is injured and should leave the field


### DESCRIPTIVE SHORTHANDS

These annotations help to read the possessions better.



* **FB** Fast Break
* **{##}ISO** Isolation Play
* **{##}PNR{##}** Pick And Roll 
* **{##}OB** An interesting off-ball movement 
* **{##}SCR** A screen that help a shot attempt
* **HL**  Used at the end of the possession to highlight the possession (Highlight Play)
* **CLOCK** A forced shot due to the risk of shot clock violation


### SCHEME SHORTHANDS


#### DEFENSE SHORTHANDS

It is in general written at the beginning of the possession but it could be put also inside the possession if the team changes.



* **PRESS{type}** It means that the defensive team is playing a **press zone**. Type is optional and can be FC (full court) or HC (half court)
* **ZONE{type}** It means that the defensive team is playing **zone defense**. Type is the optional type (eg. 23). 
* **M2M** Man to man defense


#### OFFENSIVE SCHEME

It could be useful to annotate them when called but it is not easy to have a shorthand as it is better to use the name of the called scheme.
