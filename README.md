## <a href="https://gotechnies.com/wordpress-deploy-docker-compose">wordpress deploy via docker-compose</a>

https://www.youtube.com/embed/PCYLM_447Qo?ecver=2
<h1>What is docker ?</h1>
<blockquote><a href="https://wordpress.org/about/">WordPress </a>is software designed for everyone, emphasizing accessibility, performance, security, and ease of use. We believe great software should work with minimum set up, so you can focus on sharing your story, product, or services freely. The basic WordPress software is simple and predictable so you can easily get started. It also offers powerful features for growth and success.</blockquote>
<h1>What is docker ? why we are using docker-compose ?</h1>
<a href="https://docs.docker.com/install/linux/docker-ce/ubuntu/">To install docker visit on docker site</a>
<blockquote><a href="https://www.docker.com/what-docker">Docker </a>is the company driving the container movement and the only container platform provider to address every application across the hybrid cloud. Today’s businesses are under pressure to digitally transform but are constrained by existing applications and infrastructure while rationalizing an increasingly diverse portfolio of clouds, datacenters and application architectures. Docker enables true independence between applications and infrastructure and developers and IT ops to unlock their potential and creates a model for better collaboration and innovation.</blockquote>
<h1>Docker-compose</h1>
<blockquote>Compose is a tool for defining and running multi-container Docker applications.</blockquote>
To install Docker-compose use the below steps
<pre>$ sudo curl -L https://github.com/docker/compose/releases/download/1.21.2/docker-compose-$(uname -s)-$(uname -m) -o /usr/local/bin/docker-compose</pre>
<pre>$ sudo chmod +x /usr/local/bin/docker-compose</pre>
<h1><strong>Now create a file with name of docker-compose.yml, Copy the below yaml code in docker-compose.yml.</strong>
<a href="https://github.com/arvindr226/docker-wordpress">https://github.com/arvindr226/docker-wordpress</a></h1>
<pre>version: '3.3'

services:
   db:
     image: gotechnies/mysql:5.7
     volumes:
       - /root/test/db:/var/lib/mysql
     restart: always
     environment:
       MYSQL_ROOT_PASSWORD: somewordpress
       MYSQL_DATABASE: wordpress
       MYSQL_USER: wordpress
       MYSQL_PASSWORD: wordpress

   wordpress:
     depends_on:
       - db
     image: gotechnies/wordpress:latest
     ports:
       - "80:80"
     volumes:
       - /root/test/webroot:/var/www/html
     restart: always
     environment:
       WORDPRESS_DB_HOST: db:3306
       WORDPRESS_DB_USER: wordpress
       WORDPRESS_DB_PASSWORD: wordpress
</pre>
<h1><strong>Now run the below commands to docker-compose deploy.</strong></h1>
<pre>docker-compose up -d
</pre>
<h1>Output-:</h1>
<pre>root@node:~/test# docker-compose up -d
Creating network "test_default" with the default driver
Pulling db (gotechnies/mysql:5.7)...
5.7: Pulling from gotechnies/mysql
f2aa67a397c4: Pull complete
1accf44cb7e0: Pull complete
2d830ea9fa68: Pull complete
740584693b89: Pull complete
4d620357ec48: Pull complete
ac3b7158d73d: Pull complete
a48d784ee503: Pull complete
bf1194add2f3: Pull complete
0e5c74178a02: Pull complete
e9201d309436: Pull complete
bf1ac4524e8e: Pull complete
Digest: sha256:81679f23e0ece3e50a7300050191272e5afbf5b66be9b60d2ee0e8b575b152e2
Status: Downloaded newer image for gotechnies/mysql:5.7
Pulling wordpress (gotechnies/wordpress:latest)...
latest: Pulling from gotechnies/wordpress
f2aa67a397c4: Already exists
c533bdb78a46: Pull complete
65a7293804ac: Pull complete
35a9c1f94aea: Pull complete
651774c607cc: Pull complete
7c01fbe5ed3d: Pull complete
9ff29ed84bfc: Pull complete
647feb0f6355: Pull complete
0b9d1c540863: Pull complete
3416ab5471ed: Pull complete
246c5fc29b1a: Pull complete
98923ca5a50a: Pull complete
8931bc5b7082: Pull complete
fb2e6680ec40: Pull complete
36c71eb6672c: Pull complete
aee6d1701877: Pull complete
b48dafdceab4: Pull complete
b8b77748246f: Pull complete
ae3947bf258f: Pull complete
76bf79d20589: Pull complete
Digest: sha256:00e9baa5e41e511bf0aca5544143085901b389096f8728bcb0d825cd2ae82531
Status: Downloaded newer image for gotechnies/wordpress:latest
Creating test_db_1 ... done
Creating test_wordpress_1 ... done
</pre>
