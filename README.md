# Docker

I've Made this Project just to demonstrate Docker Swarm Orchestration

To recreate this project please follow instruction.:point_down::point_down::point_down:

___
## Set up Environment:
Step 1. open [https://labs.play-with-docker.com/](https://labs.play-with-docker.com/) in your browser.

Step 2. Login with Your DOCKER ID.


<img src="https://raw.githubusercontent.com/rajneeshmehta/Docker/master/Images/login.jpg" alt="alt text" width="400" height="300">

Step 3. After succesful Login You should something like this.

<img src="https://github.com/rajneeshmehta/Docker/blob/master/Images/Start.jpg" alt="alt text" width="400" height="300">

Step 4. Click Start and You should see something like this. 

<img src="https://github.com/rajneeshmehta/Docker/blob/master/Images/InkedQuick_LI.jpg" alt="alt text" width="400" height="300">  


> For sake of simplicity Instead we add multiple instances and make them part of Swarm, we'll gonna use predefined Templates.
```
Behind the scene they run follwing command.

  $ docker swarm init --advertise-addr $(hostname -i)

this command make current node as leader and manager.and also provide token and command to add node as worker.
looks like this

  docker swarm join --token SWMTKN-1-0t4aweh5kkdkj27vsmqc7decbribadn683cm6pmsx6m2uxnf2e-6qfilnwulc2xa9h7nlml5vruy 192.168.0.44:2377

in your case it might be diiferent.

to add manager run this command

  $ docker swarm join-token manager
  
which provide you token like this
  docker swarm join --token SWMTKN-1-0t4aweh5kkdkj27vsmqc7decbribadn683cm6pmsx6m2uxnf2e-1qgxgff9j5593qzksbk2qfvl4 192.168.0.44:2377
  ```
 Step 5. After you've created Cluster ( in either way ), you must have some manager and some worker.
 > It's always advised to have odd more then one managers (3, 5, 7..), to ensure we always can elect one leader if first leader goes down.
 Just for quick sanity check run this command
 ```
 $ docker node ls
 ```
 it should show somthing like this. ( note leader may differ in my case it is node 3 )
 
 <img src="https://github.com/rajneeshmehta/Docker/blob/master/Images/node ls.jpg" alt="alt text" width="400" height="300">
 
 > this command list all nodes in Swarm.
 
 Now we are good to go now,
 Run follwoing command.
 ```
 git clone https://github.com/rajneeshmehta/Docker.git
 cd Docker
 ```
 Step 6. Run following command to start MultiHost Service.
 ```
 $ docker stack deploy --compose-file docker-stack.yml Wordpress
 ```
 You should see output like this
 ```
Creating network Wordpress_default
Creating service Wordpress_database
Creating service Wordpress_wordpress
Creating service Wordpress_visualizer
```
