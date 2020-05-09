// build the docker image
docker build -t react-ui .
// run the app
docker run -d --name reactui -p 80:80 react-ui
