# Домашка по управлению процессами
##Задача: реализовать 2 конкурирующих процесса по IO. пробовать запустить с разными ionice
1. ionice.sh
```
#/bin/bash

# Запускаем одновременно 2 команды с разным приоритетом
time nice -n -20 su -c "dd if=/dev/zero of=/tmp/test.img bs=2000 count=1M" &  time nice -n 19 su -c "dd if=/dev/zero of=/tmp/test2.img bs=2000 count=1M" &
```
# Результат
```
[1] 22650
[2] 22651
[root@centos tmp]# 1048576+0 records in
1048576+0 records out
2097152000 bytes (2.1 GB) copied, 3.58481 s, 585 MB/s

real    0m3.890s
user    0m0.805s
sys     0m2.985s
1048576+0 records in
1048576+0 records out
2097152000 bytes (2.1 GB) copied, 3.66908 s, 572 MB/s

real    0m3.900s
user    0m0.804s
sys     0m3.072s

[1]-  Done                    time nice -n -20 su -c "dd if=/dev/zero of=/tmp/test.img bs=2000 count=1M"
[2]+  Done                    time nice -n 15 su -c "dd if=/dev/zero of=/tmp/test2.img bs=2000 count=1M"
```
