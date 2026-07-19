The project is created on Raspberry Pi 5:
CPU: Broadcom BCM2712 2.4GHz quad-core 64-bit Arm Cortex-A76
RAM: 8GB

### Step 1: I install PI OS on the device. That is a Debian-based OS developed for Raspberry PI.
I install that OS using laptop with the MicroSD reader with 64GB of memory.

### Step 2: I install docker on rpi using terminal. Commands from the official Docker website (https://www.docker.com/products/docker-desktop/) that I used to pull the software in the exact order.
- sudo apt install gnome-terminal
- sudo apt-get update

*Add Docker's official GPG key:*
- sudo apt update
- sudo apt install ca-certificates curl
- sudo install -m 0755 -d /etc/apt/keyrings
- sudo curl -fsSL https://download.docker.com/linux/debian/gpg -o /etc/apt/keyrings/docker.asc
- sudo chmod a+r /etc/apt/keyrings/docker.asc

*Add the repository to Apt sources:*
- sudo tee /etc/apt/sources.list.d/docker.sources <<EOF
>> Types: deb
>> URIs: https://download.docker.com/linux/debian
>> Suites: $(. /etc/os-release && echo "$VERSION_CODENAME")
>> Components: stable
>> Architectures: $(dpkg --print-architecture)
>> Signed-By: /etc/apt/keyrings/docker.asc
>> EOF
- sudo apt update

*Now as the repository is configured we can install the actual docker software*
- sudo apt install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin\

*For tests we can run the command*
- sudo docker run hello-world
*which pulls the HelloWorld image for testing purposes. The image starts and immediately is terminated. When we run command:*
- sudo docker ps
*we won't see anything, because nothing is working in the background*
- sudo docker ps -a
*now we can see that HelloWorld image was pulled and launched successfully. We can see that it was launched and then terminated.*

### Step 3: I make a container in Docker and pull the Ollama software.
*For first I pulled NGINX server I played with it for a while. I was checking what I can actually do. I tested some docker commands for starting, stoping, deleting and pulling software.*
- sudo docker run -d -p 82:80 --name test nginx #-d for the program to run in the background
- sudo docker ps
- sudo docker stop test
- sudo docker rm test #I did some additional tests on the website in order to understand more

*Then I worked on Ollama:*
- sudo -i # I didn't want to write sudo everytime. I know that if that was a production server doing that would be dangerous but in my case that is completely fine.
- docker run -d -v ollama:/root/.ollama -p 5000:11434 --name model_ai ollama/ollama
*now the docker says that there is no ollama installed and start pulling it from the internet. It takes a while to finish and in my case there were two failures with that process. The rpi was connected to weak internet and could not finish the process. Then I connected to better network and it solved the pulling issue.*

*now we can use:*
- dokcer exec -it model_ai /bin/bash # now we are in the container and have a direct communication with ollama
- docker exec -it model_ai ollama list # now we are not entering the container and only communicating with ollama through the docker
*I think that when you do a lot of commands the first way is more convenient. When I was testing the ollama and options that I got through:*
- ollama -h # I tested all the options I got in the help menu and also tested some options further via:
- ollama run -h
- ollama create -h

### Step 4:
*I chose llama model with 1b parameters because it is small enough that it can run smoothly and leave enough RAM for the Pi OS and Docker
When inside the container and talking to ollama thanks to (docker exec -it model_ai /bin/bash)*
- ollama run llama3.2:1b
*now ollama pulls the model from internet and runs it. It takes a while, but since I connected to better network it finishes without problems.
after a while we can see the interface to talk with the LLM: (>>)*

### Step 5:
*Now we can access the model through the IP address from different device. As I want to simulate the professional environment, I decided to make a server. Therefore I pulled the image of OpenWebUI into docker and launched it.*
- docker run -d -p 3000:8080 -v open-webui:/app/backend/data --name open-webui ghcr.io/open-webui/open-webui:main # This is command from official website (https://docs.openwebui.com/getting-started/quick-start/)
*Then I figured out, this is not that simple. The OpenWebUI has to communicate with Ollama and therefore it requires additional effort to connect those two containers*
*As I searched the internet, read the documentation and talked with ai, I crafted that command:*
- docker run -d --add-host=any_string:host-gateway -p 3000:8080 -v open-webui:/app/backend/data --name open-webui ghcr.io/open-webui/open-webui:main
*any_string is a literally any string and it does not change anything. host-gateway is reference to the internal IP address of the Docker. The OpenWebUI has to know exactly where to connect and via which IP address send messages.*
*the rest of the command stays the same. Now we have an established connection between two containers.*
*OpenWebUI is a UI for LLM's and it is very similar to the interface of Gemini and ChatGPT. It has more features connected with temperture of models and many other parameters which can define the creativity. In fact that is not working correctly becuse the local LLm deployed by us is just simply not changeable.*

### Step 6:
*I install Cursor on different device and add my own local model.
I go to the Models Tab and go to the API Keys section. Then I fill the Override OpenAI Base URL and place here url for Ollama model running on rpi.
In the end of the url I have to put the /v1 because it is a standard for OpenAI
Then I need to fill the OpenAI API Key field because it cannot be empty. I write arbitrary string.
When I did then over some time the Cursor deleted my own url and replaced it with the OpenAI's url. That is propably because when you submit the url or the Cursor tries to access the model then it tries the url and if it not works then replaces it.*





