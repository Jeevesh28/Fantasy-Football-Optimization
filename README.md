# Fantasy Football Optimization ⚽

## Task 💼
1. In this round, you get to experience how it feels to be a Football manager.
2. We have to create a team consisting of 5 players in the main team and a substitute team of 5 players, respectively.
3. We are given a database with all attributes of players from which we will need to choose your team.

## Constraints 📋

1. We have to make sure that no two players are selected from the same nationality or club as provided in the dataset.
2. We have to include one left-footed player in the playing squad (main team and the substitute team).
3. The main team should compulsorily consist of a forward, a midfielder, a defender, a goalkeeper, and the fifth player could belong to any of the positions of your choice except goalkeeper.
4. The substitute team should only consist of players having positions mentioned as (SUB / RES) as their position in the dataset.
5. Note: The forward position players are mentioned as ( CF, RF, LF, ST, LS, RS, LW, RW) whereas the midfield positions are ( LM, RM, CM, CAM, CDM, LAM, LCM, LDM, RCM, RAM, RDM) and the defenders are mentioned as (CB, LB, RB, LCB, RCB, LWB, RWB ) and goalkeepers are mentioned as GK respectively.

## Approach 🎯

1. Dataset pre-processing and filling missing values (analysis and imputing).
2. Division of dataset into main team and substitute team players along with assigning playing positions.
3. Building optimization model taking care of constraints.
4. Relevant visualizations for analysis and verification.

## Final Team 🏆

**Main Team:**
| Name          | Club                | Nationality | Position | Preferred Foot | Rating |                                 
| ------------- | ------------------- | ----------- |--------- | -------------- | ------ |
| J. Oblak      | Atlético de Madrid  | Slovenia	  | GK       | Right          | 91.0   |
| R. Varane     | Manchester United	  | France	    | DEF	     | Right          | 88.0   |
| V. van Dijk   | Liverpool	          | Netherlands | DEF      | Right          | 89.0   |                    
| K. De Bruyne  | Manchester City	    | Belgium	    | MID	     | Right          | 91.0   |                 
| L. Messi      | Paris Saint-Germain |	Argentina	  | FWD	     | Left           | 93.0   |


**Substitute Team:**
| Name           | Club                | Nationality    | Position | Preferred Foot | Rating |                                 
| -------------- | ------------------- | -------------- |--------- | -------------- | ------ |
| J. Pavlenka	   | SV Werder Bremen	   | Czech Republic	| GK	     | Right          | 82.0   | 
| G. Chiellini	 | Juventus	           | Italy	        | DEF	     | Left           | 86.0   |
| J. Boateng	   | Olympique Lyonnais  | Germany	      | DEF	     | Right          | 83.0   |                    
| 15 Xavi	       | FC Barcelona        | Spain 	        | MID	     | Right          | 86.0   |                 
| Z. Ibrahimović | AC Milan            | Sweden	        | FWD	     | Right          | 84.0   |

**Team Lineup:**

![Team Lineup](https://i.imgur.com/HLP9f5b.png)

