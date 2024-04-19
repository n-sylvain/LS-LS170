# [Working with HTTP](https://launchschool.com/lessons/0e67d1ce/assignments)

## [What to Focus on](https://launchschool.com/lessons/0e67d1ce/assignments/b9609f49)

- HTTP: This chapter uses Bash and other network utilities, but this is all to better understand HTTP and how it enables network connections between client and server.
-  HTTP and the structure of messages: HTTP can be seen as a set of rules for structuring messages exchanged between applications. Understand these rules and how to apply them.
-  HTTP is a request-response protocol: One of the fundamental aspects of HTTP is its request-response behaviour. Try to form a solid mental model around this.

## [Using Telnet to explore HTTP](https://launchschool.com/lessons/0e67d1ce/assignments/20d4226d)

- Telnet and netcat don't seem to be present on my AWS cloud9, so i'm coding along on VSCode with the inbuilt Netcat. 

<img width="1176" alt="Screenshot 2023-04-27 at 08 49 39" src="https://user-images.githubusercontent.com/78854926/234795741-347a194e-1518-4c48-baba-8bc4c1c3ee4f.png">

## [Speaking the same language](https://launchschool.com/lessons/0e67d1ce/assignments/ea90d10b)

### In AWS Cloud9

- I installed Netcat with `yum install nc`
- I then ran `nc --recv-only -v launchschool.com 80`

<img width="497" alt="Screenshot 2023-04-27 at 09 50 35" src="https://user-images.githubusercontent.com/78854926/234810875-43460fad-60f7-4d4f-a1f2-804db4c6f334.png">

- But after that I can't seem to get it to repsond, so I switch to using Netcat in VSCode:

### In VSCode

- Launch School's homepage does not respond to `GET /` because I haven't specified the version of HTTP to use.

<img width="858" alt="Screenshot 2023-04-27 at 09 37 14" src="https://user-images.githubusercontent.com/78854926/234807364-f5a81b32-e295-41b1-b47a-15c256d7a4cd.png">

- Asking for the Launch School Homepage in an outdated HMTL 0.9 returns a 400 error code:

  <img width="704" alt="Screenshot 2023-04-27 at 09 27 02" src="https://user-images.githubusercontent.com/78854926/234804706-d554d76c-892e-4562-a044-4bea4e47850b.png">

- So I try asking for the homepage in HTML 1.1, which also returns a 400 error code (as expected in LS material):

Seeking LS homepage:

<img width="691" alt="Screenshot 2023-04-27 at 09 38 55" src="https://user-images.githubusercontent.com/78854926/234807890-c3cae6a3-3a44-40ed-a3af-b6525624e406.png">

Although it does work with the Google homepage:

<img width="1152" alt="Screenshot 2023-04-27 at 09 31 33" src="https://user-images.githubusercontent.com/78854926/234805826-f4d2c1ca-d87a-4582-b1e6-0c5e47416ee6.png">

- Any response code that is in the 400s means there's a problem on the client-side. The 400 code specifically means there's a syntax error in the structure of the request. In other words the server is saying, "I don't understand what you just asked me".

- LS material says that specifying the HTTP version with `GET / HTTP/0.9` will get a 505 error:

  <img width="903" alt="Screenshot 2023-04-27 at 09 17 26" src="https://user-images.githubusercontent.com/78854926/234802347-6d033a93-39dc-4aa9-bcfa-1e891dd8d9ba.png">

- The response code in the 500s which means an error on the server side. This is because  the request was valid, but the server cannot communicate in that version of HTTP.

, but I am still getting the same 400 error (or it works fine - 200 OK - with google homepage):

  <img width="662" alt="Screenshot 2023-04-27 at 09 58 52" src="https://user-images.githubusercontent.com/78854926/234813101-27f06734-a06d-4fae-9681-6267300c0397.png">

- Apparently in HTTP 1.1 the client must specify the host name in the header, so:

<img width="842" alt="Screenshot 2023-04-27 at 10 16 55" src="https://user-images.githubusercontent.com/78854926/234817732-18720de0-925d-4b7b-880b-d2a1ff41d279.png">

- Error messages in the 300s relate to redirects. The client needs to take some additional action to complete the request. Here it's because the server is set up to redirect all http to https. The response includes a `Location` header which tells the client where it can now find the resource it requested. If the client were a browser it would automatically follow this redirect. Another interesting note is the TCP dfoesn't close the connection, but sets it to `keep-alive`. This is because it is expecting a follow-up request from the client.

