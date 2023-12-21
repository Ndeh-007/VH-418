# VH-418 -> Prototype Parallel Algorithm Visualization Tool

## Description
VH-418 is a standalone application that runs a python client and an erlang server. The client animates data gotten from requested algorithms ran by the server.

The server runs two algorithms, reduce and scan. 

See the readme files for the server (`./server/ReadME.md`) and the client (`./client/ReadME.md`) for more details

# Usage Instructions

*__`NOTE`__* The application (dist) was built for a Windows environment. You could compile the source code of the client to a target system of your choice by configuring the app.spec and then running.

Read instruction to the end before starting application.

```
$ pyinstaller app.spec
```

## Prerequisites  
- *__Erlang__* : Required for the server to run. Visit https://www.erlang.org/downloads to get erlang
- *__Rebar3__* : Used for the server's OTP application. See the `rebar.config` in the server for the required modules to installed. Executing the following instruction for the first time in the directory of the server should install all required modules.
```
$ rebar3 shell
```

## Usage
- Clone repository
- Run the client. 
    - This could be done in two ways
        1. Run the `.exe` application in the `.client/dist/VH-418` folder
        2. Execute the python application (After installing the required python modules)
            ```shell
            $ python app.py
            ```
- Compile the server with the following instructions (Optional)
    ```
    $ rebar3 compile
    ```

### Using The Client
To run a simulation, after starting the client _(see `./client/ReadME.md` for more details about the client)_.
1. Configure the server
    - On the menu bar, click `File -> Settings`
    - In the settings dialog, perform the following changes:
        - set the location of `rebar3.cmd` or type in `rebar3`. The former is preferable.
        -  <span style="color:red;">[Required]</span> Set the location of the server. This is the path to `./server`.

    - <span style="color:orange;">[Optional]</span> Change frame rate, how fast you want the animation to go. `1 fps` is the default
    - <span style="color:orange;">[Optional]</span> The other url properties are for which server data should be fetched from. By default, launching a server will run at `http://localhost:8080`. You can change the values to `https://yourserver.com:port_number` or `http://ip_address_of_another_computer:port_number`. The fetching is an HTTP GET Request
2.  Start the server
    - Either do this by `File -> Start Erlang Server`
    - Or by Clicking the button on the bottom left corner of the window.
    - The state of the server is seen on the button on the button left corner
3.  After configuring client, create a program.
    - right click on the programs section, `New...` then enter the name of the program and select the type. Each type calls a different algorithm to be run by the server. The name can be left empty, it will default to its place holder text. 
    - Click `create` to create the chosen program
4. Configure the program
    - the only configuration available is the name number of process. This configuration can be done one the properties panel.
5. After setting the desired process number, Run the program
    - Click `Run` in the created tab.
        - this will send a get request to the server, (e.g. `http://localhost:8080/reduce?nprocs=4`). In this example, we want to run the reduce algorithm with 4 processes. See `./server/ReadME.md` for more details about the client
    - wait for the response or see the error message if any.

6. If the run was successfully, content will be shown on the main canvas. Use the next and previous buttons to skip between frames, or click play. Enter a new frame value to jump to the target frame.

7. Use the properties panel to see information about the processes.


<span style="color:orange;">__[WARNING]__</span> There are a lot of bugs. Thread lightly. The application starts with console which logs data, some of it is not helpful, but it may help see why the application may crash unexpectedly. Certain error may not have been caught which could be fatal 😬

In any case, Enjoy !!!
