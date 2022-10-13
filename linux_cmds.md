# My linux cheat sheet

## file access
 - chmod:  I use this command when working on my workspace. 
 
 ```
 chmod -R 755 directoryName
 ```
- chown : this command is used to give file-access to a user 
  - ```bash
    chown [username] [folder_name] # note there are more variations. the credits have details
    ``` 
  - _credit:https://linuxize.com/post/linux-chown-command/_
 ## vim
- vim command i used when I wanna save a file that does not exist
```
   :w !sudo tee %
```

## ssh
This is how you sign on to another server using ssh commands
```bash
 ssh user@ip.or.hostname -p 22 # 22 is the port number
```
 Ctrl+d if you wanna end the connection
## scp
- scp to a url using a port other than 22 ( which is the  default one )
```bash
 scp -P [port_number] [file_name] [username]@[hostname]:[file destination path]
```
  - note, the file destination path must contain the name of the file you want to save it as. 
    - ex: if you might wanna upload gwomesye.html then , you'd do :
    - ```bash
       scp -P [port_number] gwomesye.html [username]@[hostname]:/.../gwomesye.html
      ```
 ## copying files
- using the cp command to copy files to the current folder
  ```
  cp -r [wtv_path_you_want] .
  ```
## Moving everything to parent folder
- first you cd to the dir
```
cd to/parent/child
```
- then  you use the mv command
```
mv *  ../
```
## zip 
  ### zipping directories 
  ```bash
  zip -r archivename.zip directory_name
  ```
  ### zipping serveral files
  ```bash
  zip archivename.zip filename1 filename2 filename3
  ```
## Services
  ### to list services
  ```bash 
  systemctl list-units --all --type=service --no-pager
  #there is also
  service --status-all
  ```
source: https://vitux.com/how-to-start-stop-or-restart-services-in-ubuntu/

## variables
- saving a whole path to a variable instead of copying and pasting it
   ```bash
    VARIABLE_NAME="path"
   ```
   note that variable can be used as follows:
    ```bash
   cd $VARIABLE_NAME
   ```


## adding a new user

- do the following command 
```bash
sudo adduser userNameHere
```