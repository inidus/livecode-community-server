docker build --rm -t local/livecode-centos7-httpd .
docker run -dit --name my-apache-app -p 8080:80 local/livecode-centos7-httpd
