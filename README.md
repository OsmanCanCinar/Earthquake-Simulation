# Earthquake-Simulation

WHAT IS IT?
Main purpose of this model is showing the certain elements that can increase and decrease the effects of an earthquake. To do that, I designed an environment that is like Izmir, Turkey which includes a sea, seashore, and a mountain. First element I want to show is properly deciding where to construct a building, choosing the suitable ground for foundations , and avoiding fault rupture zones. Next one is following the construction regulations and building a proper structure. Third, doing urban renewals and choosing to live in newer buildings to avoid decaying buildings. Last one is doing periodical restorations to the buildings. Those are the parameters that  I came across with.
I will start informing by explaining the World then, I move on to Variables that I used and Parameters. Next, I will continue with Procedures and Calculations that I made to obtain these results. Finally, I will talk about Main Cases.
The Houses initially will be white and shapes as house, but if they collapse their shape will be a black cross.

WORLD
Initially, I draw a black frame only on the edges of the world. This way I can see environment and turtles from an outer look. Then I divided the world into three parts.
1.	Sea	
a.	I painted the left side of the world (-24 to -10) as “pxcor”, and (-24 to 24) as “pycor” to blue. This part represents the sea. There cannot be any buildings on the sea, that is why it does not affect the durability-ground or soil-type attributes of the buildings(turtles).

2.	Beach
a.	This is the middle part of the world (-10 to 0) as “pxcor”, and (-24 to 24) as “pycor” to yellow (47). This part represents the beach. There can be buildings on the beach. Since sand is not a well ground for foundation, for the turtles that spawned on sand, their durability-ground will be set as 2 and soil-type will be set as sandy.

3.	Mountain
a.	This is the right side of the world (0 to 24) as “pxcor”, and (-24 to 24) as “pycor” to grey (3). This part represents the mountain. There can be buildings on the mountain. Since mountain is a rocky ground and which is good for foundation, for the turtles that spawned on mountain their durability-ground will be set as 8 and soil-type will be set as rocky.

MONITOR
1.	Destroyed Buildings: This shows the count of the destroyed-count.


VARIABLES
•	globals:
o	destroyed-count
o	total-magnitude
o	destructive-aftershock
o	fault-rupture-affect

•	turtles-own:
o	total-durability
o	durability-ground
o	durability-age
o	durability-estate
o	durability-restoration
o	is-on-fault-rupture
o	is-restored
o	soil-type


PARAMETERS
1.	Number-of-buildings
a.	It determines the number of the building before creating turtles.
b.	Its minimum value is 20 and the maximum value is 60.
c.	Initial value is 30.

2.	Housing-Estate	
a.	If the buildings are an estate, the buildings will be spawned in a certain area. Furthermore, since they are built as an estate, we can assume that they were build according to the construction regulations. This will set durability-estate attribute of the turtles as 5.
b.	If they are not part of an estate, they will spawn randomly and they are built by different people, and this sets durability-estate attribute of the turtles as 0.



3.	Age
a.	There are three types of age. 
i.	First one is “New Build”, this sets durability-age attribute as 8.
ii.	Second one is “Mid Life”, this sets durability-age attribute as 5.
iii.	Third one is “Decayed”, this sets durability-age attribute as 2.

4.	Random-Age
a.	If it is true, the durability-age attribute of the buildings will be assigned randomly.
b.	If it is false, the selected option from Age selector will be applying to all.

5.	Random-Restoration
a.	If it is true, some buildings will be randomly restored, and some will not. The durability-restoration attribute of buildings will be set as 5 and is-restored attribute as Yes.
b.	The ones that are not restored will be set as 0 for the durability-restoration attribute and No for the is-restored attribute.

6.	Magnitude
a.	This parameter represents the magnitude of the earthquake.
b.	Its minimum value is 1.0 and the maximum value is 10.0.
c.	Initial value is 4.0.

7.	Aftershock
a.	There are two categories for aftershock. 
i.	First one is “Weak”, this sets destructive-aftershock attribute as magnitude * 0.1.
ii.	Second one is “Strong”, this sets destructive-aftershock attribute as magnitude * 0.3.
8.	Frequency-of-Aftershock
a.	This specifies the count of aftershocks.
b.	Its minimum value is 2 and the maximum value is 10.
c.	Initial value is 5.

9.	Fault-Rupture
a.	If it is true, there will be a fault-rupture on the map and the patches on it will be affected more from the earthquake. The is-on-fault-rupture is a global variable, and it will be set as “yes” and  
b.	The ones that are not on the fault-rupture will have “no” as their is-on-fault-rupture.





PROCEDURES
•	setup-world: It sets up the frame around the world and paints the world as sea, beach, and mountain.

•	setup-buildings: This procedure spawn buildings according to go housing-estate parameter and sets the turtle’s color, shape, and size attributes. Then, makes sure that buildings do not overlap by calling separate-buildings procedure. Finally, calculates total-durability of buildings by calling calculate-durability.

•	separate-buildings: If any buildings are overlapping it moves the turtle to south by 1 unit. It calls itself recursively till the turtle does not overlap with any other turtle.

