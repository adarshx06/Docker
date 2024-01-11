#Understanding Docker 
1. Intiating docker File:
FROM python:3.8-alpine
COPY . /app
WORKDIR /app 
RUN pip install -r requirements.txt
CMD python app.py

2. To build Image:
cmd: docker build -t welcome-app .

3. Check Image:
docker images

4. To run docker image as container:
a) To info should be provided Host Port and Container port
docker run -p 5000(hostport):(containerport)5000 welcome-app(dockerimg)
 PS D:\Docker> docker run -p 5000:5000 welcome-app
 * Serving Flask app 'app'
 * Debug mode: on
WARNING: This is a development server. Do not use it in a production deployment. Use a production WSGI server instead.
 * Running on all addresses (0.0.0.0)
 * Running on http://127.0.0.1:5000  (host)
 * Running on http://172.17.0.2:5000 (container)
Press CTRL+C to quit
 * Restarting with stat
 * Debugger is active!
 * Debugger PIN: 119-848-643

PS D:\Docker> docker ps
CONTAINER ID   IMAGE         COMMAND                  CREATED         STATUS         PORTS                    NAMES
1bd305096212   welcome-app   "/bin/sh -c 'python …"   2 minutes ago   Up 2 minutes   0.0.0.0:5000->5000/tcp   serene_antonelli

Stop one or more running containers
PS D:\Docker> docker stop 1bd305096212
1bd305096212

to remove docker image
PS D:\Docker> docker image rm -f welcome-app
Untagged: welcome-app:latest
Deleted: sha256:37eae4c633c436ba1779554a4deb8de4ed7ca875ed557180992d67a171da1001
5. Push the above(docker image) in dockerHub Repo
Change to name as it need my username to map:

PS D:\Docker> docker build -t adarshx06/welcome-app .
[+] Building 1.5s (10/10) FINISHED                                                                                                        docker:default
 => [internal] load build definition from Dockerfile                                                                                                0.0s
 => => transferring dockerfile: 143B                                                                                                                0.0s 
 => [internal] load .dockerignore                                                                                                                   0.0s 
 => => transferring context: 2B                                                                                                                     0.0s 
 => [internal] load metadata for docker.io/library/python:3.8-alpine                                                                                1.2s 
 => [auth] library/python:pull token for registry-1.docker.io                                                                                       0.0s 
 => [1/4] FROM docker.io/library/python:3.8-alpine@sha256:6d2e9727ae94824ab491fd6aada007df1fd15dd9cb6cb6d3edb73d4abafdc57c                          0.0s
 => [internal] load build context                                                                                                                   0.2s 
 => => transferring context: 131.25kB                                                                                                               0.2s 
 => CACHED [2/4] COPY . /app                                                                                                                        0.0s
 => CACHED [3/4] WORKDIR /app                                                                                                                       0.0s 
 => CACHED [4/4] RUN pip install -r requirements.txt                                                                                                0.0s 
 => exporting to image                                                                                                                              0.0s 
 => => exporting layers                                                                                                                             0.0s 
 => => writing image sha256:37eae4c633c436ba1779554a4deb8de4ed7ca875ed557180992d67a171da1001                                                        0.0s 
 => => naming to docker.io/adarshx06/welcome-app                                                                                                    0.0s 

What's Next?
  View a summary of image vulnerabilities and recommendations → docker scout quickview
PS D:\Docker> docker images
REPOSITORY              TAG       IMAGE ID       CREATED          SIZE
adarshx06/welcome-app   latest    37eae4c633c4   14 minutes ago   698MB

We can also change through tags:
PS D:\Docker> docker tag adarshx06/welcome-app adarshx06/welcome-app-changed
PS D:\Docker> docker images
REPOSITORY                      TAG       IMAGE ID       CREATED          SIZE
adarshx06/welcome-app-changed   latest    37eae4c633c4   16 minutes ago   698MB
adarshx06/welcome-app           latest    37eae4c633c4   16 minutes ago   698MB

Now we will PUSH
Pushing images
You can push a new image to this repository using the CLI:

docker tag local-image:tagname new-repo:tagname
docker push new-repo:tagname
PS D:\Docker> docker push adarshx06/welcome-app:latest
The push refers to repository [docker.io/adarshx06/welcome-app]
5bf6dc95fbc4: Pushed
5f70bf18a086: Pushed
65c54efd6181: Pushing [==================================================>]    637MB/637MB
6fc936d097fb: Mounted from library/python
8f6c603b1682: Mounted from library/python
cd918ed62fad: Mounted from library/python
ec4d864ac810: Mounted from library/python
5af4f8f59b76: Mounted from library/python

Now topull Image from Docker Repo:
PS D:\Docker> docker pull adarshx06/welcome-app:latest