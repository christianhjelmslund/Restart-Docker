# Restart Docker
Sometimes it is a good practice to remove your docker containers and prune the system. It can quickly become a bit messy with several containers running and especially when you stop them, there is still an unused instance of them. You can actually stop and remove all existing containers with
``` bash
docker rm -f $(docker ps -a -q)
```
and to prune unused containers, networks etc with:
``` bash
docker system prune
```
___

Might seem a bit of an overkill to make a bash script to run two commands. But they are run often if you work with several docker containers and the idea about this repo, is also just to show how to add an executable script that is accesible from anywhere.

Download the bash file, [restart_docker](https://github.com/christianhjelmslund/restart-docker/edit/master/restart_docker.sh) and place it where you want on your computer. This is for a OS X Unix system (Mac and Linux), so Windows guys, yeah, not this time :-) Just FYI, this is done on Mac.

Navigate to that directory and if you run 

``` bash
./restart_docker.sh
```
you'll get an error: ``` bash ./restart_docker.sh: Permission denied ```

This is due to the fact that it isn't an executable, so you have for sure done this before, but might wondered why/what's up with this weird syntax, but by running chmod +x, you make the file an exectuable. So run:
``` bash
chmod +x restart_docker.sh
```
to make it an executable file. Now, if you try to run 
``` bash
./restart_docker.sh
```
you'll see what you expect. Anyways, that is nice I guess, but if you navigate to a different directory and runing ```./restart_docker.sh``` it won't, because yeah, the file is not in that directory. So, what you want to do is to move the file to your PATH, which by default is in:
``` bash
/usr/local/bin
``` 
but to be sure, you can always find the path by running: ```echo $PATH ``` 
which will show you something like: 
``` bash
/usr/local/bin:/usr/bin
``` 
You may wonder why you cannot use ``` /usr/bin ``` and well, you can, but that directory contains executable programs that are installed by your package managers, so the right way to do it is to store it in ```usr/local/bin```. So let's go ahead and do that. Make sure you are in the correct repository and then run:

``` bash
mv restart_docker.sh /usr/local/bin
ls
``` 
The reason I also run ``` ls ``` is just to show you that the file is not in the directory anymore (mv = move, cp = copy). But if you run
``` bash
restart_docker.sh
```
you'll see it still works! Now, just to top it off and make it a bit more nice, we can also add an alias. This means, that we can run the above script, with a different alias. So, you should have a ```~/.bash_profile``` file, if not, you create it. It is a configuration file for configuring user environments, in this case an alias. Open the file with your favorite texteditor, for example ``` vim ~/.bash_profile ``` or if you're an atom guy: ``` atom ~/.bash_profile ``` and add this line:
```
alias restart='restart_docker.sh'
```
which gives the restart_docker.sh an alias, restart. You can of course choose a different name. Now, an **important(!)** part is to close your terminal and restart it again. If you don't do that, it will not have updated the alias. When you have restarted it, you can just type ```restart``` and it will clean up your docker containers. This can be done everywhere you navigate now. Again, the reason for this repo is more on how to add scripts to your path, so be creative and make your own scripts that you use often.



