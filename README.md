## DockerUI

DockerUI is a web interface to interact with the Remote API.  The goal is to provide a pure client side implementation so it is effortless to connect and manage docker.  This project is not complete and is still under heavy development.

### Quickstart 

#### Step 0

/etc/default# vim docker.io 
Copy this line to docker.io file

DOCKER_OPTS="-H unix:///var/run/docker.sock -H tcp://0.0.0.0:4243 -api-enable-cors"

/etc/default#service docker.io status
/etc/default#service docker.io start



#### Step 1
  
Pull the latest image:  
  
```
docker pull madhavkobal/dockerui:latest
```
  
#### Step 2
If you're running Docker using a unix socket (default):  
  
```
docker run -d -p 9999:9999 -v /var/run/docker.sock:/docker.sock \
--name dockerui madhavkobal/dockerui:latest -e="/docker.sock"
```
  
If you're running Docker over tcp:  
  
```
docker run -d -p 9999:9999 --name dockerui \
madhavkobal/dockerui:latest -e="http://<dockerd host ip>:4243"
```
  
#### Step 3
Open your browser to `http://<dockerd host ip>:9999`  

Or

If you're running Docker using go server: 

Extract your downloaded zip file dockerui-master.
Run go server using :
 go run dockerui.go
 Open your browser to `http://localhost:9999` 
  
  
#### Warning
Bind mounting the unix socket into the DockerUI container is much more secure than exposing your docker 
daemon over TCP. You should still secure your DockerUI instance behind some type of auth.  Maybe running 
Nginx infront of DockerUI with basic auth.  
  
### Screenshots
![Dashboard](screenshots/Commit.png)
![Dashboard](screenshots/Dashboard.png)
![Dashboard](screenshots/Pull.png)
![Dashboard](screenshots/Push.png)
![Dashboard](screenshots/container.png)
![Dashboard](screenshots/containers.png)


### Goals
* Little to no dependencies - I really want to keep this project a pure html/js app.  I know this will have to change so that I can introduce authentication and authorization along with managing multiple docker endpoints. 
* Consistency - The web UI should be consistent with the commands found on the docker CLI.

### Stack
* Angular.js
* Flatstrap ( Flat Twitter Bootstrap )
* Spin.js
* Ace editor

### Additional Functionalities
* Search repositories from docker hub
* Pull repositories from docker hub
* commit container
* Push files to a docker hub
 

### License - MIT
The DockerUI code is licensed under the MIT license. Flatstrap (bootstrap) is licensed under the Apache License v2.0 and Angular.js is licensed under MIT.

**DockerUI:**
Copyright (c) 2013 Michael Crosby. http://crosbymichael.com  
  
Update credits:  
Abhinav Ajgaonkar http://blog.abhinav.ca  
Ryan Krieg http://ryankrieg.com  
  
Permission is hereby granted, free of charge, to any person
obtaining a copy of this software and associated documentation 
files (the "Software"), to deal in the Software without 
restriction, including without limitation the rights to use, copy, 
modify, merge, publish, distribute, sublicense, and/or sell copies 
of the Software, and to permit persons to whom the Software is 
furnished to do so, subject to the following conditions:
  
The above copyright notice and this permission notice shall be 
included in all copies or substantial portions of the Software.
  
THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND,
EXPRESS OR IMPLIED,
INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, 
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. 
IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT 
HOLDERS BE LIABLE FOR ANY CLAIM, 
DAMAGES OR OTHER LIABILITY, 
WHETHER IN AN ACTION OF CONTRACT, 
TORT OR OTHERWISE, 
ARISING FROM, OUT OF OR IN CONNECTION WITH 
THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
