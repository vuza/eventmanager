# Eventmanager
... is a little Redux/React and Node.js Application to manage events.

I will use it to manage events, which get shown on asiamed.at

There is a redux/react backend-gui for managing events, located in ```/frontent```

## Authentication
HTTP Bearer is used for authentication. There is implemented a very poor user management, configurable at ```/config/default.json```. Get a valid bearer with ```POST /auth``` route.

## Development

### Node.js Backend
- Hard dependencies: Redis without authentication on default port, on localhost, on socker 'eventService'
- Install app: ```npm install```
- Use linting: ```npm run lint```

### Redux/React Frontend
See package.json in ```/frontent``` for build commands.

## Deployment

### Remote (Ship Docker to server via ansible)
- Install ansible dependencies: ```ansible-galaxy install -r deployment/requirements.yml --roles-path deployment/roles```
- Install on remote machine, replace alagoda.at in this command and in host file: ```ansible-playbook deployment/playbook.yml --extra-vars "target=alagoda.at" --ask-sudo```

### Local
- Build docker container: ```docker build -t vuza/eventservice .```
- Start redis docker container: ```docker run --name eventService-redis -d redis```
- Start eventService docker container, link it to eventService-redis and expose it to any port, e.g. 8080: ```docker run --link eventService-redis:redis -p 8080:8080 -d vuza/eventservice```
