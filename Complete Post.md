Hello everyone,
Recently I was part of a great online instructor-led training of DOCKER.
There the instructor Mr. Vimal Daga sir, teach us so many things like
Container
Docker Architecture
Docker Networking
Docker Image
Dokerfile and Docker-Compose
from very basics to advanced level. 

They've managed to excite me about this containerization world so much, So I decided to continue the same to the next level. Then I went through so many articles, blogs.

Then I encountered with some more concept like 
Orchestration
Kubernetes
Docker Swarm
Platform as a Service ( PaaS )
Multistage Build
Microservices
and so many others and I'm trying to figure it out.
And after gaining some sort of confidence in Docker Swarm I've decided to let's integrate whatever I've learned from Mr. Vimal Daga and whatever I've learned from blogs.

So I've created a project for the same. 

Introduction to Project:
	So I've created a WebServer with Wordpress and MySQL database.
which works in multi-host ( and single host architecture as well).
	Multiple containers running on the different hosts connected via Overlay Network. All load balancing stuff is done by Docker Swarm itself( by ingress internally).
	Docker Swarm makes joining more nodes, scaling services so simple.
Just run command and service will scale up or down in seconds.
Even if a few nodes get down, Docker manages to spin more containers to meet the desired state.
	It also comes handy to rolling updates or Rolling back. Everything got easier.
Requirements:
	To utilize its full potential it is recommended to run at least 3 or more Host( maybe VMs, Amazon EC2 instance, GCP, Microsoft Azure, or any other cloud-based service ).

	So if you don't have any like I don't :)
Feel free to use this service https://labs.play-with-docker.com/ . 
You'll need Docker ID for the same.

Step by step guide is in GitHub.
https://github.com/rajneeshmehta/Docker


#righteducation #docker #vimaldaga #iiec_connect #iiec_rise