## [Implementing your own HTTP server: Project overview](https://launchschool.com/lessons/0e67d1ce/assignments/be0e4401)

- HTTP is a set of rules for structuring a message between two points. It's up to the client and server to implement those rules, which result in how the message is interpreted.
- We will now implement our own basic server. It will only:
  - respond to GET requests
  - serve static text files.
- We will use netcat with some bash scripting. 

### Bash

- A command language for interacting with a system environment.

### Netcat

- A network utility which provides a variety of features. One feature is providing TCP connections between two network end-points.

### Installing Netcat

- already done? I'm doing a brew install anyway using `brew install netcat`

## [Bash Basics](https://launchschool.com/lessons/0e67d1ce/assignments/a0f37a79)

### Input and Output

<img width="320" alt="Screenshot 2023-04-27 at 10 43 52" src="https://user-images.githubusercontent.com/78854926/234825054-0f4930b1-65ff-4769-ba23-a24c2de287d3.png">

### Variables

- Like any other scripting language, Bash stores temporary data in variables, like this: `name='Sandy'` (no spaces) 
- Case sensitive:
  - `Cat='Maggy'` has to be called with `$Cat`
- Variable references must be prepended with `$`
  - `$Cat`
- We can pass bash variables as arguments to commands:
  - `echo $Cat`
- If you pass multiple varible names to `read` and then assign a multi-word string, it will divide the string at the spaces:

```
$ read first second third
Do you like apples?
$ echo $first # Do
$ echo $second # you
$ echo $third # like apples?
```

### Bash Files

- These bash commands are executable files.
- We can also create our own executables.
- By convention bash files are appended with `.sh`

Instructions:
- Create a directory called `bash_basics`
- In that directory create a file called `hello_world.sh`
- in that file write `echo "Hello World!"`
- in the command line write `bash hello_world.sh` and it will run the command in the `hello_world.sh` file.

Alternatively: 
- the `hello_world.sh` file can include `#!/bin/bash` at the beginning of the file. The `#!` character sequence is known as the 'shebang' and is followed by the path to the file or program that should be used to run the subsequent code in the bash file.
- Trying to run the file now: `./hello_world.sh` returns `Permission denied. So we need to grant the permission.
- `$ chmod +x hello_world.sh`
- Then it works.

### Conditional statements

- Bash provides a way to work through conditional logic with `if` statements.
- They are opened with `if` and closed with `fi`:

```
if [[ <condition> ]]
then
  <commands>
fi
```
- The condition is written between two square brackets, unless it is a boolean:

```
if true
then
  echo 'True'
fi
```

- The double square-brackets are in fact shorthand for running the `test` command. The test command provides operators for evaluating things. See below:

|Operator|Description|
| :--- | :---: |
|**Strings**|
|-n string|Length of string is greater than 0|
|-z string|Length of string is 0 (string is an empty string)|
|string_1 = string_2|	string_1 is equal to string_2|
|string_1 != string_2|	string_1 is not equal to string_2|
|**Integers**|
|integer_1 -eq integer_2|	integer_1 is equal to integer_2|
|integer_1 -ne integer_2|	integer_1 is not equal to integer_2|
|integer_1 -gt integer_2|	integer_1 is greater than integer_2|
|integer_1 -ge integer_2|	integer_1 is greater than or equal to integer_2|
|integer_1 -lt integer_2|	integer_1 is less than integer_2|
|integer_1 -le integer_2|	integer_1 is less than or equal to integer_2|
|**Files**|
|-e path/to/file|	file exists|
|-f path/to/file|	file exists and is a regular file (not a directory)|
|-d path/to/file|	file exists and is a directory|

- Example 1: String longer than 0?

```
string='Hello'

if [[ -n $string ]]
then
  echo $string
fi
```

- Example 2: two integers are equal?

```
integer_1=10
integer_2=10

if [[ $integer_1 -eq $integer_2 ]]
then
  echo $integer_1 and $integer_2 are the same!
fi
```

- Example 3: Tests if file exists:

```
if [[ -e ./hello_world.sh ]]
then
  echo 'File exists'
fi
```

### Testing multiple conditions:

- We can:
  - Nest `if` statements
  - `else` and `elif`
  - Use boolean operators like `&&` and `||`

Example 1: Nested `if` statement:

```
integer=4

