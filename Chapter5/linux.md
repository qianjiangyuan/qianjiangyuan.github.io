# 5.2: linux操作

#### 查看

```
# 文件系统的磁盘空间占用情况，通常可以查看挂载情况
df -h
```



#### 查找

​	一般用grep，用法也比较多

```
grep -r xxxxxx /usr/WebPortal 
grep -rnw . -e FAMILY_TOKEN
```



挂载

```
# 查看设备
fdisk -l

# 把设备sde1挂载成/mnt/目录
sudo mount /dev/sde1 /mnt/dlwsdata4

# 把storage下的某个目录挂载到/tmp/目录
sudo mount zjlab-storage:/mnt/dlwsdata /tmp/zjlab-storage
```

