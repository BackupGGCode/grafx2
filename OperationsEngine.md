# Principle #

What is an operation? It's mainly the use of a drawing tool (for example: the freehand drawing tool). More precisely, it's **the management of the mouse's actions while it is above the pixels of the edited image**. Hence, the color picker management is also handled through operations.

The engine which is in charge of these operations is as simple as possible. Its principle is the following: when the mouse is above the picture, the main loop of GrafX2 (located in **MOTEUR.C** ("moteur"="engine")) determines the **atomic part** of instructions to execute, then **executes it**, for each combination of a **type of operation** (an integer that we'll call here ID\_OP), an indicator of the **sate of the mouse** (actually the state of its buttons, also coded on an integer), and the **size of a stack** (not the system stack but a stack of 16-bit words exclusively dedicated to operations, so that they can store parameters for next operations). We call "atomic part" a **sequence of instructions that must be integrally executed at each iteration of the main loop**. It only does what it has to do at some event implied by the combination (ID\_OP, State of mouse, Size of stack) for which it is called.

In fact, the engine has to be assisted for determining the insctructions to execute. Each of these atomic parts is defined as a function containing all the necessary code. These functions are what we called "fonction\_action" (definition in STRUCT.H), i.e. a simple function that **receives no parameter and returns none**. A simple void My\_function(void)...

It's not in my intention to teach you how to write such atomic functions. In the case of the simplest functions to implement following this principle, the conception of atomic parts is quite intuitive, but it happens in certain cases that the method reaches its limites. It's then necessary to **cheat** a little bit (but gently! - by **placing arbitrary values in the stack** only to produce a transition to another combination, therefore another atomic part, for example). You'll find every examples you could need in file OPERATIO.C.

After having written the atomic parts that will be necessary for the management of a whole operation (in file OPERATIO.C), and having written the prototypes of these functions (in OPERATIO.H), you must indicate to the engine in **which conditions** it must use these functions. This is done in the **initialization process** of the program (located in file INIT.C), where we describe each atomic function with the **combination of values that must trigger the call** of the function. The function used to describe all atomic functions only fills a **table** called "Operation" (global variable declared in GLOBAL.H and **indexed by the 3 values of the combination**: ID\_OP, State of mouse, Size of stack) with the address of the function to call. This table will be used by the engine to call directly the atomic function corresponding to the current combination of states, without having to run a bunch of heavy tests (swich/case).

As we had a feeling that these atomic functions could often need to systematically hide the mouse pointer for displaying things on the screen/image and then show it back, we have added a **boolean** in the table Operation which indicates whether the atomic function **demands the engine to handle the visibility of the mouse pointer during the operation**. Finally, I'm not sure this was really useful, but I explain it anyway so that you can understand what the "hide mouse" parameter, needed in the initialisation of the atomic function, stands for.

It is important to note that there is **always** an atomic function called by the main loop, independently from fact that the state of the mouse changes or not. These **repeated calls** permit, for example, to have a **continuous spray** when the mouse button is pressed, even if the mouse is not moved.

Moreover, the atomic functions do not have to care about the position of the mouse because as soon as there is some data in the stack (generally after the first click), **the engine prevents the mouse from leaving the drawing area**. The engine also ensures that the mouse **does not crosses the splitting bar** in "magnifier" mode. At last, **don't forget to empty the stack** when the operation must end! ;-)

# Information for implementation #

  * The initialization of an atomic function is done in INIT.C by:
`Initialisation_operation(ID_OP, State of mouse, Size of stack, Callback, Hide mouse);`

  * The stack dedicated to the operations for the storage of parameters:
    * It contains **16-bit words** (type word, defined in STRUCT.H)
    * For putting a value: `Operation_PUSH(val)`
    * For removing a value: `Operation_POP(&var)`
    * Examples of values that can be stored : mouse or paintbrush **coordinates**, **colors**, any values for changing the size of the stack...
  * Inside an atomic function :
    * If the function corresponds to the **first stage** of an operation, call `Initialiser_debut_operation()` (="initialize start of operation")
    * If the function corresponds to the first stage of an operation that will **modify the picture**, call `Backup()` before the modification of the picture; this will allow the user to **cancel the modification** with "undo" if he wishes to.
    * For displaying the mouse coordinates, call `Print_coordonnees()` (="print coordinates") without being concerned whether the tool bar is hidden or not. If you need to display relative or absolute coordinates (according to the settings chosen by the user), use `Aff_coords_rel_ou_abs(RefX,RefY)` (="Displ coords rel or abs"). If the coordinates are configured as relative, this function displays the difference between the current coordinates of the paintbrush and the coordinates of reference given as parameters. In the case of special information to display in the tool bar, one can use the function `Print_dans_menu(text, position in characters)` ("dans"="in").
    * If you need to ensure that mouse buttons are released before going any further, use `Attendre_fin_de_click()` (=Wait for end of click)
    * Please study OPERATIO.C for examples.
  * For **starting an operation** (after clicking on a button of the tool bar, for example), call `Demarrer_pile_operation(ID_OP)` (start operation stack). Note: the **mouse pointer must be hidden** before the call (and it's state is not modified). (see examples in BOUTONS.C)
  * One can know the ID\_OP of the current operation thanks to the global variable `Operation_en_cours` (="current operation")
  * The global variable `Operation_Taille_pile` (="Operation Stack size") corresponds to the size of the stack dedicated to operations. It can be consulted and modified (even if it's preferable using Operation\_PUSH and Operation\_POP in the latter case).

## How to create a new operation? ##
  * In CONST.H :
add an identifier (ID\_OP) in the enum OPERATIONS (example : OPERATION\_DUMMY)
  * In GLOBAL.H :
add the identifier of the **shape of the pointer** used for this operation in the table CURSEUR\_D\_OPERATION[.md](.md) (="cursor of operation"). Take care to insert at the right place (**place corresponding to ID\_OP** : at the end of the list if ID\_OP was inserted at the end).
  * In OPERATIO.C :
Write every atomic functions of the operation.

# Example #
```
void Dummy_1_0(void)
// Operation : OPERATION_DUMMY
// Mouse click: 1
// Stack size : 0
// Mouse hidden: Yes or No (given thanks to Initialiser_operation() in INIT.C)
{
     Initialiser_debut_operation();
     Backup();

     // ACTIONS...

     Operation_PUSH(some_value_needful_for_next_steps);
     Operation_PUSH(some_other_value_needful_for_next_steps);
}
```

(For this example, the next stage to define will consequently be a stage with the size of the stack equal to 2)

There's a **default action** which only displays the mouse coordinates if no atomic function was explicitly defined for processing a certain combination (ID\_OP, State of mouse buttons, size of stack).

If the operation is a **temporary interruption** of other operations, and that you think you should **restore the previous operation** once it is finished (this is the case of the magnifier, the color picker, the brush grabbing, ...), add the ID\_OP in the corresponding section of the function `Demarrer_pile_operation()`, at the beginning of the file.
If the operation finds an interest in **letting the user change the color of the paintbrush** during the operation (this is the case of two of the freehand drawing modes, the spray, and the rays tools), add the ID\_OP in the corresponding section of the function `Demarrer_pile_operation()`, at the beginning of the file.
  * In OPERATIO.H :
Write the prototype of each atomic function.
  * In INIT.C :
In `Initialisation_des_operations()`, for each atomic function of the operation, write a call to Initialiser\_operation(ID\_OP, State of mouse buttons, Size of stack, Callback, Hide mouse);
    * ID\_OP : identifier of the operation concerned by the atomic function (defined in CONST.H). State of mouse buttons:
      * 0 = no button pressed
      * 1 = left button pressed
      * 2 = right button pressed

(note : the state "more than one button are pressed" does not exist, only the 3 states above are allowed)

  * Size of stack: number of parameters (16-bit words) in the stack
  * Callback: name of the atomic function to call for the combination of the 3 parameters of state
  * Hide mouse: boolean indicating that engine will be in charge of hiding the mouse pointer before calling the atomic function, and showing it back at the end of this function.

Example:
`Initialiser_operation(OPERATION_DUMMY, 1, 0, Dummy_1_0, 1);`