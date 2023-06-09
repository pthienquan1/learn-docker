# Build the app’s container image
1. $ cd getting-started
2. $ touch Dockerfile (create docker file)
3. add following contents to Dockerfile:<br>
    FROM node:18-alpine<br>
    WORKDIR /app<br>
    COPY . .<br>
    RUN yarn install --production <br>
    CMD ["node", "src/index.js"] <br>
    EXPOSE 3000 <br>

4. $ docker build -t getting-started .

# Start an app container
docker run -dp 3000:3000 getting-started <br>
--> open your web browser to http://localhost:3000. You should see your app.

# Remove old container
- Check container: $ docker ps
- Stop container: $ docker stop + id
- Remove container: $ docker rm + id

# Share the application
- Login to Docker Hub: docker login -u YOUR-USER-NAME
- Use docker tag to have the new name for the image: docker tag getting-started YOUR-USER-NAME/getting-started
- Push: docker push YOUR-USER-NAME/getting-started

## Login to https://labs.play-with-docker.com/ 
- add new instance, then: 
docker run -dp 3000:3000 YOUR-USER-NAME/getting-started

# Persist the DB
### Container Volumnes: 
Volumes provide the ability to connect specific filesystem paths of the container back to the host machine.
### Persist the todo data
1. Create a volume by using the docker volume create command: $ docker volume create todo-db
2. Stop and remove the todo app container once again with docker rm -f <id>, as it is still running without using the persistent volume.
3. Start the todo app container, but add the --mount option to specify a volume mount. Give the volume a name, and mount it to /etc/todos in the container, which captures all files created at the path. In your Mac or Linux terminal, or in Windows Command Prompt or PowerShell, run the following command:
    - $ docker run -dp 3000:3000 --mount type=volume,src=todo-db,target=/etc/todos getting-started