if [[ $integer -lt 10 ]]
then
  echo $integer is less than 10

  if [[ $integer -lt 5 ]]
  then
    echo $integer is also less than 5
  fi
fi
```

Example 2: two conditional branches with `if` and `else`

```
integer=15

if [[ $integer -lt 10 ]]
then
  echo $integer is less than 10
else
  echo $integer is not less than 10
fi
```

Example 3:

```
integer=15

if [[ $integer -lt 10 ]]
then
  echo $integer is less than 10
elif [[ $integer -gt 20 ]]
then
  echo $integer is greater than 20
else
  echo $integer is between 10 and 20
fi
```

Example 4:

```
integer=15

if [[ $integer -gt 10 ]] && [[ $integer -lt 20 ]]
then
  echo $integer is between 10 and 20
fi
```

Example 5:

```
integer=12

if [[ $integer -lt 5 ]] || [[ $integer -gt 10 ]]
then
  echo $integer is less than 5 or greater than 10.
fi
```

Example 6:

```
integer=8

if [[ ! ($integer -lt 5 || $integer -gt 10) ]]
then
  echo $integer is between 5 and 10.
fi
```

- In bash the `!` can be used in multiple different ways.

### Loops

- Bash has `for`, `until` and `while` loops. The second 2 are as you know them, but the `for` loop iterates through a list.
- for loops:

```bash
numbers='1 2 3 4 5 6 7 8 9 10'

for number in $numbers
do
  echo $number
done
```

- until loops

```bash
counter=0
max=10

until [[ $counter -gt $max ]]
do
  echo $counter
  ((counter++))
done
```

- while loops:

```
counter=0
max=10

while [[ $counter -le $max ]]
do
  echo $counter
  ((counter++))
done
```

### Funtions

- You can save multiple commands in a chunk of code called a 'function'
- Functions can take 0, 1 or more arguments.

Example 1:
```
greeting () {
  echo Hello $1
}

greeting 'Peter' #=> 'Hello Peter'
```
- The variable is scoped to the function, which means we can access this variable within the function body but not outside it.
- Subsequent arguments would have 2, 3, 4 etc. assigned to them:

```
greeting () {
  echo "Hello $1"
  echo "Hello $2"
}

greeting 'Peter' 'Paul' # => 'Hello Peter'
                        # => 'Hello Paul'
```
- Variables can be interpolated in double quoted strings.

## [Working with Netcat](https://launchschool.com/lessons/0e67d1ce/assignments/7989eb3f)

- Netcat is a Network utility used for reading and writing data accross network connections using TDP or UDP. (It's like Telnet from before).

```
$ netcat -v google.com 80
```
- The verbose flag means netcat will print messages when certain things happen, like a connection opening and closing.

- This is the command for installing netcat:

```
sudo yum -y install netcat
```
### Setting up a server

- As well as connecting to a domain and port, netcat also allows you to listen to that doman/port for incoming connections:
- VSCode:
```
$ netcat -lv 2345 #              => Warning: Inverse name lookup failed for `0.0.9.41'
# LS said the message should be: => Listening on [0.0.0.0] (family 0, port 2345)
```
- Alternative command:
<img width="614" alt="Screenshot 2023-04-28 at 08 30 02" src="https://user-images.githubusercontent.com/78854926/235083434-0af81c2a-caba-45a8-955a-5e68a845f12e.png">
- AWS Cloud9:
<img width="431" alt="Screenshot 2023-04-27 at 16 30 57" src="https://user-images.githubusercontent.com/78854926/234911862-1ed46d66-85f6-4008-8e14-da5680ae7f90.png">

### Setting up a client:

- Alternative VSCode command: `netcat -v localhost 2345`: 
<img width="659" alt="Screenshot 2023-04-28 at 08 20 18" src="https://user-images.githubusercontent.com/78854926/235081295-cdb3a12c-adcf-4ac3-baf0-218f9d25cb01.png">

This will be our client instance.
You should now have two terminal windows; one acting as a client, the other as a server. Typing text into either one will appear in the other as well. Congratulations, you have made a TCP connection.
- terminate the Netcat session with `command + C`

## [Implementing our own HTTP server: Basic Program Structure](https://launchschool.com/lessons/0e67d1ce/assignments/2e3c6bc3)

 - In the previous exercise we sent arbitrary messages. HTTP rquires a certain structure and now we will work on that.
 - Our server should:
   - Receive messages from the client
   - Process HTTP messages
   - Issue a response created according to the logic within the server
 - The next few lessons are for building that logic.

Step 1:

Create a file called `http_server.sh` inside a directory called `simple_http_server`, and paste this code into it:

```bash
#!/bin/bash

