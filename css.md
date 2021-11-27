# CSS cheatsheet
## The following is a series of hints  found usefull while doing CSS

- having a body style of margin:0;padding:0 makes all the elements touch the edge of the browser page
- when using fonts. its good to start defining the base font inside of the body. then you can use the **em** unit which basically scales based on the size of the base font
- When styling background in one line .the order is as follows :  color image repeat x-position y-position;
  - ex : 
    ```css
      div{
      background: #cf0004 url(../images/banner_1200.jpg) no-repeat center bottom;}
    ```
- the following are some banner graphic sizes: 
  1200, 825, 625, 425

- structuring a css file
   - it could  be wise to put everything that is segemented together , and everything global on top

- psuedo elements 
  - they allow you  to add html elements 
  - ex: element
   ```css
   /*- the following would add a paragraph tag at the end of every div -*/
    div::after{content:'<p>hihi</p>'}
   /*- the following would add a paragraph tag at the start of every div -*/
    div::before{content:'<p>hihi</p>'}
   ```
     - they can be defined by :: or :
     - when using content. you cannot use html codes , you have to use unicodes instead 
        ```html 
        &copy; <!-- this wont work in the css pseudo elements-->
        <!-- unicodes have to be used instead. they can be found on wikipedia-->
        ```

- to clear floats
   - make sure that the parent element of floating items has an element with the clear:both at the end