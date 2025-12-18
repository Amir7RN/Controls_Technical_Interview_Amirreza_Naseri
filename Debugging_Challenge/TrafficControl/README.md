# Traffic Light Problem (1 hour)

There's a busy traffic intersection outside your building. The roads at the intersection are horizantal street and vertical street. 
You are an engineer with the department of transportation and you're trying to come up with a new traffic light pattern that 
prevents cars from crashing in the intersection but also minimizes traffic jams. You ask a junior engineer to come up with a new 
traffic pattern and simulate the traffic flow at the intersection for two minutes or until 40 cars pass through. They work on it 
but then come to you saying they're stuck and they can't get the simulation to work. The traffic lights are exhibiting erratic 
behavior, crashes aren't reported properly, and their output results of cumulative time waiting look off. They ask you to review 
their code and help them make it work.

Your goal:
- Find all the errors in the code to get the simulation working properly
- Give feedback on how to make the code better next time

You will additionally be assessed on:
- The quality of your code

A few things to note about where the junior engineer is 98% certain there are NOT errors:
- There should be no issues with the 'advanceLane' function or the functions that start with 'draw'

A few other things to note about the simulation:
- Cars waiting to go into the intersection can only move into the intersection if the light is green.
- Cars already in the intersection can move out of the intersection even when the light is red or yellow.
- A crash should occur if a car on horizantal street and a car on vertical street are in the intersection at the same time.
- Cars IN the intersection are denoted with an 'X'. Cars on either side of the intersection are denoted with a '+'. 
  This will make more sense once you try running the program.
- Only one car from each lane can be IN the intersection at once. For example, if two cars are waiting in the eastbound 
  lane to cross the intersection, they cannot both move into the intersection at the same time. The first car in the 
  lane will move into the intersection. Then, the second car will move into the intersection as the first car leaves. 

To build the project, type the following in your bash terminal:
gcc traffic_light_problem.c -o traffic_light_problem

To run the project, type the following in your bash terminal:
./traffic_light_problem.exe

Candidate Action Items:
- Find the errors in the code to make the simulation work as the junior engineer intended
- Make any other improvements to the code as you see fit
- Answer the following questions:
  - What would you tell the junior engineer about ways that they could improve their code in the future? (1-3 sentences)
    - 1- I would encourage writing small assertions (e.g., never both directions green simultaneously) to catch logic errors early  during simulation.
      2- To minimize total simulation time, I would implement Hysteresis. The system would only initiate a switch if the opposing lane has a lead of at least 2 cars. This ensures we don't incur a "Yellow Light Penalty" for a negligible difference in traffic. However, to prevent idling, I would allow an override if the current lane is completely empty while demand exists elsewhere. This ensures we maximize the "Saturation Flow" of every green light and never waste seconds idling at an empty intersection.
      3- I would encourage consolidating the horizontal and vertical controllers into a single unified function in order to prevent the current bugs and issues.   
      
  - How else would you change this code to make it better so you can build on it in the future?(1-10 sentences).
    - code-wise improvemnet: To make this project more robust and scalable, 
      1- I would then move all hard-coded Numbers, such as the 10-car lane capacity and the 120-second simulation limit, into into global constants to improve maintainability.
      2- I would encourage explicitly initializing the "initIntersection struct" to avoid relying on implicit compiler behavior.
      3- I would also refactor the functions to pass the intersection by reference rather than by value, ensuring we’re always working with the actual system state.  
      4- I would replace the string-based color logic with the provided traffic_light_colors_t enum to eliminate the risk of typos.
    Algorithm-wise improvement: 
      1- Instead of a fixed 10 sec max-green, extend green one second at a time when the served direction still has cars waiting and the opposing direction is below a threshold. This reduces unnecessary switching.
      2- If the goal is to make it more real-world scenarios, to improve stability, I would add a "Minimum Green Time" to the state machine; this prevents the lights from "chattering" rapidly when car counts are nearly equal. 
      3- Also, for real world scenarios, I would move toward a weighted cost-function that considers not just the number of cars, but the cumulative wait time of the lead vehicle, ensuring that lanes with lower popularity aren't left waiting indefinitely.


Don't forget; we are interested in both your solution and your thought process.

Good Luck!