•	calculate-durability: It is a very important procedure because it calculates the total-durability of the buildings by calling check-age, check-soil, check-estate, check-restoration. After all these procedures that set the attributes of building, it calculates the total-durability of the building.

•	check-age: It reads the age and random-age parameters and assigns the age of the building accordingly.

•	check-soil: It checks the patch color “pcolor” of the building that it is standing on and if it is on beach/yellowish color (47), it will assign a weaker durability-ground value as 2 and as soil-type it will set “sandy”. If it is on the mountain/greyish color (3), it will assign a stronger durability-ground value as 8 and as soil-type it will set “rocky”.

•	check-estate: It reads the parameter housing-estate and if its in an estate then, it will set durability-estate as 5 because of the better and more controlled construction. If it is not, it will set durability-estate as 0 because the constructions are done by separate people.

•	check-restoration: It checks the random-restoration parameter. If it is true, some house will be restored, and their durability-restoration attribute will be 5 and is-restored attribute will be “yes”. If it is false, their durability-restoration attribute will be 0 and is-restored attribute will be “no”.

•	setup-fault-rupture: This is where I set up a fault rupture. If the fault-rupture parameter is true, I create a diagonal fault rupture, paint the patches on it to red and set the global is-on-fault-rupture to “yes”. If it is false, set the global is-on-fault-rupture to “no”.

•	calculate-destructivity: It calculates the destructivity of the earthquake by calling handle-aftershock and check-fault-rupture. After calling those procedures, it calculates the total-magnitude of the earthquake by using global variables.


•	handle-aftershock: It reads the selected value from aftershock selector. If it is “Weak”, it sets the global destructive-aftershock variable to magnitude times 0.1. If it is “Strong”, it sets the global destructive-aftershock variable to magnitude times 0.3. Finally, it set the destructive-aftershock variable to multiplication of destructive-aftershock and frequency-of-aftershock parameter.

•	check-fault-rupture: This is where I check fault rupture. If the color of current patch that the building is standing on is red, then this procedure sets the global fault-rupture-affect variable to multiplication of constant 3 and half of the magnitude.

•	shake-it: This is where I simulate the earthquake. I compare the calculated total-durability attribute of building with global variable total-magnitude. If the total-durability is smaller or equal to total-magnitude, the building collapses. To represent this, I set the shape of the turtle to a “X”, its color to black and increase the global variable destroyed-count. 

•	setup: Initially it resets the world by calling clear-all. It asks patches to call setup-world procedure then it calls setup-buildings procedure. Then, it again asks patches to call setup-fault-rupture. Finally, it calls calculate-destructivity procedure, and it also shows the count of turtles before reset-ticks.

•	go:  This procedure asks turtles to call shake-it procedure and it shows total-magnitude.



CALCULATIONS
•	total-durability: 
( ( durability-ground * durability-age ) + durability-estate + durability-restoration )

•	total-magnitude:
( ( magnitude * 1.5 ) + destructive-aftershock + fault-rupture-affect )

•	destructive-aftershock: 
( destructive-aftershock *  frequency-of-aftershock )

•	fault-rupture-affect: 
( ( magnitude / 2 ) * 3 )





MAIN CASES
1-) Difference of Foundation Ground 
For this case, we have 30 houses. They are all in midlife, not a part of estate, no restoration , no fault rupture , and magnitude of earthquake 5.0 with small 5x aftershocks(power of earthquake is 10).  The houses on the beach are collapsed because of the sandy ground(turtle13) but rocky did not(turtle14).  
 
2-) Difference of Being in an Estate(Proper Construction) 
For this case, we have 30 houses. They are all in midlife,  part of an estate, no restoration , no fault rupture , and magnitude of earthquake 5.0 with small 5x aftershocks(power of earthquake is 10).  This time, the houses on the beach did not collapsed because proper construction(turtle22) . Rocky(turtle25)
 
 
3-) Difference of Doing Restorations and Living in a Newly Build Building 
For this case, we have 50 houses. They are all in new build,  part of an estate, random restoration , no fault rupture , and magnitude of earthquake 7.0 with Strong 7x aftershocks(power of earthquake is 25.2).  This time, some of the houses on the beach did collapsed (turtle6) but some survived (turtle12) thanks to being  newly build and doing restorations even though the earthquake’s effect is stronger. Rock ground is (turtle16).
 
 
4-) Difference of Random Ages, Random Restorations and Not Being in an Estate 
For this case, we have 50 houses. They are all randomly aged, not a part of estate, random restoration , no fault rupture , and magnitude of earthquake 7.0 with Strong 7x aftershocks(power of earthquake is 25.2).  This time, houses on the beach collapsed (turtle43) and some of the houses on the mountain collapsed as well(turtle11) but some of the houses on the mountain survived(turtle46).
 
 
5-) Difference of Fault Rupture and Random Age
For this case, we have 50 houses. They are all randomly aged, not a part of estate, random restoration , there is a fault rupture , and magnitude of earthquake 7.0 with Strong 7x aftershocks(power of earthquake is 35.7).  There are two houses on fault line and one of them collapsed(turtle32) and other did not(turtle48).
 
 
