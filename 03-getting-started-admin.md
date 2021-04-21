# Getting Started with Administration

## Basic Admin Commands
- `who` -- outputs who is on the host currently
- `whoami` -- outouts who you are currently logged in as
- `date` -- outputs current time
- `time` -- outputs how long the current session has been running
- `printenv` -- outputs all user/group environment variables
- `id` -- outputs all the user information and affliated groups or a users info
- `users` -- outputs users on a host
- `useradd` -- adds user on a host
- `groups` -- outputs user groups or a users groups
- `groupadd` -- adds user to group or creates a group
- `ssh-keygen` -- creates a ssh-key for you to securely access servers.
- `grep` -- finds a value in a text or directory
- `|` -- pipe used to run commands at the same time/parallel
- `chmod` -- change access to a file or directory
- `chown` -- change owner to a file or directory
- `df` -- output disk/storage capacity
- `man` -- manual of commands
- `wc` -- word count but usually used for counting number of output per line
- `systemctl` -- controls systemd services
- `sudo` -- use super-user permissions
- `shutdown` -- shutdown the server
- `reboot` -- reboot the server
- `top` -- see what processes are running
- `sudo su -` - the only `su` command you should use as user root
- `exit` - exit the session
- `ps`

Let's get started!

FYI - Most of these commands apply to your host machine and servers. 

1. `ssh` into a server.
    ```
    ssh <some-ip-address> 
    Last login: Tue Mar  9 18:14:14 UTC 2021 from <some-ip-address> on ssh
    ```
2. `who` allows you to see who is currently signed on to a server.
    ```
    jyang060@<some-ip-address> ~ $ who
    jyang pts/2        Apr 21 22:06 (<some-ip-address>)
    ```
3. `date` will help you see what timezone the server is running on. 
    ```
    jyang060@<some-ip-address> ~ $ date
    Wed Apr 21 22:12:03 UTC 2021
    ```
4. `time` don't dont get the date command confused with time because one shows the current server time and one shows how long you have logged on a server.
    ```
    jyang060@<some-ip-address> ~ $ time

    real	0m0.000s
    user	0m0.000s
    sys	0m0.000s
    ```
5. When you need to figure out what environment variables exist use `printenv`. Some environment variables hold sensitive information like where important files and locations are so for this example I am going to be leaving it out.
6. As a admin one useful command for you to find permission problems is `id` id will allow you to see what groups you're under and what your __uid__ is. A uid is your user ID and it should be different across all other user IDs. GID stands for group ID and can be shared per user. 
    ```
    ❯ id
    uid=502(jyang060) gid=20(staff) groups=20(staff)
    ```
7. Similar to `id` there is also the command `groups` which outpouts all the group names you're in but not the GID. Groups can be created and similarly users can be added via `groupadd` and `useradd` commands but if neither commands are working you can always edit the file in `/etc/group`. 

8. `ssh-keygen` allows you to create __ssh keys__. You can encrypt keys to be certain bytes or type of encryption methods like RSA and etc... but for simplicity sake we will create a simple ssh-key. 
    ```
    ❯ ssh-keygen
    Generating public/private rsa key pair.
    Enter file in which to save the key (/Users/jyang060/.ssh/id_rsa): test-key
    Enter passphrase (empty for no passphrase):
    Enter same passphrase again:
    Your identification has been saved in test-key.
    Your public key has been saved in test-key.pub.
    The key fingerprint is:
    SHA256:DHH86+pm8cYv4nFH9ueMPVGvzV9QzORNI/6qSAomSJ4 jyang060@COSML-1719674
    The key's randomart image is:
    +---[RSA 3072]----+
    |      ...    . .o|
    |       o.   . .*o|
    |      .  .   .  *|
    |       o  .   ...|
    | .      S  .o ..o|
    |o o     . .o ..o.|
    | E . o  .*. ...++|
    |    o . *oB.. .B+|
    |       *+= +. . B|
    +----[SHA256]-----+
    ❯ ls -l .ssh/test*
    -rw-------@ 1 jyang060  staff  2610 Nov 11 12:20 .ssh/test
    -rw-r--r--@ 1 jyang060  staff   576 Nov 11 12:20 .ssh/test.pub
    ```
9. `grep` is a word pattern finder in files. This command is very useful when you need to search logs or look up any files in a directory with a certain word in their content. Below I am using grep to find any line with the word "image" and output it to the terminal.
    ```
    ❯ grep image simple.yaml
            image: hub.comcast.net/sepulse/neues-server:1.35.0-be50bb0
            imagePullPolicy: IfNotPresent
    ```