function server () {
 #this is where we will add the processing logic for our HTTP server program.
}

coproc SERVER_PROCESS { server; }

netcat -lv 2345 <&${SERVER_PROCESS[0]} >&${SERVER_PROCESS[1]} # => netcat listen verbosely on port 2345
# the second part of the line redirects STDOUT and STDIN, taking the input from the netcat process and redirecting it to the SERVER_PROCESS
```
- `coproc` is a co-process, which runs our `server` function asynchronously with our `netcat` command. In this code we name it `SERVER_PROCESS` and tell it to run the `server` command.
- `echo "${BASH_VERSION}"` reveals that my bash is `3.2.57(1)-release` and since the `coproc` command was only introduced in Bash v4 I will need to update.
  - `brew install bash`
  - `exec bash`
  - `bash --version` => `version 5.2.15(1)`
- The code in this file means:
  - Any input received by `netcat` can be accessed within the server function with the `read` command.
  - Any output produced by `echo` within the server function will be output by `netcat`.

## [Implementing our own HTTP server: Sending a simple response](https://launchschool.com/lessons/0e67d1ce/assignments/1787cbb1)

Step 2: Writing some logic for the `server` function

Aim: For our server funtion to be able to receive some input via `netcat` and then use that data as part of a response.

- Create a loop within server
- Inside the loop 
  - save input to a variable called 'message'.
  - Output 'you said'+ message

I did:

- `netcat -lvp 2345` in client terminal 
- `bash http_server.sh` in server terminal

It's not working on VSCode:

<img width="649" alt="Screenshot 2023-04-28 at 10 03 24" src="https://user-images.githubusercontent.com/78854926/235104852-91a97cca-bda6-476a-9147-2199d7ec36ad.png">

I'm trying AWS Cloud9 again:

- Sometimes it works. I have to change ports though. 
- I get a lot of:

```
hello there: netcat -lvp 2345
Error: Couldn't setup listening socket (err=-3)
```
- My attempt at the exercise on this page : Sending a Simple Response
```
#!/bin/bash

function server () {
  message=$1
  counter=0
  max=1

  while [[ $counter -le $max ]]
  do
    echo "you said" + message
    ((counter++))
  done
}

coproc SERVER_PROCESS { server; }

netcat -v 2345 <&${SERVER_PROCESS[0]} >&${SERVER_PROCESS[1]}
```
LS code:
```
#!/bin/bash

function server () {
  while true
  do
    read message
    echo "You said: $message"
  done
}

coproc SERVER_PROCESS { server; }

netcat -lv 2345 <&${SERVER_PROCESS[0]} >&${SERVER_PROCESS[1]}
```

- [This discussion thread](https://launchschool.com/posts/abc85a9a) explains why I might be getting weird responses to my things.

- I eventually got this to work on AWS like so:

Client:

<img width="1108" alt="Screenshot 2023-04-29 at 08 48 13" src="https://user-images.githubusercontent.com/78854926/235291427-9b3ea0ee-b5ce-4781-98f4-900ab83ff879.png">

Server:
<img width="1099" alt="Screenshot 2023-04-29 at 08 49 06" src="https://user-images.githubusercontent.com/78854926/235291463-9fdbcaad-71cd-4282-8d1d-d5c2812fe793.png">

Bash file:

<img width="757" alt="Screenshot 2023-04-29 at 08 49 26" src="https://user-images.githubusercontent.com/78854926/235291477-55bb3308-8946-46f5-bc4f-08f6310975fa.png">


## [Implementing our own HTTP server: Processing the request](https://launchschool.com/lessons/0e67d1ce/assignments/13c19d80)

- In the previous assignment we were just sending text, now we will add some structure to the messages.
- We will break any messages received into:
  - Request method
  - path
  - HTTP version
- The method will be GET.

My attempt:

```bash
function server () {
  while true
  do
    read method, path, version
    if method == GET
      echo HTTP/1.1 200 OK
    else
     echo HTTP/1.1 400 Bad Request
    fi
  done
}
```

LS solution:

```bash
#!/bin/bash

