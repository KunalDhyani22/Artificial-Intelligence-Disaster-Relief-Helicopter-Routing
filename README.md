Goal: The goal of this assignment is to take a complex new problem and formulate and solve it 
as search. Formulation as search is an integral skill of AI that will come in handy whenever you 
are faced with a new problem.  Heuristic search will allow you to find optimal solutions.  Local 
search may not find the optimal solution, but is usually able to find good solutions for really large 
problems.  

Scenario 
There are floods in a region. There is an urgent need to carry out relief operations from 
neighboring cities. There are a fixed set of relief packages to deliver to affected villages using a 
fleet of helicopters. Each village has a number of people stranded. The goal is to allocate relief 
deliveries to helicopters such that maximum aid is delivered, while respecting capacity and range 
limits of each helicopter, and while simultaneously minimizing a “logistical strain” cost caused by 
routing aid inefficiently. 
For this we assume, we are provided a list of villages V that need relief. Each village v is associated 
with its 2D coordinates (xv, yv). Similarly, we have a few cities C, along with 2D coordinates for 
each city. The distance between any two locations is given by the straight line distance between 
their coordinates (in kms). For each village, we are also provided nv: the number of people 
expected to be stranded in that village.  
There are three types of packets T = {d, p, o}, which stand for dry food, wet (perishable) food, 
and other supplies. The goal is to send about 9 meals per stranded person, and about 1 unit of 
other supplies per stranded person. Each packet of type t weighs a fixed amount w(t). Each packet 
of type t has a fixed value v(t). The meals may be dry or perishable food, but wet food is 
preferable, i.e., v(p) > v(d). 
There are H helicopters. Each helicopter h has a home city home(h). It also has a weight capacity 
wcap(h), and a distance capacity dcap(h) per trip. Each trip starts at the home city and ends at 
the home city, and package weight on the trip cannot exceed wcap(h) and total distance traveled 
cannot exceed dcap(h).  Moreover, total distance traveled by any helicopter across trips cannot 
exceed a given DMax. 
Each trip costs F + alpha*distance. Here F is the fixed cost per trip (for takeoff and landing). And 
alpha represents some notion of fuel efficiency. 
Total value of solution = Total value achieved – total trip cost. 
The goal of the assignment to produce a plan for each helicopter, such that the total value is 
maximized. How many trips they do. How many total packages of each type they start with per 
trip. Which villages do they visit and in what order. How many packages of each type do they 
drop per village. 

Input: 
The first line has total processing time available in minutes. 
The second line has DMax: the max distance in kilometres 
The third line has six numbers representing: w(d) v(d) w(p) v(p) w(o) and v(o) 
The fourth line has C: the number of cities followed by 2C coordinates. Imagine each city is {1, …, C}. The 
2C numbers represent x, y coordinates of each city, successively. 
The fifth line has V: the number of villages, followed by 3V numbers. Imagine each village is {1, …, V}. The 
3V numbers represent x, y, n – the coordinates of each village and number of people stranded. 
The sixth line has H: the number of helicopters followed by 5H numbers representing home city id, wcap 
and dcap, F and alpha of the helicopter, successively. 
Here is a sample input 
1 
100 
0.01 1 0.1 2 0.005 0.1 
2 0 0 10 10 
2 0 5 1000 0 10 1000 
2 1 100 25 10 1 2 100 50 10 1 
This input suggests that there are two cities at (0, 0) and (10, 10) and two villages at (0, 5) and 
(0,10). 1000 villagers are stranded in each village. Each packet weighs 10 gms, 100 gms and 5 gms 
for d, p, and o. Similarly, value of dropping a dry packet is 1, for a perishable packet is 2 and other 
supplies packet is 0.1. There are two helicopters, one at each city. Their weight capacity is 100 kg 
each, but distance capacity is 25 km and 50 kms each. Both helicopters have F and alpha 10 and 
1 respectively. The maximum distance covered by any helicopter cannot exceed 100 kms. 

Output: 
Your algorithm should return the trips undertaken by each helicopter. Make one row for each helicopter 
in the order 1 to H. You should first write helicopter number. Follow this with number of trips. Then for 
each trip, write the number of packages of type d, p and o to pick up.  Then mention number of villages 
the helicopter will travel, and village id and the number of packages of each type it will drop per village. 
Make one new row per trip. In the end add a -1 to move to the next helicopter.  For example, see the 
following output: 
1 2 
9000 0 2000 2 1 9000 0 1000 2 0 0 1000 
8889 111 0 1 2 8889 111 0 -1 
2 0 -1 
The first row is read as: helicopter#1 makes two trips. In the first trip it picks up 9000 packets of dry food 
and 2000 packets of other supplies. It visits two villages in this trip: village 1 dropping all dry packets and 
1000 of other supplies and then village 2 dropping 1000 other supplies. In trip 2 it picks up 8889 packets 
of dry food and 111 packets of perishable food and drops all of them in village 2. A -1 indicates that we 
are done with helicopter 1. Helicopter 2 does not undertake any trips. 
The value of objective function for this solution is evaluated as: 
Distances covered in both trips: 20 kms each. 
Cost of both trips: 10 + 1*20 = 30 
Value gained by village 1: 9000*1 + 1000*0.1 = 9100 
Value gained by village 2: 8889*1 + 111*2 + 1000*0.1 = 9211 
Total objective function  = 9100 + 9211 – 60 = 18251 
Note that total distance covered is 40 km by helicopter 1, which is under 100 kms.  Note that each trip of 
helicopter was 20 km which is within dcap constraint of 25 kms. Note that trip1 and trip2 had weights of 
100 Kg and 99.99, which are under 100Kg. Hence, it is a valid solution. 
Note also that if at any place more than 9x#stranders amount of food is dropped, then no additional value 
is gained from it. 
