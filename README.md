# deckbuilder

![alt text](https://raw.githubusercontent.com/1c3be4r/stash/master/deckbuilder.png "deckbuilder")

## Table of Contents
1. Summary and Methodology
2. Walkthrough
3. Under the Hood


## Summary and Methodology

This script, deckbuilder.cna, utilizes the **argue** command introduced with Cobalt Strike v 3.13. It will take a list of already defined programs, such as *cmd.exe* or *wmic.exe* and generate fake arguments for those commands. These arguments will appear when the commands are executed via **&run** in the beacon console.  

If an argument genreated by the initial command, **shuffle**, is insufficient then the operator can **mulligan** that command until they find one suitable for their needs; the **mulligan** command does not need to already be in the pre-compiled list.

It should also be noted that these argument spoofs are *paper thin*. They may stick out like a sore thumb to a defender that is looking, but it is better than them catching your entire lateral movement command via ETW.

## Walkthrough

Finally: the "just tell me how to turn the damn thing on" portion of the README. 

### 1) Load deckbuilder.cna

Load the script via Cobalt Strike -> Script Manager.

![alt text](https://raw.githubusercontent.com/1c3be4r/stash/master/deckbuilderstep1.png "Step 1")

### 2) Run the shuffle command

Run the **shuffle** command to generate arguments for common arguments executed via **run**.

![alt text](https://raw.githubusercontent.com/1c3be4r/stash/master/deckbuilderstep2.png "Step 2")

### 3) Modify and tweak commands via mulligan

Modify any commands that do not fit your needs via the **mulligan** command. Keep running **mulligan** until you find something you need. This also allows you to spoof commands that are not in the initial list (example: if you need to upload your own binary and execute it via **&run**.

![alt text](https://raw.githubusercontent.com/1c3be4r/stash/master/deckbuilderstep3.png "Step 3")

### 4) Kill the spoofs

If you ever need to wipe the argument list, run the **argue_off** command to wipe the commands from the pre-compiled list.

![alt text](https://raw.githubusercontent.com/1c3be4r/stash/master/deckbuilderstep4.png "Step 4")


## Under the Hood

Deckbuilder uses a series of precompiled lists to generate and randomize arguments. It uses random number seeds to generate types of numers generated. The randomization of the file paths, file names, file extensios, and input/output redirection all come from lists that can be modified. 

The deckbuilder.cna script then takes these randomized argumens and executes them on a beacon via &bargue_add, &bargue_list, or &bargue_remove.
