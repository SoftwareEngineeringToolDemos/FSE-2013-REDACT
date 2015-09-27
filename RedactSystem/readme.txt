Pre-requisites:

1) You need the derby network server running in your system.
   http://db.apache.org/derby/papers/DerbyTut/ns_intro.html

2) You need to have JMeter installed in your system.
   http://jmeter.apache.org/

3) YOu need to have java (JDK) installed in your system
http://www.oracle.com/technetwork/java/javase/downloads/index.html
   

Description of the files in the directory:

i) transactions: in this subdirectory you have to put the transactions file
 naming in the order of T0.txt, T1.txt,...,Tn.txt. As an example, we put four transaction files
 that was used for the HIM application. 

ii)(B)aselineSystem.jar: executable jar that runs the baseline system.

iii)(G)racefulSystem.jar: executable jar that runs the graceful system.

iv)(R)edactSystem.jar: executable jar that runs the redact system.

v)client.jar: jar files that you specify in JMeter to point out the location of TCP Client class.

vi) cycles.txt: here we specify the cycles that exist among the transactions. You specify
   a cycle with a list of comma separated transaction file names.Please open the default file to see an example.

vii) readme.txt: instructions to run the product.

viii) JMeterFile.jmx: you have to open this file from JMeter. Then you can change the settings as per your requirements.


Execution Instructions:



The easiest way to run the applications is to extract all the transactions from them 
and put them in the 'transactions' directory. You don't need to run the whole 
application as we are only concerned with the transactions in those applications.
The execution time for the application is little relevant to the execution of 
transactions in Database.

Settings: 

Redact System part-

1) Under 'redactSystem' directory open the 'cofig.properties' file
2) set the database connection property.
For example, if the derby database server runs at port 
1527 of my localhot and the database 'HIM' is located under the directory DATABASES in C,
it should be like the following:
 
db.connectionURL=jdbc:derby://localhost:1527/C:\\DATABASES\\HIM

3) set the inputTransactionsDirectory property, in our case which is the directory 'transactions'.
4) set the 'noOfTransactions' property like the following:
	noOfTransactions=4
Note that default value of this peoperty is 4 for the 'HIM' application. You have to change that each time you run 
experiments with different application.



JMeter Part-

1) go to the 'bin' directory of JMeter installation.
2) open user.properties 
3) add a line at the end like the following:
   noOfTransactions=4
Note that default value of this peoperty is 4 for the 'HIM' application. You have to change that each time you run 
experiments with different application.


Running instructions:

JMeter Part-

1) Go to the 'bin' directory of JMeter installation.
2) Double Click on 'Jmeter.bat' file
3) Go to FIle menu and open the 'redact.jmx' file from the 'redactSystem' directory.
4) Click on TestPlan and you need to set the jar file as 'client.jar' in 'redactSystem' directory by clicking
 on 'Browse' button at the bottom part of the page.
5) Expand 'Test Plan' and select 'Redact Thread Group'.
6) Number of Threads(user) is 10 by default. Change it as required (100 or 1000).
7) Expand 'Redact Thread Group' and select TCP Sampler
8) make sure the TCPClient classname is set as 'redactClientServer.MyTCPClient'.
9) also, make sure the server name and port are set as localhost and 7777.
10) please note that, at this point you dont run the JMeter.JMeter is run after following the steps 
in the following.

Redact System part-
1) Go to the 'redactSystem' directory and run any of the jar file as required from the
following list:

a) To run Baseline System type: java -jar (B)aselineSystem.jar
b) To run Graceful system type: java -jar (G)racefulSystem.jar
c) To run Redact System type:   java -jar (R)edactSystem.jar


Now, You can hit the 'start' button in JMeter.


At this point, you can observe the result. every minutes system print the
total execution status. 

For example, following output shows that, the system has iterated or
run for 4 minutes. By that ime, it detects 4 deadlocks and 8 other exceptions. Othe exceptions 
could be a exception when derby refuse to serve the client as it has a limit on maximum 
number of clients per unit of time that it can serve. The total number of successfully executed transactions
are 17 and per transactions statistics also shows the number of executions
for each individual transation. In our default case, it shows for 4 transacions for 'HIM'
application.

Iteration number: 4
Detected deadlocks: 4
Other exceptions: 8
Total transactions executed : 17
Per transactions statistics: : [8, 4, 5, 0]


In case of any difficulties, please feel free to contact via the email given below.

Thank You.

B. M. MAINUL HOSSAIN
PhD student
University of Illinois at Chicago
email: mainul.raju@yahoo.com


