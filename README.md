Note: I forked this from https://github.com/domardfern/Nubot-Simulator. However, I have found a more recently maintained fork of this project here: https://github.com/danielthank/nubot-simulator
so I am abandoning and archiving this fork, and starting again with a new fork at https://github.com/chigozienri/nubot-simulator based on danielthank's fork.


###Nubot Simulator
======
The Nubot Simulator is a tool built to help researchers model their Nubot configurations and rulesets. This simulator has a number of features including but not limited to:

* Video Export
* Simulation Speed Changes
* Configuration Editing

###Compiling the Simulator
======
Open the directory in Eclipse. Choose Export>Runnable JAR file>Package required libraries into generated JAR>Finish
To compile manually, note that you need the JDK, not just the JRE (not included by default in OS X), and you need to explicitly tell the compiler to include the JARs inside the lib folder in the classpath:
```
cd src
javac -cp ../lib/monte-cc.jar:../lib/javatuples-1.2-javadoc.jar:../lib/javatuples-1.2.jar: -d ../classes Main.java
```
If you do it manually, you also need to explicitly give the classpath when you run the program (otherwise it will load, but crash when you try to load a ruleset:
```
java -cp ../lib/monte-cc.jar:../lib/javatuples-1.2-javadoc.jar:../lib/javatuples-1.2.jar: Main   
```

###Running the Simulator
======
Double click on Nubot-Simulator.jar (unless you have compiled by hand, in which case you will need to run from the command line (see above)

###Using the Simulator
======
You are not allowed to start the simulation until both the configuration and ruleset files are loaded. However, in the case of testing a system that uses only agitation, you may simulate as long as a configuration is loaded and agitation is turned on.

####Loading a Configuration
======

One of the first things you'll want to do in order to simulate a system is load the seed configuration file. The simulator uses its own format and extension.

The configuration file format ends with the .conf extension and looks something like this:

```
States:
x, y, state

Bonds:
M1.x, M1.y, M2.x, M2.y, bondTYPE
```
Each monomer is specified under the 'States:' directive and consists of: the x coordinate, y coordinate and state.

Bonds between monomers are specified under the 'Bonds:' directive following the monomer declarations. Bond declaration consists of: the x & y coordinate of the first monomer, the x & y coordinate of the second monomer, followed by the type of bond between them.

Bond Types: 0 - null, 1 - rigid, 2 - flexible.

Example: rulesets/walker.conf

####Loading a Ruleset
======
Before you can start a simulation you must load a configuration and, unless you are testing agitation, a ruleset. The simulator uses its own format and extension.

The ruleset file format ends with the .rules extension and more closely follows the specifications presented in the model for interactions:

```
M1.state M2.state bondTYPE Direction M1'.state M2'.state bondTYPE' Direction'
```

Directions: NE, E, SE, SW, W, NW

Example: rulesets/walker.rules
