**1. Docker Compose File (docker-compose.yml):**

```yaml
version: '3.8'
services:
  container1:
    image: ubuntu:latest  # Or any other image you need
    volumes:
      - ./shared_data:/shared_data # Share current directory's 'shared_data'
    tty: true
    stdin_open: true
    command: bash # Override default command to open bash

  container2:
    image: ubuntu:latest
    volumes:
      - ./shared_data:/shared_data # Share same volume as container1
    tty: true
    stdin_open: true
    command: bash
  container3:
    image: ubuntu:latest
    volumes:
      - ./shared_data:/shared_data # Share same volume as container1
    tty: true
    stdin_open: true
    command: bash
```

**Explanation:**

* **`version: '3.8'`:** Specifies the Docker Compose file format version.
* **`services:`:** Defines the services (containers) to run.
* **`container1`, `container2`, `container3`:** Names of the services. You can change these to something more descriptive.
* **`image: ubuntu:latest`:** Specifies the Docker image to use for each container. Replace `ubuntu:latest` with the desired image.
* **`volumes:`:** This is the crucial part for sharing files.
    * `./shared_data:/shared_data`: This mounts the `shared_data` directory in your current host directory to the `/shared_data` directory within each container. Any files created or modified in `/shared_data` in one container will be visible to the others.
* **`tty: true` and `stdin_open: true`:** These options are necessary to allocate a pseudo-TTY and keep stdin open, allowing you to interact with the bash shell.
* **`command: bash`:** This overrides the default command of the image and starts a bash shell when the container starts.

**2. Create the Shared Directory:**

* Create a directory named `shared_data` in the same location as your `docker-compose.yml` file:

    ```bash
    mkdir shared_data
    ```

**3. Run Docker Compose:**

* Navigate to the directory containing your `docker-compose.yml` file and run:

    ```bash
    docker-compose up
    ```

    This will start the three containers.

**4. Open Bash in Each Container:**

* To open a bash shell in each container, use the following commands in separate terminal windows:

    ```bash
    docker exec -it container1 bash
    docker exec -it container2 bash
    docker exec -it container3 bash
    ```

**5. Sharing Files:**

* Now, any files you create in the `/shared_data` directory within any of the containers will be accessible from the other containers.

**Example workflow:**

1.  Create a file in container1:

    ```bash
    echo "Hello from container1" > /shared_data/file1.txt
    ```

2.  View the file from container2:

    ```bash
    cat /shared_data/file1.txt
    ```

3.  Modify the file from container3:

    ```bash
    echo "Modified by container3" >> /shared_data/file1.txt
    ```

4.  View the modified file from container1:

    ```bash
    cat /shared_data/file1.txt
    ```

**Important Notes:**

* If you change the content of the docker-compose.yml file, you will need to run `docker-compose down` followed by `docker-compose up` to apply the changes.
* If you need to share other folders, simply add more volumes to the docker-compose.yml file.
* If you want to share a single file, you can also mount it as a volume, like: `./shared_data/my_file.txt:/shared_data/my_file.txt`
* Using docker compose, you can configure other network related settings, to allow the containers to communicate with each other.
