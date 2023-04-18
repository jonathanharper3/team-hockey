# team-hockey

This portion of the Capstone centered around identifying the next optimal event to occur based on the current
state of the hockey game by leveraing a Q-learning algorithm.

The dataset includes 20 hockey games with the following relevant columns:

gameid: Game identifier
playerid: Player identifier for the player performing the event
teamid: Team identifier for the player performing the event
opposingteamid: Team identifier for the opposing team
teaminpossession: Team identifier for the team in possession of the puck
currentpossession: Possession count in the game
xg: Expected goal value (percentage) when a shot is taken
compiledgametime: Rolling time elapsed in the game
eventname: Action taken at the point in time (shot, save, goal, etc.)
outcome: Whether the action was successful or failed
xadjcoord: X position of the puck in relation to the rink
yadjcoord: Y position of the puck in relation to the rink
scoredifferential: Score differential between the two teams
period: Game period (1, 2, 3, or 4 for Overtime)
manpowersituation: Manpower situation (even strength, power play, or penalty kill for team in possession)

As detailed above, the model leverages Q-learning, a reinforcement learning approach, to learn the next optimal event 
to occur based on the current state of the hockey game. The epsilon-greedy strategy is employed to balance 
exploration and exploitation when choosing this next event. As can be seen in the logic, two separate Q-learning
approaches are taken, with the difference being how the unique states are identified (granular vs. high-level states).
This was done in an attempt to overcome data skew and see whether different states would improve outcomes.

Using the Q-Learning Code:

Import libraries and load the dataset into a pandas DataFrame.
From this already prepared and cleaned dataset, create the transitions DataFrame that provides likelihood of one event leading to another.
Define unique states, actions, and their mappings.
Set hyperparameters for Q-learning methodology.
Train the model using Q-learning and the epsilon-greedy strategy.
Generate the optimal event based on the current state of the hockey game.

Dependencies:

See requirements.txt


--- Generative Model (Q-learning) ---

This model takes a similar approach to the Q-Learning Methodology. Instead of utilizing the transitions dataframe, this model trains the q-table using the 
hockey event dataset by iterating through each event and assigning a reward and and changing the next state, if necessary. After the model has been trained 
on the data, a random (or manually selected) state can initiate a new sequence of events that lead to a goal being scored.

The number of episodes, and steps, can be changed to further the learning or stop early to prevent over-fitting.


--- Shots on Goal Exploratory Analysis ---

This portion of the Capstone centered around understanding the events that contribute to a shot, assist, or goal.

It begins by creating labels for each play that places it into a zone, based on the x- and y-coordinates provided 
in the original data. It then looks at the zone patterns for different events, including goals, assists, successful
shots, unsuccessful shots, and so on. This information is further shown for areas in the offensive zone, or '4' 
areas like A4 and C4. 

After this analysis is complete, the notebook builds out a play sequence, or a list of plays that happen while
one team is in possession. These lists are filtered to only include sequences where a shot occurs or sequences
where a goal is the last event in the sequence. A Counter is used to determine the most common events in different
sequences and bar graphs are built to visualize these events.


--- Visualizations ---

This notebook utilizes the hockey_rink package to create custom charts (mainly heat and ozone maps) that are used to visualize certain datapoints corresponding 
to certain events from the dataset such as shots, assists, blocks etc. 
