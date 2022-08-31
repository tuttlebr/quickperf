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
   1. `gpu-info.xml` is the result of `nvidia-smi -q -x -f` and may be modified from [01-machine_info](root/etc/cont-init.d/01-machine_info)
   2. `gpu-query.csv` is the result of `nvidia-smi --query-gpu=index,timestamp,utilization.gpu,power.draw,clocks.gr,clocks.video,temperature.gpu,pstate,clocks_throttle_reasons.hw_thermal_slowdown,clocks_throttle_reasons.sw_thermal_slowdown,clocks_throttle_reasons.hw_slowdown,clocks_throttle_reasons.sw_power_cap,utilization.memory,memory.total,memory.free,memory.used,clocks_throttle_reasons.active --format=csv --loop=5` and may be modified from [run](root/etc/services.d/nvidia-smi/run)
   3. `training-logs.json` is the result of NVIDIA's DLLogger logging tool and will collect training specific metrics such as epuch times and imgs/s during training. While this is modifiable, it is not supported from this repo implimentation as the Docker container is built directly from the source repo's GitHub.

## Teardown
The training operation should run as long as you'd like as this is just a method of measuring performance. Once you've run the process long enough, you can kill the containers with `docker compose down` or `ctrl+c` if you're still in the same terminal.  