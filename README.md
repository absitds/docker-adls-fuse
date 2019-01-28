docker build -t  adls_fuse:1.0.0 .

As we are mounting the drive --privileged  is needed
docker run -it -d -v  /home/exa00015/fuse/conf/:/etc/hadoop/conf/  -e ABFS_URI=abfs://sprk-itds-dev-wus-2019-01-23t04-24-36-227z@absitdsdevwus001.dfs.core.windows.net --privileged adls_fuse:1.0.0
