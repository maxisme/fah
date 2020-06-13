# GPU setup
```
distribution=$(. /etc/os-release;echo $ID$VERSION_ID)
curl -s -L https://nvidia.github.io/nvidia-docker/gpgkey | sudo apt-key add -
curl -s -L https://nvidia.github.io/nvidia-docker/$distribution/nvidia-docker.list | sudo tee /etc/apt/sources.list.d/nvidia-docker.list
apt-get update && sudo apt-get install -y nvidia-container-toolkit nvidia-headless-440 nvidia-utils-440
```

```bash
docker run -d \
  --name=foldingathome \
  --gpus all \
  -e PUID=1000 \
  -e PGID=1000 \
  -e NVIDIA_VISIBLE_DEVICES=all \
  -e TZ=Europe/London \
  -p 7396:7396 \
  -v /root/fah/fahclient:/config \
  --restart always \
  linuxserver/foldingathome
```