# MSSQL/Sqlpackage Docker Image
Baked in sql package in docker, and MSSQL + sqlpackage in docker as well.

## Usage:
There are two version of the docker image provided:
1. [Standalone sqlpackage](#standalone-sqlpackage)
2. [MSSQL + sqlpackage](#mssql-+-sqlpackage)

### Standalone sqlpackage
1. Build docker image
    ```powershell
    # in sqlpackage-docker
    ./build.ps1
    ```
2. Prepare your input script in a folder. (e.g. `input/data.bacpac`)
3. Run the standalone docker image with volume mounting input folder to `/app`.
    ```powershell
    docker run `
        -v C:\input:/app/input `
        sqlpackage-docker `
        # add your sqlpackage arguments here. e.g. :
        /a:Import `
        /sf:"/app/input/data.bacpac" `
        /tcs:"Server=host.docker.internal,1433;User ID=sa;Password=1234;Database=master-imported" 
    ```

### MSSQL + sqlpackage
1. Build docker image
    ```powershell
    # in mssql-sqlpackage-docker
    ./build.ps1
    ```
2. Prepare your input script in a folder. (e.g. `input/data.bacpac`)
3. Run the docker image as daemon, and expose the port.
    ```powershell
    docker run `
        -p 1434:1433 `
        -d `
        -v C:\input:/app/input `
        mssql-sqlpackage-docker
    # Container ID 4c4d65fd014c
    ```
4. Run the script via `docker exec`. Note that `sqlpackage` is already available in the image.
    ```powershell
    docker exec 4c4d65fd014c `
        sqlpackage `
        # add your sqlpackage arguments here. e.g. :
        /a:Import `
        /sf:"/app/input/data.bacpac" `
        /tcs:"Server=localhost,1433;User ID=sa;Password=1234;Database=master-imported" 
    ```