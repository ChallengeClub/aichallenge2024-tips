# 遭遇したエラーと解決方法


## rockerがうまく動かない
### 起こった現象

```
ubuntu@ubuntu-desktop:~/aichallenge-2024$ ./docker_run.sh dev cpu
usage: rocker [-h] [--noexecute] [--nocache] [--nocleanup] [--pull] [--version] [--cuda]
              [--dev-helpers] [--devices [DEVICES ...]] [--env NAME[=VALUE] [NAME[=VALUE] ...]]
              [--env-file ENV_FILE] [--expose EXPOSE] [--git] [--git-config-path GIT_CONFIG_PATH]
              [--group-add GROUP_ADD] [--home] [--hostname HOSTNAME] [--name NAME]
              image [command ...]
rocker: error: DependencyMissing encountered: Docker Client failed to connect to docker daemon. Please verify that docker is installed and running. As well as that you have permission to access the docker daemon. This is usually by being a member of the docker group. The underlying error was:
"""
Error while fetching server API version: Not supported URL scheme http+docker
"""
```

### 解決方法
ホスト側のros2 humbleをアンインストールする

### 改善後
```
ubuntu@ubuntu-desktop:~/aichallenge-2024$ rocker
Extension volume doesn't support default arguments. Please extend it.
usage: rocker [-h] [--noexecute] [--nocache] [--nocleanup] [--pull] [--version] [--cuda]
              [--dev-helpers] [--devices [DEVICES ...]] [--env NAME[=VALUE] [NAME[=VALUE] ...]]
              [--env-file ENV_FILE] [--expose EXPOSE] [--git] [--git-config-path GIT_CONFIG_PATH]
              [--group-add GROUP_ADD] [--home] [--hostname HOSTNAME] [--name NAME]
              [--network {none,host,bridge}] [--nvidia [{auto,runtime,gpus}]] [--port PORT]
              [--privileged] [--pulse] [--rmw {cyclonedds,fastrtps}] [--ssh] [--user]
              [--user-override-name USER_OVERRIDE_NAME] [--user-preserve-home]
              [--user-preserve-groups [USER_PRESERVE_GROUPS ...]]
              [--user-preserve-groups-permissive] [--user-override-shell USER_OVERRIDE_SHELL]
              [--volume HOST-DIR[:CONTAINER-DIR[:OPTIONS]] [HOST-DIR[:CONTAINER-DIR[:OPTIONS]]
              ...]] [--x11] [--mode {interactive,non-interactive,dry-run}]
              [--image-name IMAGE_NAME] [--extension-blacklist [EXTENSION_BLACKLIST ...]]
              [--strict-extension-selection]
              image [command ...]
rocker: error: the following arguments are required: image
```


## ./build_autoware.bash がうまくできない

### 起こった現象

```
ubuntu@ubuntu-desktop:/aichallenge$ ./build_autoware.bash 
Starting >>> aichallenge_submit_launch
Starting >>> goal_pose_setter
Starting >>> imu_gnss_poser
Starting >>> path_to_trajectory
Starting >>> racing_kart_description                                                              
Starting >>> racing_kart_sensor_kit_description
Starting >>> simple_pure_pursuit
--- stderr: simple_pure_pursuit                                               
CMake Error: The current CMakeCache.txt directory /aichallenge/workspace/build/simple_pure_pursuit/CMakeCache.txt is different than the directory /home/ubuntu/aichallenge-2024/aichallenge/workspace/build/simple_pure_pursuit where CMakeCache.txt was created. This may result in binaries being created in the wrong place. If you are not sure, reedit the CMakeCache.txt
CMake Error: The source "/aichallenge/workspace/src/aichallenge_submit/simple_pure_pursuit/CMakeLists.txt" does not match the source "/home/ubuntu/aichallenge-2024/aichallenge/workspace/src/aichallenge_submit/simple_pure_pursuit/CMakeLists.txt" used to generate cache.  Re-run cmake with a different source directory.
---
Failed   <<< simple_pure_pursuit [0.35s, exited with code 1]
Aborted  <<< aichallenge_submit_launch [0.62s]                                           
Aborted  <<< racing_kart_sensor_kit_description [0.50s]
Aborted  <<< racing_kart_description [0.53s]
Aborted  <<< goal_pose_setter [0.64s]
Aborted  <<< imu_gnss_poser [0.63s]
Aborted  <<< path_to_trajectory [0.61s]

Summary: 0 packages finished [1.35s]
  1 package failed: simple_pure_pursuit
  6 packages aborted: aichallenge_submit_launch goal_pose_setter imu_gnss_poser path_to_trajectory racing_kart_description racing_kart_sensor_kit_description
  7 packages had stderr output: aichallenge_submit_launch goal_pose_setter imu_gnss_poser path_to_trajectory racing_kart_description racing_kart_sensor_kit_description simple_pure_pursuit
  1 package not processed
```

### 解決方法
aichallenge-2024のレポジトリを最新のものをクローンする
