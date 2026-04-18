  today we will try to run a custom node script , it will detect the node health of of virtual machine:
  
  so we have written a nodeHealth.sh shell script in our ec2 instance (virtual machiene of ubuntu), that will give us info in terms of parameters about the cpu, memory, and processes that are used and free.
  
  set -x --> x is debug mode, will give command and its output
  
printing all processes in this ec2 instance (vm):
ps -ef -> ps for processes and ef for details of processes
(stoped, running, daemon processes)


find the procceses that is run by amazon and get their ids.
	ps -ef | grep "amazon" -> give process details
	now, just process id
		ps -ef | grep "amazon" | awk -F" " '{print $2}'
understand the command:
	1. ps -ef -> info about the processes
	2. grep " " -> fetch specific things from output
	
pipe parameter (|) -> link both commnad and sends the output of the first command to the second command


example:
	exmple.sh
	chmod 777 exmple.sh
	./exmple.sh | grep 1 -> give specific output from the results
	or we can use 
			grep 1 exmple.sh
INTERVIEW QUESTION:
	
	whats the output of:
		date | echo "date is "
		date is system default command and send result to stdin channel (linux has channels like stdin , stdout, stderr), pipe only send result that is output to another command but date is sendng output to stdin, thats y. pipes do not recieve info from stdin.
		
		
people also use the cut, trim and awk, awk is very pwerfull.

awk is pattern scanning and processing language.

awk can be use to fetch specific results from the output.

defference between grep and awk command:
grep gives u entire statements that is matched with the pecified paramenters but awk can give u specific cols from the output.

ps -ef | grep "amazon" | awk -F" " '{print $2}'
	we can mention any col(considering each a string and give index numbers) to get the specific results from the output.
	
grep will output the whole row if found match and using awk we can get specific output from results.

whenevr u use pipes in scriptes, also use commands like set -e and set -o
why:
	purpose of set -e:
		exits the script when there is an error, if uh have error on line 1 and u didnt used set -e command, all the script will still run which is not a good practise.
		exmple:
			u have a flow 
			create user -> create a file -> write the user name to the file
			if u have error on line 1 and 2 will get exectued then whats the reason of making the script. so thats y we have to use the set -e command so if there is error, script will not run.

Drawback of set -e:
	it do not give error if there is pipe fail.
	thats y we have to use set -o command.
	
set -o :
	 set -e sees the if the last command is true/correct, it get passed and if not correct, it stoped and gives error.
	 consider:
		asdjdsjdn | echo 
		it will get passed , even if first has error but second is correct
		now consider this:
		asdasds | echo | asadf
		it will get stoped cz there is error in last command
		
	so, set -e will still run if there is pipe fail, thats y we have to use set -o for it.
	
----------------------------------------------

if the vm is failing , you will go and look into the log files and find errors
devops engineers go and look into the log files about the erros that y the application is failing.

command :
cat logfile | grep error

when there are alot of log files, people store it in external storgae like s3, azure,  or google storage.


to access such files, u provide the url of the log file and use curl command.

curl command retrieve info from internet, u can use it with the logfile url (form internet / browser url) and it can print it.

like postman that helps u crate api request, curl do the same
	
		curl https:// ----- | grep "error"
		
	curl -X GET api.food.com
	fro api we can get info
	
	
wget command:
	wget download the file, unlike curl which just print the data
	
------------------------------------------------

find command:
	as we are in the aws linux system wheich we have created, and it is default so we have some limited or less files we can check with :
	ls /etc/
	
in your day to day vm, u can mount new volumes for stoing different log files, so how do you find files?

find command give you the location that you are looking for a file.
command:
	sudo find / -name pam # pam is file name, we have used sudo cz we will get permisiion denied	
	
chnaign to root user:
	sudo su -
	
	uh can then logout-> logout
	using su (switch user) you can chnage to any user 
	
	 with sudo (substitute user do), you get priviliges as root
	 
	 u go as root user, to some specific commands
	 
	
