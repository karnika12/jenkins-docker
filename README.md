<h1>Jenkins CI labs</h1>
<h2>Jenkins CI pipeline - build Docker image and Push to DockerHub</h2>
<p align="center">
<img src="https://github.com/Joska99/jenkins-docker/blob/main/diagram.drawio.svg">
</p>

<h2>Requirements:</h2>

1. Jenkins server
- [My Jenkins Container guide](https://github.com/Joska99/joska/tree/main/docker/jenkins)
2. Docker Hub registry
3. Add your Docker Hub credentials to Jenkins
4. Install required plugins for Jenkins

<h2> Steps:</h2>

1. Configure Jenkins

- In Jenkins portal: Navigate to "New Item"
- Give "Name" to item and Chose "Pipeline"
- You can add description to the pipeline
- Then chose "Github project" and add Github repo URL
- Then in "Building Triggers" select "GitHub hook trigger for GITScm polling"
- In Pipeline select "Pipeline script from SCM", SCM is "Git" add Github repo URL, specify branch, "Script Path" is File name "Jenkinsfile"

2. Configure GitHub

- In GitHub repo: Go to "Setting" -> "Webhooks"
- Payload URL: https://<UR_PUBLIC_IP>:8000/github-webhook/

>You need to expose container from localhost to internet </br>
>You can use ngrok to achieve this </br>
>Run this with ngrok installed
```bash
ngrok.exe http 8000
```
>copy link and paste to "Payload URL" </br>
>example: https://2966-93-172-72-111.ngrok.io/github-webhook/ </br>

- Content type: "application/json"
- In "Witch events would trigger?" chose "Just the push event"
- In "Secret" add API token from Jenkins
>in Jenkins portal click on your user name on right top and chose "Configure" </br>
>Scroll till "API Token" and generate new 

- Click on "Add webhook"

3. Finely push some changes and enjoy your pipeline

<h2> Add credential to Jenkins:</h2>

1. In Jenkins portal: Go to "Manage Jenkins" -> "Credentials"
2. click on "global"
3. Chose "Add credentials"
> Docker Hub
1. Chose "Username with Password"
2. Fill credentials fields 
>ID - DockerHub-LG</br>
>password - password</br>
>username - username
3. Add description 

<h2> Add plugins to Jenkins:</h2>

1. In Jenkins portal: Go to "Manage Jenkins" -> "Plugins" -> "Available plugins"
2. Search for "GitHub Integration Plugin" and install
2. Search for "Docker Pipeline" and install
2. Search for "Docker Plugin" and install

</h2> Add Docker to jenkins: </h2>

1. In Jenkins portal: Go to "Manage Jenkins" -> "Tools"
2. Scroll till Docker -> Docker installation
3. Name - Docker
4. Install automatically 
5. Chose from Docker.com





