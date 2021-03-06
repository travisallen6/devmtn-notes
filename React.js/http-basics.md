# HTTP Basics

## Todd's Focus Questions:
- _What does Asynchronous code mean and why is it important in HTTP?_
    <details>
    <summary> <code> answer </code> </summary>

    Synchronous Programming:
    - program ignores conditions and functional calls and executes code from top to bottom
    - this causes a block on HTTP requests and other long-running tasks

    Asynchronous Programming:
    - allows the engine to run in an event loop
    - when a blocking operation is needed, it begins the processes and then continues to execute code without pausing to await a (potentially long-delayed) response
    - response is ready **->** interruptor is fired **->** flow continues
        - think react lifecycles
    - allows a single program thread to handle many event occurences 

    </details>

- _What is a Promise?_
    <details>
    <summary> <code> answer </code> </summary>

    A value not yet available, as seen in callback functions.
    - instead of stringing a bunch of `if/else` statements along to handle errors, `return new Promise` to await expected data without having to bounce a number of requests first

    Allows you to write asynchronous code in a more synchronous fashion.

    For example...

    ```
      function getCurrentTime(onSuccess, onFail) {
      // GET the current 'global' time from an API using Promise
        return new Promise((resolve, reject) => {
            setTimeout(function() {
            var didSucceed = Math.random() >= 0.5;
            didSucceed ? resolve(new Date()) : reject('Error');
            }, 2000);
        })

      getCurrentTime()
        .then(currentTime => getCurrentTime())
        .then(currentTime => {
            console.log('The current time is: ' + currentTime);
            return true;
        })
        .catch(err => console.log('There was an error:' + err))
    ```

    </details>

- _When does a .then callback function run?_
    <details>
    <summary> <code> answer </code> </summary>

    After the function it trails.
    - For example...
    ```
      getData().then()
    ```

    </details>

- _What is an API and what does it mean to “Make an API call?”?_
    <details>
    <summary> <code> answer </code> </summary>
    
    An API is an **A**pplication **P**rogram **I**nterface and it...
    - serves data to clients
    - allows users to interact with data stored by a org through a website
    - not a remote server, but instead a part of the server that sends and receives requests

    </details>

- _What is Axios?_
    <details>
    <summary> <code> answer </code> </summary>

    

    </details>


## Clients: 
- Handle user interaction
- Present data from server
- Request data from server
- Request data from 3rd party APIs 

## Servers:
- Listen for and process requests
- Send front-end files to client
- Mediate between client and database 

## URLs:
- **U**niform **R**esource **L**ocator: used to uniquely identify a resource over the web. 
- `protocol://hostname:port/path-and-file-name`
    + `protocol` — the application-level protocol used by the client and server (like HTTP, FTP, telnet)
    + `hostname` — the DNS domain name or IP address of the server
    + `port` — the TCP port number that the server is listening for incoming requests from the clients on. If not specified, takes on a default. 
        + in HTTP, that default is TCP port 80
    + `path-and-file-name` — the name and location of the requested resource, under the server document base directory
- For example… `mailto:user@test101.com`  `telnet://www.nowhere123.com/` `ftp://www.ftp.org/docs/test/txt`
- Whenever you enter a URL in the address box of the browser, the browser translates the URL into a request message according to specified protocol

## **H**yper**T**ext **T**ransfer **P**rotocol - otherwise known as HTTP Requests:
- This is communication between a computer and a server, a request is sent to get the HTML and then everything else attached to it.
- HTTP Requests are stateless -- they don't remember anything 
- `From:` client, `to:` server
- There are hundreds of open APIs — different servers with ways for anyone to interact with them — that we can communicate with.
- They have different labels depending on what they’re used for.
    * `GET`: Requests a web resource from the server
    * `HEAD`: Requests the header that a `GET` would have obtained. Often used to check against the local cache copy, as the header contains the last-modified date of the data.
    * `POST`: Used to post data up to the server
    * `PUT`: Asks the server to store the data
    * `DELETE`: Asks the server to delete the data
    * `TRACE`: Asks the server to return a disanostic trace of the actions it takes
    * `OPTIONS`: Asks the server to return the list of request methods it supports 
    * `CONNECT`: Used to tell a proxy to make a connection to another host and simply reply the content, without attempting to parse or cache it. Often used to make SSL connection through the proxy


## HTTP Responses:
- The first line of the response message contains the response status code, generated by the server to indicate an outcome to the request. 

- Status code is output in a 3-digit-number:
    * `1xx` _(Informational)_: Request received, server is continuing the process.
    * `2xx` _(Success)_: The request was successfully received, understood, accepted, and serviced.
    * `3xx` _(Redirection)_: Further action must be taken in order to complete the request.
    * `4xx` _(Client Error)_: The request contains bad syntax or cannot be understood.
    * `5xx` _(Server Error)_: The server failed to fulfill an apparently valid request. 

- Some commonly encountered status codes...
    * `100 Continue`: The server received the request and in the process of giving the response.
    * `200 OK`: The request is fulfilled.
    * `301 Move Permanently`: The resource requested for has been permanently moved to a new location. The URL of the new location is given in the response header called Location. The client should issue a new request to the new location. Application should update all references to this new location.
    * `302 Found & Redirect` (or `Move Temporarily`): Same as `301`, but the new location is temporarily in nature. The client should issue a new request, but applications need not update the references.
    * `304 Not Modified`: In response to the If-Modified-Since conditional GET request, the server notifies that the resource requested has not been modified.
    * `400 Bad Request`: Server could not interpret or understand the request, probably syntax error in the request message.
    * `401 Authentication Required`: The requested resource is protected, and require client’s credential (username/password). The client should re-submit the request with his credential (username/password).
    * `403 Forbidden`: Server refuses to supply the resource, regardless of identity of client.
    * `404 Not Found`: The requested resource cannot be found in the server.
    * `405 Method Not Allowed`: The request method used, e.g., POST, PUT, DELETE, is a valid method. However, the server does not allow that method for the resource requested.
    * `408 Request Timeout`:
    * `414 Request URI too Large`:
    * `500 Internal Server Error`: Server is confused, often caused by an error in the server-side program responding to the request.
    * `501 Method Not Implemented`: The request method used is invalid (could be caused by a typing error, e.g., "GET" misspell as "Get").
    * `502 Bad Gateway`: Proxy or Gateway indicates that it receives a bad response from the upstream server.
    * `503 Service Unavailable`: Server cannot response due to overloading or maintenance. The client can try again later.
    * `504 Gateway Timeout`: Proxy or Gateway indicates that it receives a timeout from an upstream server.