10. `|` is not a command and is called "pipe" but pipe allows you to combine commands together.
    ```
    ❯ ls -l | grep .yaml
    -rw-r--r--   1 jyang060  staff    358 Dec 14 13:31 kh-aortb-svc-monitoring.yaml
    -rw-r--r--   1 jyang060  staff   1809 Apr 21 09:45 simple.yaml
    -rw-r--r--   1 jyang060  staff   5214 Feb 18 15:12 sysdig-cm.yaml
    -rw-r--r--   1 jyang060  staff   1012 Dec 14 13:29 tmp.yaml
    ```
    Obviously you can use a wild card with `ls -l` to find any file with the ending .yaml but not all commands will worth with wild-cards.
11. The `chmod` command allows you to change the permission of a file. You can find a [permission calculator](http://permissions-calculator.org/) as you build your command line skills. Why it matters is that you dont want a file to be openly available to anyone. If there are secrets or sensivtive infomation you want to protect it from being read, moditfied or executed by other users.
    ```
    ❯ ls -l tmp.yaml
    -rw-r--r--  1 jyang060  staff  1012 Dec 14 13:29 tmp.yaml
    ```
    In this case `-rw-r--r--` is the permission. What this tells us is that, and you should look at this split in the view of columbs as pairs of 3s `rw-` is read and write owned by the user. Both group and all-users(everyone) is `r--` which is read-only. How to use `chmod` to make it so that it is __rw__ to your group see below:
    ```
    ❯ sudo chmod 664 tmp.yaml
    ❯ ls -l tmp.yaml
    -rw-rw-r--  1 jyang060  staff  1012 Dec 14 13:29 tmp.yaml
    ```
    As you can see 664 will allow __rw__ to the owner of the file and their group and allow everyone else with just read. When using `chmod` you will need to specify `sudo` with the command. I will later explain `sudo`.
12. Similarly with `chmod` using `chown` will change the owner of a file and can also change the group as well. In this example we switched the group from staff to admin.
    ```
    ❯ ls -l tmp.yaml
    -rw-rw--wx  1 jyang060  staff  1012 Dec 14 13:29 tmp.yaml
    ❯ sudo chown jyang060:admin tmp.yaml
    ❯ ls -l tmp.yaml
    -rw-rw-r--  1 jyang060  admin  1012 Dec 14 13:29 tmp.yaml
    ```
13. Sometimes when troubleshooting checking if you have enough disk/storage will be a common thing you look at. The `df` command will help you determine if your storage HDD is full.
    ```
    ❯ df -h
    Filesystem      Size   Used  Avail Capacity iused      ifree %iused  Mounted on
    /dev/disk1s5   466Gi   10Gi  353Gi     3%  488309 4881964571    0%   /
    devfs          187Ki  187Ki    0Bi   100%     646          0  100%   /dev
    /dev/disk1s1   466Gi   99Gi  353Gi    22% 1324856 4881128024    0%   /System/Volumes/Data
    /dev/disk1s4   466Gi  3.0Gi  353Gi     1%       3 4882452877    0%   /private/var/vm
    map auto_home    0Bi    0Bi    0Bi   100%       0          0  100%   /System/Volumes/Data/home
    /dev/disk1s3   466Gi  504Mi  353Gi     1%      50 4882452830    0%   /Volumes/Recovery
    ```
    It's hard to read the size sometimes because its default output measured size is it bytes so append the param `-h` with it to get a calculated size. Also UNIX based OS do not label drives like Windows computer. Although you might think its easier UNIX based computers sees HDD as a device on the computer and labels them accordingly from the first HDD as __disk1s1__. The __s1__ that is appende to the end of it tells you what partition it is. The __disk1__ portion means it the HDD that you are using. If you have multiple HDD it will be label from __disk1__ to __disk2__ and so on.

14. The `man` command can be useful when you dont know how to use a command. It will give you a manual on how to use it.

15. The `wc` command stands for word count and can be useful when you want to count how many files are in a directory by counting number of lines. You will need to pipe it to a command though as in the example.
    ```
    ❯ ls | wc -l
      29
    ```
16. Whenever you hear about systemd and need to control it think of `systemctl`. This command is used to control systemd services. 
    ```
    jyang@<some-ip-address> ~ $ sudo systemctl status docker
    ● docker.service - Docker Application Container Engine
    Loaded: loaded (/run/systemd/system/docker.service; disabled; vendor preset: disabled)
    Drop-In: /etc/systemd/system/docker.service.d
            └─50-docker-opts.conf
    Active: active (running) since Sun 2021-01-31 20:36:25 UTC; 2 months 19 days ago
        Docs: http://docs.docker.com
    Main PID: 8333 (dockerd)
        Tasks: 145
    Memory: 2.2G
    CGroup: /system.slice/docker.service
            └─8333 /run/torcx/bin/dockerd --host=fd:// --containerd=/var/run/docker/libcontainerd/docker-containerd.sock --selinux-enabled=true --log-driver=json-file --log-opt max-size=10m -H unix:///var/run/rdei/docker.sock --init --bip>

    Apr 21 22:00:03 <some-ip-address> env[8333]: time="2021-04-21T22:00:03.681328187Z" level=info msg="ignoring event" module=libcontainerd namespace=moby topic=/tasks/delete type="*events.TaskDelete"
    Apr 21 22:00:04 <some-ip-address> env[8333]: time="2021-04-21T22:00:04.053342153Z" level=info msg="ignoring event" module=libcontainerd namespace=moby topic=/tasks/delete type="*events.TaskDelete"
    Apr 21 22:15:01 <some-ip-address> env[8333]: time="2021-04-21T22:15:01.668764804Z" level=info msg="ignoring event" module=libcontainerd namespace=moby topic=/tasks/delete type="*events.TaskDelete"
    ```
    In the above example I paired the command with `status` to get an output on the status of the docker systemd service. It's in a `active (running) since` state which is good, if its ever inactive or failed then that is a problem you will want to troubleshoot by reading the events it outputs with it. Other than that you can replace status with `start`, `restart`, and `stop`. BE VERY CAREFUL OF WHAT YOU __STOP__ IN PRODUCTION!

17. To reboot (restart) a server if its not behaving correctly you can either use either command with sudo `sudo reboot` or `sudo shutdown -r`. The reboot command is more safe if you are unsure. BE VERY CAREFUL OF WHAT YOU __REBOOT__ IN PRODUCTION!
18. Before you run the `sudo shutdown` command make sure you are able to power on the server back up again if it goes down because you wont be able to walk int oa datacenter to power it back on if its 1000 miles away from you. 
19. So why are we pairing some commands with `sudo`? `sudo` is actually a super-user command (aka admin-privilaged command) to do big changes on a server/computer. If you are not the user `root` you have to use the command `sudo`. `sudo` servers as a safe-guard so that you dont accidently shut a server down by accident or change anything that is a systemd service or file. 
20. To login as the user `root` login into a server and run this command `sudo su -` this will sign you on as root to the server. BE VERY CAREFUL AS YOU WONT NEED TO TYPE IN SUDO TO RUN ANY COMMANDS AND CAN DO A LOT OF DAMAGE THAT CANT BE UNDONE!
21. To see what processes are currently running on a server use `top`. 
    ```
    Processes: 526 total, 2 running, 524 sleeping, 3324 threads                                                                                                                                                                          17:12:33
    Load Avg: 2.31, 1.90, 1.76  CPU usage: 3.51% user, 2.34% sys, 94.13% idle   SharedLibs: 214M resident, 50M data, 14M linkedit. MemRegions: 255410 total, 4410M resident, 115M private, 2736M shared.
    PhysMem: 16G used (3289M wired), 38M unused. VM: 4884G vsize, 1991M framework vsize, 6185823(0) swapins, 6587884(0) swapouts. Networks: packets: 5827627/5931M in, 3617829/578M out. Disks: 2864389/73G read, 1996910/45G written.

    PID    COMMAND      %CPU TIME     #TH    #WQ  #PORT MEM    PURG   CMPRS  PGRP  PPID  STATE    BOOSTS          %CPU_ME %CPU_OTHRS UID  FAULTS    COW   MSGSENT   MSGRECV   SYSBSD     SYSMACH    CSW        PAGEIN IDLEW    POWE INSTRS
    707    iTerm2       29.0 32:20.29 16     13   462-  828M+  215M-  58M    707   1     sleeping *0[1992]        0.22300 1.41775    502  20591135+ 2944  4828048+  4529828+  14566900+  116707530+ 15447426+  4588   4793291+ 54.0 714870083
    263    WindowServer 7.0  40:02.28 10     4    2570- 604M   2624K  70M    263   1     sleeping *0[1]           1.43031 0.05784    88   4761814+  70009 41939081+ 21920050+ 17529528+  63455135+  22926124+  7679   844622+  8.3  89951259
    27652  top          5.6  00:00.95 1/1    0    25    6732K+ 0B     0B     27652 24080 running  *0[1]           0.00000 0.00000    0    5289+     131   642959+   321437+   13180+     351129+    455+       24     4+       5.6  137296371
    2154   com.docker.h 4.6  29:22.11 13     0    36    8940M  0B     742M   1160  2140  sleeping *0[1]           0.00000 0.00000    502  2396505+  478   441       264       41802801+  642        24032200+  163    2650699+ 7.6  20128953
    ```
    `top` is only good to see system load and HDD sizes live and what is consuming the most of the cpu and memory.
22. If you don't want to see all the processes there is you can always narrow down if a processes is running by using the commnad `ps`. Thats if you know the proccess's name.
    ```
    ❯ ps -ef | grep docker
    502  1160  1122   0 Tue03PM ??         0:11.07 /Applications/Docker.app/Contents/MacOS/com.docker.backend -watchdog
        0  2083     1   0 Tue03PM ??         0:00.06 /Library/PrivilegedHelperTools/com.docker.vmnetd
    502  2087  1160   0 Tue03PM ??         0:02.80 /Applications/Docker.app/Contents/MacOS/com.docker.supervisor -watchdog
    502  2129  2087   0 Tue03PM ??         0:00.06 com.docker.osxfs serve --address fd:3 --connect vms/0/connect --control fd:4
    502  2136  2087   0 Tue03PM ??         0:03.45 com.docker.vpnkit --ethernet fd:3 --diagnostics fd:4 --pcap fd:5 --vsock-path vms/0/connect --host-names host.docker.internal,docker.for.mac.host.internal,docker.for.mac.localhost --listen-backlog 32 --mtu 1500 --allowed-bind-addresses 0.0.0.0 --dhcp /Users/jyang060/Library/Group Containers/group.com.docker/dhcp.json --port-max-idle-time 300 --max-connections 2000 --gateway-ip 192.168.65.1 --host-ip 192.168.65.2 --lowest-ip 192.168.65.3 --highest-ip 192.168.65.254 --log-destination asl --gc-compact-interval 1800
    502  2140  2087   0 Tue03PM ??         0:03.68 com.docker.driver.amd64-linux -addr fd:3 -debug
    502  2141  2087   0 Tue03PM ??         0:04.84 docker serve --address unix:///Users/jyang060/.docker/run/docker-cli-api.sock
    502  2154  2140   0 Tue03PM ??        29:29.96 com.docker.hyperkit -A -u -F vms/0/hyperkit.pid -c 4 -m 8192M -s 0:0,hostbridge -s 31,lpc -s 1:0,virtio-vpnkit,path=vpnkit.eth.sock,uuid=164f82af-15e1-47b7-9af5-27eb2f2dfed4 -U 20b51830-4026-45b2-9fb9-bdcfcec6a669 -s 2:0,virtio-blk,/Users/jyang060/Library/Containers/com.docker.docker/Data/vms/0/data/Docker.raw -s 3,virtio-sock,guest_cid=3,path=vms/0,guest_forwards=2376;1525 -s 4,virtio-rnd -l com1,null,asl,log=vms/0/console-ring -f kexec,/Applications/Docker.app/Contents/Resources/linuxkit/kernel,/Applications/Docker.app/Contents/Resources/linuxkit/initrd.img,earlyprintk=serial page_poison=1 vsyscall=emulate panic=1 nospec_store_bypass_disable noibrs noibpb no_stf_barrier mitigations=off console=ttyS0 console=ttyS1  vpnkit.connect=connect://2/1999
    502 27698 24080   0  5:15PM ttys000    0:00.00 grep --color=auto --exclude-dir=.bzr --exclude-dir=CVS --exclude-dir=.git --exclude-dir=.hg --exclude-dir=.svn --exclude-dir=.idea --exclude-dir=.tox docker
    ```
    You will need to pipe the name of the process you're looking for with a grep to find all related proccesses. Also pair the command with the param `-ef` which is commonly used when running the command `ps`. Find a process this way is very useful because this allows you to see a processes ID (PID). The PID is a good way for you to identify which process you might need to kill. The PID is the middle column, in the example above first row, the PID is 1160.
23. After you are done with a server you want to make sure you logout of the server. Leaving them hang will allow you to unproperly disconnect from them and also its good practice for you to exit out from them incase you think its your actual localhost. The command to logout of a server is `exit`.

### Summery 
These are some of the most basic commands you should familiar yourself with as it will be handy to you in most scenario where you have to modify files and check hardware/devices attached to a host/virtual machine (VM). When you start using AWS for instance sometimes spinning up a new EC2 (aka, VM) you will need to pre-configure it if you dont have tools that are already setup on the AWS account to automatically setup a new server. These commands will help you do that. As a rule of thumb and best practices don't `sudo su -` all the time or use `sudo` if you can get away with not having to use either commands that would be best but if you must be very careful on what commands you use as it can be devestating. 


