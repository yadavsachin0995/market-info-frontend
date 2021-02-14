# market-info-frontend

## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run build
```

### Instructions to run

npm run serve from the root directory exposes the application on port 8080. Alternatively, docker image for this app can be pulled from dockerhub and can be run on the local using below command:

docker pull yadavsachin0995/dockerized-market-info-app (images not uploaded to docker-hub as of now, will update if my system stops timing out for no valid reason)
docker run -it -p 8080:8080 --rm --name dockerized-market-info-app dockerized-market-info-app


Hint - To run the container in detached mode, use -d.


### What's pending?

1. Test Cases - Unit Test cases have not been written for any component or util.
2. Generic Error Dialog component can be added in case the request to the backend fails.
3. Extract globally configurable variables from components and put the in a conf file.


### Is there a demo link available?

No. Since the locally built container images were not uploaded to remote, was unable to pull those images on ECS. Planned to have one instance each for frontend, backend and redis server - exposing the frontend app through a public IP. If my VPN stops behaving irrationally, might upload the docker images and complete the hosting. 

If docker is locally installed and a good internet bandwidth is available, images for frontend and backend (refer - https://github.com/yadavsachin0995/marketinfobackend) can be built using -
a. docker build -t dockerized-market-info-backend . (from the root folder of the backend project - https://github.com/yadavsachin0995/marketinfobackend)
b. docker build -t dockerized-market-info-app . (from the root folder of this project)


Some snapshots of the running app are attached below -

Landing page with no filter on Equity Name

![alt text](/snapshots/screen1.PNG)

Filter text entered inside textbox provides real-time filtering of results

![alt text](/snapshots/screen2.PNG)

If a user clicks download button on filtered results screen, only present records are downloaded in csv

![alt text](/snapshots/screen3.PNG)

Information of containers used to run the app along with port numbers

![alt text](/snapshots/screen4.PNG)