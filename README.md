# QuickPerf
A simple performance collection tool to determine the performance of a GPU enabled environment. 

## Requirements
1. NVIDIA GPU
2. Docker and Docker Compose (`DOCKER_BUILDKIT=0` required)
3. NGC repo access.

## Launch
1. Build images: `DOCKER_BUILDKIT=0 docker compose build`
2. Launch containers: `docker compose up`
3. Logs will be written to `logs/`:
   1. `gpu-info.xml`
   2. `gpu-query.csv`
   3. `training-logs.json`

## Teardown
The training operation should run as long as you'd like as this is just a method of measuring performance. Once you've run the process long enough, you can kill the containers with `docker compose down` or `ctrl+c` if you're still in the same terminal.  