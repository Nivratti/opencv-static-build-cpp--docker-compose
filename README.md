# Opencv static build with cpp demo inside docker-compose
### statically building opencv to avoid any external dependency on production system to run generated binary file

## 1. Docker compose build and run useful commands:

```console
sudo docker compose build
sudo docker compose up
```

After running docker container, you can coonect it via bash from other terminal window.

```
sudo docker compose exec opencv bash
```

## 2. Building and testing demo - you can change dir inside docker to:
```
cd /workspace/opencv-dnn-demo/build/
cmake .. && make -j $nproc
./main
```