function server () {
  while true
  do
    read method path version
    if [[ $method = 'GET' ]]
    then
      echo 'HTTP/1.1 200 OK'
    else
      echo 'HTTP/1.1 400 Bad Request'
    fi
  done
}

coproc SERVER_PROCESS { server; }

netcat -lv 2345 <&${SERVER_PROCESS[0]} >&${SERVER_PROCESS[1]}
```

<img width="634" alt="Screenshot 2023-04-29 at 09 03 04" src="https://user-images.githubusercontent.com/78854926/235291935-424d5bf8-f877-4ddb-a37d-da0825b0e23a.png">

## [Implementing our own HTTP server: Serving HTML](https://launchschool.com/lessons/0e67d1ce/assignments/3d0e0a8b)

- At this point the `code` command is not working on AWS, so I'm manipulating files with `cat >` to write and `cat` to read.

### Updating our program logic

-  I looked at the solution pretty early on here

## [Implementing our own HTTP server: Working with the browser](https://launchschool.com/lessons/0e67d1ce/assignments/c884da8a)

- My brain is dead and it's only 10am. Am I not sleeping properly? Am I not relaxing properly? 
- [After a nap...]
- Recap:
  -  Up till now our client has been a terminal window running Netcat
  -  It sends one line requests.
  -  The client outputs the response from the server without tampering at all.
-  If our client was a browser, we would have to adapt our code for:
   -  Most browsers automatically include multiple headers, over multiple lines.
     -  The initial request header.
     -  Then other headers.
   -  Browsers don't just output the response without tampering, they process it. This is how HTML becomes a displayable web-page. So our response needs more information.
   -  A browser might terminate the connection after receiving a response. We want to keep our netcat process open.
 
### Parsing the response

- The current logic reads one line at a time, ie `GET /lion.html HTTP/1.1`
- But a browser response would be multiple lines:
```
GET /lion.html HTTP/1.1
Host: localhost:2345
User-Agent: Mozilla/5.0 (X11; Ubuntu; Linux x86_64; rv:67.0) Gecko/20100101 Firefox/67.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: en-GB,en;q=0.5
Accept-Encoding: gzip, deflate
Connection: keep-alive
Upgrade-Insecure-Requests: 1
Pragma: no-cache
Cache-Control: no-cache
```
- Like this, our server would read each line as a seperate request and return a 400 response code.
- So we need to read everything, and then process it. The end of the message can be identified by the empty line after the final header.
- Here is LS's code for doing this:

```
#!/bin/bash

function server () {
  while true
  do
    message_arr=() #  This is how you initialize an array in bash.
    check=true
    while $check # will cease when $check is false
    do
      read line
      message_arr+=($line) # Apparently this adds each element of $line to the array seperately, so that it can be index accessed. So 0 is the method, 1 is the path etc.
      if [[ "${#line}" -eq 1 ]] # this is called a 'parameter expansion' and is returning the length of the line. If it is 1 then it reassigns check to false, because that is the last line.
      then
        check=false
      fi
    done
    method=${message_arr[0]} # we assign the element at index 0 to `method`
    path=${message_arr[1]} # we assign the element at index 1 to `path`
    if [[ $method = 'GET' ]]
    then
      if [[ -f "./www/$path" ]]
      then
        echo -ne 'HTTP/1.1 200 OK\r\n\r\n'; cat "./www/$path"
      else
        echo -ne 'HTTP/1.1 404 Not Found\r\n\r\n'
      fi
    else
      echo -ne 'HTTP/1.1 400 Bad Request\r\n\r\n'
    fi
  done
}

coproc SERVER_PROCESS { server; }

netcat -lv 2345 <&${SERVER_PROCESS[0]} >&${SERVER_PROCESS[1]}
```

### Improving the response

- To help our browser process this response we're going to add some headers.

#### Content length

- Key question: where does the message end?
  - The first empty line after the headers for:
    - 1xx responses
    - 204
    - 304
    - Any response to a HEAD request.
- Other types of responses are assumed to have a body even if it's empty.
- For messages with a body, the size of the body can be used to determine the end of the message.
- How to calculate the size of the message body:
  - Send a `transfer encoding` header as part of the response. (Beyond the scope of this course).
  - Send a `content length` header, which says the body length in bytes. We'll do this (but set it to 0 for the 400 and 404 responses)

#### Content type

- The value of this header indicates the media type of the resource.
- Browsers can sometimes ignore this header and determine the header in another way. 
- It's good practice to include it.
- We will include a content-type header for our `200` response, with a value of `text/html; charset=utf-8`.

#### Implementing the Changes

- Add a content-type header
- Add a content-length header.

LS code:

```
#!/bin/bash

