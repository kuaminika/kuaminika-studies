# Docker cheatsheet

## Conatiners

### **How to list docker containers**
```bash
docker container ls
```
or 
```bash
docker ps
```

### **How create a container ( ie running an image)**

Usually its the _docker run_ command but there's also the _docker create_ command. 
- One of the differences is that docker run actually runs the container. Docker create just creates it but the container is not running.  
- ```bash
   docker run -p 127.0.0.1:80:8080/tcp ubuntu bash # <-- this will run the ubuntu image and I assume that bash is the first command
   # note. in this case the port 8080 inside the container is being exposed at port 80
  ```