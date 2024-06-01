# ---RAID10
# Этот Vagrantfile создаст виртуальную машину с 4 дополнительными дисками и запустит скрипт setup_raid.sh, который выполнит следующие действия:
# Установит необходимые пакеты mdadm и parted
# Создаст RAID10 из 4 дисков
# Настроит конфигурационный файл для автоматической сборки RAID при загрузке
# Создаст GPT раздел на RAID
# Создаст 5 партиций на RAID
# Создаст файловые системы на каждой из партиций
# Смонтирует партиции и добавит записи в /etc/fstab для автоматического монтирования при загрузке
# Требуется сохранить оба файла в одной директории и выполнить vagrant up для создания и настройки виртуальной машины
# $lsblk
sdb                         8:16   0     1G  0 disk
└─md0                       9:0    0     2G  0 raid10
  ├─md0p1                 259:1    0   408M  0 part   /mnt/raid/part1
  ├─md0p2                 259:4    0   409M  0 part   /mnt/raid/part2
  ├─md0p3                 259:5    0   408M  0 part   /mnt/raid/part3
  ├─md0p4                 259:8    0   409M  0 part   /mnt/raid/part4
  └─md0p5                 259:9    0   408M  0 part   /mnt/raid/part5
sdc                         8:32   0     1G  0 disk
└─md0                       9:0    0     2G  0 raid10
  ├─md0p1                 259:1    0   408M  0 part   /mnt/raid/part1
  ├─md0p2                 259:4    0   409M  0 part   /mnt/raid/part2
  ├─md0p3                 259:5    0   408M  0 part   /mnt/raid/part3
  ├─md0p4                 259:8    0   409M  0 part   /mnt/raid/part4
  └─md0p5                 259:9    0   408M  0 part   /mnt/raid/part5
sdd                         8:48   0     1G  0 disk
└─md0                       9:0    0     2G  0 raid10
  ├─md0p1                 259:1    0   408M  0 part   /mnt/raid/part1
  ├─md0p2                 259:4    0   409M  0 part   /mnt/raid/part2
  ├─md0p3                 259:5    0   408M  0 part   /mnt/raid/part3
  ├─md0p4                 259:8    0   409M  0 part   /mnt/raid/part4
  └─md0p5                 259:9    0   408M  0 part   /mnt/raid/part5
sde                         8:64   0     1G  0 disk
└─md0                       9:0    0     2G  0 raid10
  ├─md0p1                 259:1    0   408M  0 part   /mnt/raid/part1
  ├─md0p2                 259:4    0   409M  0 part   /mnt/raid/part2
  ├─md0p3                 259:5    0   408M  0 part   /mnt/raid/part3
  ├─md0p4                 259:8    0   409M  0 part   /mnt/raid/part4
  └─md0p5                 259:9    0   408M  0 part   /mnt/raid/part5

# mdadm --manage /dev/md0 --fail /dev/sdb  # присваиваем диску статус fail
# mdadm: set /dev/sdb faulty in /dev/md0

# sudo mdadm --manage /dev/md0 --remove /dev/sdb # убираем диск из RAID

# $lsblk 
sdb                         8:16   0     1G  0 disk
sdc                         8:32   0     1G  0 disk
└─md0                       9:0    0     2G  0 raid10
  ├─md0p1                 259:1    0   408M  0 part   /mnt/raid/part1
  ├─md0p2                 259:4    0   409M  0 part   /mnt/raid/part2
  ├─md0p3                 259:5    0   408M  0 part   /mnt/raid/part3
  ├─md0p4                 259:8    0   409M  0 part   /mnt/raid/part4
  └─md0p5                 259:9    0   408M  0 part   /mnt/raid/part5
sdd                         8:48   0     1G  0 disk
└─md0                       9:0    0     2G  0 raid10
  ├─md0p1                 259:1    0   408M  0 part   /mnt/raid/part1
  ├─md0p2                 259:4    0   409M  0 part   /mnt/raid/part2
  ├─md0p3                 259:5    0   408M  0 part   /mnt/raid/part3
  ├─md0p4                 259:8    0   409M  0 part   /mnt/raid/part4
  └─md0p5                 259:9    0   408M  0 part   /mnt/raid/part5
sde                         8:64   0     1G  0 disk
└─md0                       9:0    0     2G  0 raid10
  ├─md0p1                 259:1    0   408M  0 part   /mnt/raid/part1
  ├─md0p2                 259:4    0   409M  0 part   /mnt/raid/part2
  ├─md0p3                 259:5    0   408M  0 part   /mnt/raid/part3
  ├─md0p4                 259:8    0   409M  0 part   /mnt/raid/part4
  └─md0p5                 259:9    0   408M  0 part   /mnt/raid/part5

# sudo mdadm --manage /dev/md0 --add /dev/sdb добавляет диск в RAID и выполняет ребилд
# ---