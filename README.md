<h1>Instructions</h1>
<h2>Icecast2 with docker-run</h2>

```
docker run -d -p 8000:8000 --name icecast2 ianm2/icecast2_arm
```


<p><b>Important</b><br>
Modify icecast.xml from the automatically created volume or mount your file with '-v' variable (Ex. -v /directory/icecast.xml:/etc/icecast2/icecast.xml)</p>

<h2>Icecast2 with ezstream in docker-compose:</h2>
<p><b>Important</b><br>
In this section, you need to have all files what requests the 'volume' section in the docker-compose file</p>

<p>Copy the next text in a <b>docker-compose.yaml</b> file:</p>

```
version: "3.7"
services:
  icecast2:
    image: ianm2/icecast2_arm
    container_name: icecast2
    volumes:
      -  /directory/icecast.xml:/etc/icecast2/icecast.xml
    ports:
      - 8000:8000
  
  ezstream:
    image: ianm2/ezstream_arm
    container_name: ezstream
    depends_on:
      - icecast2
    volumes:
      - /directory/ezstream_mp3.xml:/etc/ezstream/ezstream_mp3.xml
      - /directory_playlist/:/etc/ezstream/music/
      - /directory/playlist.txt:/etc/ezstream/playlist.txt
    restart: unless-stopped
```

<p>Run the next command:</p>

```
docker-compose up -d
```
