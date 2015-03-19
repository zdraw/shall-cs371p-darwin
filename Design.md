# Darwin #
The Darwin class is essentially responsible for orchestrating the game simulation. Its member data consists of:
  * A 2D Creature vector 'creatures' which represents the grid in which the simulation occurs
  * ints 'r' and 'c,' which keep track of the last location that Darwin iterated through in the simulation.

At each 'step' of the simulation:
  * Darwin's simulate\_turn() method is called. This iterates through the Creatures array left to right and top to bottom. One by one, Darwin allows each Creature to act. It uses the 'acted' flag to make sure that a Creature doesn't perform more than one action during each simulation step.
  * The acting Creature is allowed to run through it's own Creature code, making calls to Darwin in the event that it needs information about its environment.
  * The creature will eventually perform an action and set its 'acted' flag.
  * When a Creature asks for information about the environment or requests to perform an action, Darwin's creatureStuff() method is called. This switch statement uses Darwin's 'r' and 'c' indicator's of the calling Creature's location to examine the relevant area around the Creature. In the event that the Creature is acting, it changes the area around the Creature accordingly.

# Creature #
In accordance with the OO principle of encapsulation, each creature is aware of only its own state and not it's status in Darwin's overall grid. Creature is responsible for keeping track of:
  * it's program counter, 'pc'
  * a boolean flag 'acted,' which records whether the creature has acted yet this "turn"
  * it's direction, 'dir'
  * a pointer to the Darwin it's located in, 'darwin'
  * a pointer to its species vector
In the event that a Creature is infected, the creature's program counter is set to 0 and its Species vector pointer is changed. Everything else about the creature remains the same. This allows the infected creature to start its new Species code in the same location where it left off before it was infected.

# Species #
Keeping things simple, we've chosen to store each species' instructions in its own string vector.
  * The first n-1 elements represent the species' instruction
  * The nth element is display character for when the species is printed as part of Darwin's grid.

  * Creature's act() method is easily able to parse these strings and interprete them as commands.
  * In the event that a paramater (such as a line number, etc) needs to be passed with the command, it is simply appended to the end of the command's string.