function server () {
  while true
  do
    my_arr=()
    check=true
    while $check
    do
      read line
      my_arr+=($line)
      if [[ "${#line}" -eq 1 ]]
      then
        check=false
      fi
    done
    method=${my_arr[0]}
    path=${my_arr[1]}
    if [[ $method = 'GET' ]]
    then
      if [[ -f "./www/$path" ]]
      then
        echo -ne "HTTP/1.1 200 OK\r\nContent-Type: text/html; charset=utf-8\r\nContent-Length: $(wc -c <'./www/'$path)\r\n\r\n"; cat "./www/$path"
      else
        echo -ne 'HTTP/1.1 404 Not Found\r\nContent-Length: 0\r\n\r\n'
      fi
    else
      echo -ne 'HTTP/1.1 400 Bad Request\r\nContent-Length: 0\r\n\r\n'
    fi
  done
}

coproc SERVER_PROCESS { server; }

netcat -lkv 2345 <&${SERVER_PROCESS[0]} >&${SERVER_PROCESS[1]}
```

### Testing the code:

- it's not working:

```
dial tcp: lookup www.localhost.com on 127.0.0.1:53: server misbehaving
```
- Also a signal saying "not secure".
- Perhaps this is caused by my DNS blocker...
- I'm going to ask Olly about this, there are many things in this lesson that are not working for me at all.

## [Implementing our own HTTP server: adding Hyperlinks](https://launchschool.com/lessons/0e67d1ce/assignments/1e7bc560)

- Hypertext is text containing references (AKA hyperlinks).

### HTML anchors

- the `<a>` element when used with a reference creates a hyperlink. Like this:
```
<a href="/path/to/target">Click here!</a>
```
- In the above example `path/to/target` could be a complete URL or a file on that server or a file elsewhere.

### Browsers and Hyperlinks

- When you click on a hyperlink the browser automatically sends a GET request for the location specified in the `href` attribute. If no scheme and path is provided the browser will use that of the current page.

### Updating our HTML file

- Add hyperlinks to the html files
- Jesus Christ this is depressing.

LS solution:
```
<ul>
  <li><a href="/leopard.html">Leopard</a></li>
  <li><a href="/tiger.html">Tiger</a></li>
</ul>
```

## [Summary](https://launchschool.com/lessons/0e67d1ce/assignments/dcae7f89)

- HTTP is a text-based protocol for sending Requests and Responses between client and server.
- In order for each side to understand the message it has to be structured in a certain way.
- With HTTP/1.1 the end of the message is indicated by an empty line.
- The `content-length` header tells us the size of the body. So the reader knows where the message should end.

- No quiz. If there was one, after the first go through I would certainly score very low.

## Overview:

|  | Once | Twice(just re-reading my own notes) | Thrice | Comprehension | Retention
| :--- | :---: | :---: | :---: | :--- | :---
|1. What to Focus on|26th April|13th Sept '23||10%|0%|
|2. Using Telnet to explore HTTP|27th April|13th Sept '23||10%|0%|
|3. Speaking the same language|27th April|13th Sept '23||10%|0%|
|4. Implementing your own HTTP server: Project overview|27th April|13th Sept '23||10%|0%|
|5. Bash Basics|27th April|13th Sept '23||10%|0%|
|6. Working with Netcat|28th April|13th Sept '23||10%|0%|
|7. Implementing our own HTTP server: Basic Program Structure|28th April|13th Sept '23||10%|0%|
|8. Implementing our own HTTP server: Sending a simple response|28th April|13th Sept '23||10%|0%|
|9. Implementing our own HTTP server: Processing the request|29th April|13th Sept '23||10%|0%|
|10. Implementing our own HTTP server: Serving HTML|29th April|13th Sept '23||10%|0%|
|11. Implementing our own HTTP server: Working with the browser|29th April|13th Sept '23||10%|0%|
|12. Implementing our own HTTP server: adding Hyperlinks|5th May|13th Sept '23||10%|0%|
|13. Summary|7th May|13th Sept '23||10%|0%|
| + Read through Discussions |
