# 磁盘性能测试


## iozone

### iozone 安装

**Ubuntu 安装**

	sudo apt install iozone3

**Centos 安装**

	wget http://www.iozone.org/src/current/iozone3_434.tar
	tar -xvf iozone3_434.tar
	cd iozone3_434/src
	make linux-AMD64
	./iozone -h


### 使用iozone对文件系统进行基准测试

	$ iozone -a 
iozone 将在所有模式下进行测试，使用记录块从4k到16M，测试文件大小从64k到512M

	$ iozone -Ra 或 iozone -Rab output.xls 
iozone将测试结果放在Excel中

	$ iozone -Ra -g 2g 
如果内存大于512MB，则测试文件需要更大；最好测试文件是内存的两倍。例如内存为1G，将测试文件设置最大为2G

	$ iozone -Ra -g 2g -i 0 -i 1 
如果只关心文件磁盘的`read/write`性能，而不必花费时间在其他模式上测试，则我们需要指定测试模式

	$ iozone -Rac 
如果测试 NFS，将使用`-c`，这通知 iozone 在测试过程中执行`close()`函数。使用`close()`将减少 NFS 客户端缓存的影响。但是如果测试文件比内存大，就没有必要使用参数`-c`

	-a  在所有模式下进行测试，使用记录块从4k到16M，测试文件大小从64k到512M
	-b  生成excel文件
	-R  生成excel输入
	-f  指定临时文件名
	-g  自动模式的最大文件大小
	-n  自动模式的最小文件大小
	-s  指定文件大小，默认单位是KB, 也可以使用m 和 g
	-y  自动模式的最小记录大小，默认单位是KB
	-q  自动模式的最大记录大小，默认单位是KB
	-r  指定记录大小，单位是KB
	-i  选择测试模式
	0=write/rewrite
	1=read/re-read
	2=random-read/write
	3=Read-backwards
	4=Re-write-record
	5=stride-read
	6=fwrite/re-fwrite
	7=fread/Re-fread,
	8=random mix
	9=pwrite/Re-pwrite
	10=pread/Re-pread
	11=pwritev/Re-pwritev
	12=preadv/Repreadv

例如：

	$ iozone -a -s 128M -y 512 -q 16384 -i 0 -i 1 -i 2 -f /test/a.out -Rb /root/ext3_writeback.out

## fio

### fio 安装

FIO 是测试 IOPS 的非常好的工具，用来对硬件进行压力测试和验证，支持 13 种不同的 IO 引擎，包括：sync, mmap, libaio, posixaio, SG v3, splice, null, network, syslet, guasi, solarisaio 等等。

IOPS (Input/Output Operations Per Second)， 即每秒进行读写（I/O）操作的次数，多用于数据库等场合，衡量随机访问的性能。 IOPS是指存储每秒可接受多少次主机发出的访问，主机的一次IO需要多次访问存储才可以完成。

bw 传输带宽。bw=19372KB/s,

**Ubuntu 安装**

	sudo apt install fio

**Centos 安装**

	yum install libaio-devel fio


### 测试 

**顺序读**

每次读取大小4k的块，默认的`ioengine=sync`,运行`60s(runtime) -direct=1`,跳过 buffer 

	fio -filename=/data/hello -direct=1 -bs=4k -rw=write -size=5G -numjobs=8 -runtime=60 -group_reporting -name=test_for_sync

**随机读**

	fio -filename=/dev/sdb1 -direct=1 -iodepth 1 -thread -rw=randread -ioengine=psync -bs=16k -size=200G -numjobs=10 -runtime=1000 -group_reporting -name=mytest


说明

	filename=/dev/sdb1       测试文件名称，通常选择需要测试的盘的data目录。 
	direct=1                 测试过程绕过机器自带的buffer。使测试结果更真实。 
	rw=randwrite             测试随机写的I/O 
	rw=randrw                测试随机写和读的I/O 
	bs=16k                   单次io的块文件大小为16k 
	bsrange=512-2048         同上，提定数据块的大小范围 
	size=5g                  本次的测试文件大小为5g，以每次4k的io进行测试。 
	numjobs=30               本次的测试线程为30. 
	runtime=1000             测试时间为1000秒，如果不写则一直将5g文件分4k每次写完为止。 
	ioengine=psync           io引擎使用pync方式 
	rwmixwrite=30            在混合读写的模式下，写占30% 
	group_reporting          关于显示结果的，汇总每个进程的信息。 
	此外 
	lockmem=1g               只使用1g内存进行测试。 
	zero_buffers             用0初始化系统buffer。 
	nrfiles=8                每个进程生成文件的数量。

**顺序读**

	$ fio -filename=/dev/sdb1 -direct=1 -iodepth 1 -thread -rw=read -ioengine=psync -bs=16k -size=200G -numjobs=30 -runtime=1000 -group_reporting -name=mytest

**随机写**

	$ fio -filename=/dev/sdb1 -direct=1 -iodepth 1 -thread -rw=randwrite -ioengine=psync -bs=16k -size=200G -numjobs=30 -runtime=1000 -group_reporting -name=mytest

**顺序写**

	$ fio -filename=/dev/sdb1 -direct=1 -iodepth 1 -thread -rw=write -ioengine=psync -bs=16k -size=200G -numjobs=30 -runtime=1000 -group_reporting -name=mytest

**混合随机读写**

	$ fio -filename=/dev/sdb1 -direct=1 -iodepth 1 -thread -rw=randrw -rwmixread=70 -ioengine=psync -bs=16k -size=200G -numjobs=30 -runtime=100 -group_reporting -name=mytest -ioscheduler=noop 