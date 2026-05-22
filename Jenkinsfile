docker stop demo-container || True
docker rm demo-container || True

docker build -t html-application .

docker run -d --name html-container -p 9876:80 html-application
