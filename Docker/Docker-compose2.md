```yaml
version: '3.8'
services:
  picard:
    image: quay.io/biocontainers/picard:3.2.0--hdfd78af_0
    volumes:
      - /mnt/sisplockers/krittiyabhornk:/home
    tty: true
    stdin_open: true
    command: bash

  samtools:
    image: quay.io/biocontainers/samtools:1.20--h50ea8bc_0
    volumes:
      - /mnt/sisplockers/krittiyabhornk:/home
    tty: true
    stdin_open: true
    command: bash
```

**Explanation:**

1.  **`version: '3.8'`:** Specifies the Docker Compose file format version.
2.  **`services:`:** Defines the services (containers) to run.
3.  **`picard:`:**
    * `image: quay.io/biocontainers/picard:3.2.0--hdfd78af_0`: Uses the specified Picard image.
    * `volumes: - /mnt/sisplockers/krittiyabhornk:/home`: Mounts the `/mnt/sisplockers/krittiyabhornk` directory from your host machine to the `/home` directory inside the container. This allows the container to access and modify files in that location.
    * `tty: true` and `stdin_open: true`: Enable interactive terminal access.
    * `command: bash`: Starts a bash shell when the container runs.
4.  **`samtools:`:**
    * `image: quay.io/biocontainers/samtools:1.20--h50ea8bc_0`: Uses the specified samtools image.
    * `volumes: - /mnt/sisplockers/krittiyabhornk:/home`: Shares the same volume as the Picard container. This allows both containers to access the same files.
    * `tty: true` and `stdin_open: true`: Enable interactive terminal access.
    * `command: bash`: Starts a bash shell when the container runs.

**How to Use:**

1.  **Save the YAML:** Save the code above as `docker-compose.yml` in a directory.
2.  **Run Docker Compose:** In the terminal, navigate to the directory where you saved the file and run:

    ```bash
    docker-compose up
    ```

3.  **Open Bash in Containers:** Open separate terminal windows and run:

    ```bash
    docker exec -it picard bash
    docker exec -it samtools bash
    ```

Now you have two containers running, one with Picard and one with samtools, both sharing the `/mnt/sisplockers/krittiyabhornk` directory through the `/home` mount point.
