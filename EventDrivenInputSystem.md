# Introduction #

The current input system in GrafX2 uses a polling scheme like it was done in the DOS days. This worked fine at the time, but it nows feel a bit limitating. This page gathers ideas and technical solutions to improve that and get something better. Objectives include :
  * Don't block the mouse even when the program is really busy with something (like 24bit image color reduction)
  * Don't have the mouse cursor lag behind even if there is an expensive drawing op running
  * Allow for some multitasking so the mouse can still move while playing an animation at a constant framerate


# Details #
The main idea is to replace SDL\_PollEvent with SDL\_WaitEvent in get\_input. This allows to make the function block and exit only when there is an usefull event, without any "busy waiting" on our side. Less CPU usage, less code, everyone is happy. However this has one drawback : the blocking function will make things like airbrush not work if you don't move the mouse.

To avoid that, we need a new event created by software to be generated at a constant rate a bit like a VBL retrace interrupt (without the VBL retrace). This can be done with an SDL timer sending an SDL\_PushEvent. The timer could also call some other functions directly for high-precision asynchronous timed things like playing an animation.

# Mouse cursor thread #
Have a thread handle mouse cursor movements. It can take care of merging mouse events if needed/wanted, displaying only the cursor, and let the current operation draw the heavy things below.
Need to be really carefull to not allow muliple operation to be started at the same time.
This thread can also poll the keyboard and be used to add a shortcut to undo a long running operation (like rendering of a distortion for an animation once you see it's going to look really wrong and want to change it anyway).

# Heavy multithreading #
Add support for multiple thread to use the full power of modern multicore computers. For example 24-bit color reduction could benefit from that and be made about twice as fast (both palette generation (only the cluster list needs locking) and image reduction (no locking needed if the threads work on different parts of the picture).
It needs proper locking on screen access for some things however, like any threading (also applies for the mouse thread). So beware. Excessive locking will make it not-so-usefull.

Lua scripts could also run from threads (only one script at a time as the Lua interpreter is not fully safe, I fear) and do thing in realtime for an animation, for example (like altering the pixel data).

# Event locking #
Instead of calling get\_input explicitly, everything could just block on a semaphore or a condition variable that would be released when an event occurs. Same apply for the "Wait\_VBL"-synced things. It avoid playing with getticks and all this stuff. Everyone would lock on a condition variable, then the "VBL" timer would send a global signal to tell them to go ahead.

# SDL support #
SDL provides timers, threads, semaphores, and all that stuff. So all of this can be done in a proper portable way.