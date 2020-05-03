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
 
 <img src="https://github.com/rajneeshmehta/Docker/blob/master/Images/node ls.jpg" alt="alt text" width="900" height="250">
 
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
And two ports pop up like this

<img src="https://github.com/rajneeshmehta/Docker/blob/master/Images/create Service.png" alt="alt text" width="400" height="300"> 

click both ports, It will open two tabs, on port 8089 You can access WordPress site and on port 8080 we can visulaize which node running which services.

<img src="https://github.com/rajneeshmehta/Docker/blob/master/Images/wordpress.jpg" alt="alt text" width="400" height="300">  <img src="https://github.com/rajneeshmehta/Docker/blob/master/Images/visualizer.jpg" alt="alt text" width="400" height="300">


> Be patient it takes time to run container sometimes 20 to 30 sec, to open ports. :smiley:


___

Now you can scale up service by following command
```
$ docker service scale Wordpress_wordpress=5
```

and Output should be like this
```
Wordpress_wordpress scaled to 5
overall progress: 5 out of 5 tasks 
1/5: running   [==================================================>] 
2/5: running   [==================================================>] 
3/5: running   [==================================================>] 
4/5: running   [==================================================>] 
5/5: running   [==================================================>] 
verify: Service converged 
```
And Visulizer tab sholud look like this.

<img src="https://github.com/rajneeshmehta/Docker/blob/master/Images/visualizer_with_5_replicas.jpg" alt="alt text" width="400" height="300">

You can even Scale down service by same command
```
$ docker service scale Wordpress_wordpress=3
```
And Output looks like this
```
Wordpress_wordpress scaled to 3
overall progress: 3 out of 3 tasks 
1/3: running   [==================================================>] 
2/3: running   [==================================================>] 
3/3: running   [==================================================>] 
verify: Service converged 
```
And Visulizer tab sholud look like this.

<img src="https://github.com/rajneeshmehta/Docker/blob/master/Images/visualizer_with_3_replicas.jpg" alt="alt text" width="400" height="300">

> Your Figure may vary.:relaxed: :thumbsup:

To stop service Run following command
```
$ docker stack rm Wordpress
```
And Output looks like this
```
Removing service Wordpress_database
Removing service Wordpress_visualizer
Removing service Wordpress_wordpress
Removing network Wordpress_default
```

to Ensure it's Gone run Following command
```
$ docker stack ps Wordpress
```
And Output looks like this
```
nothing found in stack: Wordpress
```
> If you see something other then this notice DESIRED STATE column it is remove. Wait for some time and Run above command again. 
