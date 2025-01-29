# Thanksgiving Dinner Synchronization (C Mini)

This C mini program simulates a Thanksgiving family gathering with concurrent processes, demonstrating classical synchronization problems like producer-consumer and dining philosophers. It utilizes semaphores to coordinate the actions of different family members (Mother, Father, Children, and Relatives) involved in meal preparation, hayrides, and dinner, ensuring controlled access to shared resources and preventing deadlocks and race conditions.

## Description

The program models a Thanksgiving scenario with various processes representing family members:

*   **Mother:** Prepares the meal, goes on a hayride with the youngest child (Child 8), returns, sets the table, and eats.
*   **Father:** Gives hayrides, unhooks the horses, cleans up, carves the turkey, and eats.
*   **Children (8):** Rake leaves, go on hayrides, clean up, and eat. Child 8 must be accompanied by the Mother on the hayride.
*   **Relatives (6):** Arrive, go on hayrides, clean up, and eat.

The program simulates these activities concurrently, synchronizing them using semaphores to adhere to the following rules:

*   **Hayrides:** The Father gives hayrides with a limited capacity (up to 3 children, or 1 adult and 2 children, or 2 adults).  Hayrides are on a first-come, first-served basis within these group constraints. The Father prioritizes groups of 3 children, then 1 adult and 2 children, then 2 adults. He also handles edge cases like the last few riders.
*   **Meal:** The Mother prepares the meal.
*   **Dinner:** No one eats until everyone is seated and the Father has carved the turkey. No one leaves the table until everyone has finished eating and the Father excuses them.

## Build Instructions

This program is written in C mini and requires a C mini compiler and execution environment.  Because C mini is a simplified language, it often comes as part of an operating systems course or textbook.  Consult your course materials for how to compile and run C mini programs.  A general outline would be:

1.  **Save:** Save the provided code as a `.c` file (e.g., `thanksgiving.c`).
2.  **Compile:** Use your C mini compiler to compile the code.  The exact command will depend on your compiler.  It might look something like:  `cmini thanksgiving.c -o thanksgiving`
3.  **Run:** Execute the compiled program.  Again, the command is compiler-specific but could be: `./thanksgiving`

## Usage

After compiling and running the program, the output will show the actions of each family member, indicating who is doing what at each stage (raking leaves, waiting for hayride, on hayride, sitting at the table, eating, etc.). The output is formatted to be readable and demonstrate the concurrent execution and synchronization.

## Code Explanation

The code utilizes semaphores for synchronization:

*   `mutex`: Protects shared variables like `waiting_children`, `waiting_adults`, `eating_count`, and `seated_count`.
*   `hayride_ready`: Signals that a hayride is ready to begin.
*   `all_done_eating`: Signals that everyone has finished eating.
*   `mother_hayride`: Signals that Child 8 is ready for the hayride with the Mother.
*   `seated_mutex`: Protects the `seated_count` variable.
*   `all_seated`: Signals that everyone is seated at the table.
*   `turkey_carved`: Signals that the turkey has been carved.
*   `done_eating`: Signals that everyone is done eating.
*   `print`: Controls access to standard output to prevent garbled output.
*   `aDone[7]`: Signals relatives are done with the hayride.

The `cobegin` construct creates concurrent processes for each family member. The code implements the logic for hayride groups, meal preparation, and the synchronized dinner using wait and signal operations on the semaphores.  Random delays are introduced using the `Delay()` function to simulate realistic timings.

## Authors

Fardeen Shahed, Rohan Mankame

## Date

Fall 2024

## Course

CMPSC 472-002

## Acknowledgements

This project was completed as part of the CMPSC 472 Operating Systems course at Penn State University.
