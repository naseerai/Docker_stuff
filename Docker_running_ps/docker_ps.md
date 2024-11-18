# Docker CLI Command : docker `ps`

The docker ps command is used to list the currently running Docker containers on your system. Here's a breakdown of what it does and some options you can use with it:

### Basic Command
```bash
 docker ps
 ```
 ![alt text](images/2.png)   

### Explanation

*   **docker**: This is the Docker CLI.
    
*   **ps**: This is the command that shows a list of running containers.
    
### Default Output

When you run docker ps, it shows:

*   **CONTAINER ID**: A unique identifier for the container.
    
*   **IMAGE**: The Docker image used to create the container.
    
*   **COMMAND**: The command that was run to start the container.
    
*   **CREATED**: When the container was created.
    
*   **STATUS**: The current status of the container (e.g., "Up 5 minutes").
    
*   **PORTS**: Port mappings between the container and the host.
    
*   **NAMES**: The name of the container. 


### Common Options

* `docker ps -a`  Shows all containers, including stopped ones (by default, docker ps only shows running containers).
    
* `docker ps -q` Only shows container IDs, useful for scripting.
    
* `docker ps --filter "status=exited"` Filters containers based on criteria, like status, name, or label.
    
* `docker ps --format "{{.ID}}: {{.Names}}"`  Allows you to format the output.