That's correct. When you run `docker-compose up` in your terminal, it starts the containers and attaches the terminal to their output. This means that:

* **The terminal is actively displaying logs:** You'll see the output from the containers (logs, errors, etc.) in that terminal window.
* **Closing the terminal stops the containers:** If you close the terminal window where you ran `docker-compose up`, Docker Compose will stop the containers.

**How to Run Docker Compose in the Background (Detached Mode):**

If you want to run the containers in the background and free up your terminal, you can use the `-d` or `--detach` flag:

```bash
docker-compose up -d
```

**What happens in detached mode:**

* The containers will start, but the terminal will not be attached to their output.
* You'll get back your terminal prompt, and you can continue using it for other tasks.
* The containers will continue running in the background.

**How to View Logs:**

If you need to see the logs of your running containers when they are in detached mode, you can use the following command:

```bash
docker-compose logs
```

Or, to see the logs of a specific container:

```bash
docker-compose logs <container_name>
```

Replace `<container_name>` with the name of the container (e.g., `picard`, `samtools`).

**How to Stop the Containers:**

When you're finished with the containers, you can stop them using:

```bash
docker-compose down
```

This will stop and remove the containers and any associated resources.

**In summary:**

* `docker-compose up`: Runs the containers in attached mode (foreground).
* `docker-compose up -d`: Runs the containers in detached mode (background).
* `docker-compose logs`: View the container logs.
* `docker-compose down`: Stop and remove the containers.
