# jupyter-notebook-on-docker-wsl2

[Full instructions on installing docker with wsl2 on windows](https://docs.docker.com/docker-for-windows/wsl/)

## Install wsl 2
1. **Enable the required features**  
*Powershell:*
```
dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
```

2. **Restart your PC**

3. Download and run the wsl2 kernel update [download here](https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi)

4. Then set default version to wsl2:  
Powershell:
```
wsl --set-default-version 2
```

## Setting up Linux distribution

1. **Install linux distribution from windows store** (example Ubuntu)
2. **start distribution**
3. **Install latest updates**  
Linux shell:
```
apt update 
apt dist-upgrade
```

## Install Docker Desktop

1. **Download Docker Desktop** [here](https://hub.docker.com/editions/community/docker-ce-desktop-windows/)
2. **Enable wsl2 integation in Docker: Settings/Resources/wsl integration**

## Setting up Jupyter notebook 
1. **Check that everything is set up correctly**  
Linux shell:
```
docker --version
Docker version 20.10.5, build 55c4c88
```

2. **Create folder for persistent data**
```
cd ~
mkdir ~/docker/notebooks
```

3. **Creating docker container**
```
docker run -p 127.0.0.1:8888:8888 -v ~/docker/notebooks:/home/jovyan -e GRANT_SUDO=yes --user root --name jupyter jupyter/all-spark-notebook
```
*If root privileges are not required, use:*
```
docker run -p 127.0.0.1:8888:8888 -v ~/docker/notebooks:/home/jovyan --name jupyter jupyter/all-spark-notebook
```
*If you need access from another PC on your network, use:*
```
docker run -p 8888:8888 -v ~/docker/notebooks:/home/jovyan --name jupyter jupyter/all-spark-notebook
```
4. **Copy token from shell and open http://localhost:8888/ or http://127.0.0.1:8888/**