# livecode-centos7-httpd

LiveCode Community Server running as a CGI handler within an Apache web server environment on Centos 7.

## Docker

Build the image `docker build -t livecode-centos7-httpd:latest .`

Add your LiveCode to the folder `livecode-centos7-httpd/html` (you may need to create the folder `html`)

Run the container `docker run --rm --name livecode -p 8080:80 livecode-centos7-httpd:latest`

Open [http://127.0.0.1:8080](http://127.0.0.1:8080) in your browser

## Authors

* [Rob Dyke](https://gitlab.com/robdyke) for [inidus](https://inidus.com)

## Notes

`docker build --rm -t livecode-centos7-httpd .`

`docker run -dit --name livecode -p 8080:80 livecode-centos7-httpd`
