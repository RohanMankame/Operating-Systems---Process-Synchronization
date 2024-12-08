# Operating-Systems---Process-Synchronization

Coded in C-mini

Task:

It's Thanksgiving in BACI-land. We're going to write the necessary code to synchronize some Thanksgiving processes. There are 4 different types of processes we will have to synchronize:

Mother process: This process will be responsible for cooking the entire meal. She will prepare the foods for the meal and put them in the oven. When done with this, she must go on a hayride (see the rules for the hayrides below) with the youngest child (as he is afraid to go without his mother). Assume this is child process 8. When done, she enters the house, washes up, puts the food on the table (we will assume the food is done by the time she gets back from the hayride) and then sits down to eat dinner. She must wait to eat until all other processes are sitting down and ready to eat and the turkey has been carved. When everyone is done eating and has been excused from the table (done by the Father process), she will go read her favorite book.

Father process: This process will hook up the horses to the wagon and begin giving hayrides. (See rules below for giving the hayrides.) When all children and relative processes have been given hayrides, the father process will unhook the horses, feed them, and then go into the house and clean up for dinner. He will then sit down at the table. When everyone is seated, he will carve the turkey. When he has carved the turkey everyone can begin eating. After eating, this process excuses everyone from the table and is done (he goes to take a nap on the sofa and watch the football game).

Child process: There will be 8 child processes. These processes start by raking leaves in the yard. When done, each child will line up for a hayride. When done with the hayride, the child will go into the house, clean up, and sit at the table, waiting for everyone else to arrive before eating. Note: Child process 8 has a special requirement: the Mother process must accompany this child on the hayride; therefore, this child must wait for the mother process to finish preparing the meal. When done eating, the child processes wait to be excused from the table and then are all done (they can go out and play).

Relative (aunts and uncles) process: These adult processes (6 total) arrive, go on a hayride, clean up and sit down at the table. As with everyone else, they cannot eat until everyone is seated and the Father process has carved the turkey. They eat, wait to be excused from the table, and then they return home.

The hayride rules are as follows:

No one eats until everyone is ready and the turkey has been carved. No one is allowed to leave the table until everyone is done eating. Only the Father process can excuse people from the table.

The hayrides are given by the Father process. The Father process hooks up two horses to a wagon full of hay and drives the horses around a 100-acre forest and then back to the house. That constitutes one ride. Since the horses are older, the Father process is concerned with them pulling too much weight. Therefore he limits the number of people (in addition to himself - meaning the father does not count as an adult on the hayrides) on any one ride to 3 kids or 1 adult and 2 kids or 2 adults (this is the order of preference if there is a tie when a choice is to be made). This is a first come, first served situation (after these group rules have been applied). If you use semaphores, you do not need to worry about the lack of FIFO ordering when removing processes from the queues. If you use monitors, you should enforce FIFO. The father wants to limit the number of rides, but toward the end, he will give a ride to only one or two children if there is no one else waiting, or to only 1 adult in the same situation.

If there are specific situations not covered by the above rule, you can opt to deal with them however you choose, but you must add comments on your code to explain what you are doing in that situation.

Given the following: Suppose Child 1 and Child 2 are waiting. Now Relative 1 and Relative 4 arrive. The Father would take Child 1 and Child 2 along with Relative 1 before he would take the two relatives. Suppose Child 1 and Child 2 were in line, and the Mother arrives. The Father would wait unless these were the only two children left besides Child 8 and there were no other adults. If there are no more children (besides Child 8) and no more adults, then the Father would take Child 1 and Child 2 on a hayride and then return to wait for Child 8 (so Child 8 and the Mother can go together). If there were Relatives that hadn't taken any hayrides, one of these adults would need to go with the two children that are left.

Possible hayride scenarios include giving rides to groups as follows:

2 adults; 3 children, 1 adult and 2 children, 1 adult and 2 children; Mother and Child 8; 2 adults
1 adult and 2 children, 1 adult and 2 children, 1 adult and 2 children; 2 adults; 1 adult and 1 child; Mother and Child 8
Mother and Child 8 and 1 other child, 3 children; 2 adults; 2 adults, 1 adult and 2 children; 1 adult and 1 child
1 adult and 2 children, 1 adult and 2 children, 1 adult and 2 children; 2 adults; Mother and 2 children; 1 adult


Program must print appropriate messages so that your output clearly indicates who is doing what. The possible output might appear as follows: (using indentation to see who prints is a good idea)
Child 1 is raking leaves.
Mother is making the meal.
Child 2 is raking leaves.
Relative 1 arrives.
Relative 2 arrives.
... (assume all relatives arrive and all children are raking leaves)
Child 1 is waiting for hayride. Relative 1 is waiting for hayride. Relative 3 is waiting for hayride. Child 3 is waiting for hayride.
Father is ready to give hayrides.
Father gives hayride to Child 1, Child 3 and Relative 1.
Child 8 is waiting for hayride.
Child 2 is waiting for hayride.
Child 1 is sitting at table.
Mother is waiting for hayride.
Father gives hayride to Child 2, Child 8 and Mother. (assume all have had hayrides and are seated at table) Father carves turkey.
Child 1 is eating.
Child 3 is eating.
Relative 1 is eating.
Mother is eating.
... (assume they are all eating)
Child 1 is done eating.
Relative 4 is done eating.
... (assume they are all done eating)
Father excuses everyone from table.
Relative 2 goes home.
Child 7 goes out to play.
Mother goes to read her book.
Father goes to watch football.
Child 1 goes out to play.
Please format your output in a legible manner. NOTE: Baci has limited string space. If you get a "string space exhausted error", you may have to shorten the number of strings you are outputting or reduce the number.
You can use a monitor or semaphores, whichever you prefer. You should add random delays (don't make it too large) at various places so the interleaving of processes is more realistic (the delay will simulate the passage of time), for example, when children are raking leaves. You can do this by using a Delay() function:
void Delay(void)
{
int i;
int DelayTime;
Delay Time = random(DELAY);
for(i=0; i<Delay Time; i++ );
}
where the constant integer DELAY equals some number from 10 to 100. Then you can simply call Delay() to simulate the passage of
time.
