# My linux cheat sheet

## file access
 - chmod:  I use this command when working on my workspace. 
 
 ```
 chmod -R 755 filename
 ```
- vim command i used when I wanna save a file that does not exist
```
   :w !sudo tee %
```
- scp to a url using a port other than 22 ( which is the  default one )
```bash
 scp -P [port_number] [file_name] [username]@[hostname]:[file destination path]
```
  - note, tje file destination path must contain the name of the file you want to save it as. 
    - ex: if you might wanna upload gwomesye.html then , you'd do :
    - ```bash
       scp -P [port_number] gwomesye.html [username]@[hostname]:/.../gwomesye.html
      ```
