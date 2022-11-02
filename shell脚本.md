#!/bin/sh
log="/home/zjy/code/shell/checklcpulog.txt"

time=`date "+%Y-%m-%d %k:%M"`
day=`date "+%Y-%m-%d"`
minute=`date "+%k:%M"`
echo  "*************************************************************************" >> LOG.txt
echo "统计开始时间：$day $minute" >>$log

cpuuse=$(cat /proc/loadavg | awk '{print $1}')
if [ "$cpuuse" > 0 ]; then
SUBJECT="ATTENTION: CPU Load Is High on $(hostname) at $(date)"
TO="*****@qq.com你的邮箱地址"
echo "CPU Current Usage is: $cpuuse%" >>$log
echo "" >>$log
echo "+-------------------------------------+" >>$log
echo "Top CPU Process Using top command" >>$log
echo "+-------------------------------------+" >>$log
echo "$(top -bn1 | head -20)" >>$log
echo "" >>$log
echo "+-------------------------------------+" >>$log
echo "Top CPU Process Using ps command" >>$log
echo "+-------------------------------------+" >>$log
echo "$(ps -eo pcpu,pid,user,args | sort -k 1 -r | head -10)" >>$log
mail -s "$SUBJECT" "$TO" <$log
fi



运行后的checkcpulog.txt

统计开始时间：2022-11-01 20:34
CPU Current Usage is: 0.38%

+-------------------------------------+
Top CPU Process Using top command
+-------------------------------------+
top - 20:34:15 up  5:01,  1 user,  load average: 0.38, 0.34, 0.29
任务: 294 total,   1 running, 293 sleeping,   0 stopped,   0 zombie
%Cpu(s): 17.1 us, 14.3 sy,  0.0 ni, 68.6 id,  0.0 wa,  0.0 hi,  0.0 si,  0.0 st
MiB Mem :   7375.8 total,   4086.6 free,   1280.6 used,   2008.6 buff/cache
MiB Swap:   2048.0 total,   2048.0 free,      0.0 used.   5697.3 avail Mem 

 进程号 USER      PR  NI    VIRT    RES    SHR    %CPU  %MEM     TIME+ COMMAND
   1306 zjy       20   0 4600740 625708 204312 S  29.4   8.3  13:53.52 gnome-s+
   1556 zjy       20   0 1029104 121144  76676 S  17.6   1.6   0:16.40 nautilus
   7623 zjy       20   0   21912   3968   3352 R   5.9   0.1   0:00.03 top
      1 root      20   0  102368  13152   8152 S   0.0   0.2   0:03.01 systemd
      2 root      20   0       0      0      0 S   0.0   0.0   0:00.04 kthreadd
      3 root       0 -20       0      0      0 I   0.0   0.0   0:00.00 rcu_gp
      4 root       0 -20       0      0      0 I   0.0   0.0   0:00.00 rcu_par+
      5 root       0 -20       0      0      0 I   0.0   0.0   0:00.00 netns
      7 root       0 -20       0      0      0 I   0.0   0.0   0:00.00 kworker+
      9 root       0 -20       0      0      0 I   0.0   0.0   0:00.85 kworker+
     10 root       0 -20       0      0      0 I   0.0   0.0   0:00.00 mm_perc+
     11 root      20   0       0      0      0 S   0.0   0.0   0:00.00 rcu_tas+
     12 root      20   0       0      0      0 S   0.0   0.0   0:00.00 rcu_tas+

+-------------------------------------+
Top CPU Process Using ps command
+-------------------------------------+
%CPU     PID USER     COMMAND
 4.6    1306 zjy      /usr/bin/gnome-shell
 2.4    5893 zjy      /usr/bin/gedit --gapplication-service
 0.1     675 root     /usr/bin/vmtoolsd
 0.1    6659 root     [kworker/1:1-events]
 0.1     633 systemd+ /lib/systemd/systemd-oomd
 0.1    2342 zjy      /usr/libexec/gnome-terminal-server
 0.1    1680 zjy      /usr/bin/vmtoolsd -n vmusr --blockFd 3 --uinputFd 4
 0.0       9 root     [kworker/0:1H-events_highpri]
 0.0      99 root     [irq/27-pciehp]
统计开始时间：2022-11-01 20:36
CPU Current Usage is: 0.20%

+-------------------------------------+
Top CPU Process Using top command
+-------------------------------------+
top - 20:36:03 up  5:03,  1 user,  load average: 0.20, 0.29, 0.27
任务: 294 total,   1 running, 293 sleeping,   0 stopped,   0 zombie
%Cpu(s): 23.5 us, 17.6 sy,  0.0 ni, 58.8 id,  0.0 wa,  0.0 hi,  0.0 si,  0.0 st
MiB Mem :   7375.8 total,   4083.2 free,   1283.8 used,   2008.9 buff/cache
MiB Swap:   2048.0 total,   2048.0 free,      0.0 used.   5694.1 avail Mem 

 进程号 USER      PR  NI    VIRT    RES    SHR    %CPU  %MEM     TIME+ COMMAND
   1306 zjy       20   0 4600752 625756 204312 S  50.0   8.3  14:12.69 gnome-s+
   2342 zjy       20   0  691860  99892  78548 S   6.2   1.3   0:21.39 gnome-t+
      1 root      20   0  102368  13152   8152 S   0.0   0.2   0:03.01 systemd
      2 root      20   0       0      0      0 S   0.0   0.0   0:00.04 kthreadd
      3 root       0 -20       0      0      0 I   0.0   0.0   0:00.00 rcu_gp
      4 root       0 -20       0      0      0 I   0.0   0.0   0:00.00 rcu_par+
      5 root       0 -20       0      0      0 I   0.0   0.0   0:00.00 netns
      7 root       0 -20       0      0      0 I   0.0   0.0   0:00.00 kworker+
      9 root       0 -20       0      0      0 I   0.0   0.0   0:00.86 kworker+
     10 root       0 -20       0      0      0 I   0.0   0.0   0:00.00 mm_perc+
     11 root      20   0       0      0      0 S   0.0   0.0   0:00.00 rcu_tas+
     12 root      20   0       0      0      0 S   0.0   0.0   0:00.00 rcu_tas+
     13 root      20   0       0      0      0 S   0.0   0.0   0:00.16 ksoftir+

+-------------------------------------+
Top CPU Process Using ps command
+-------------------------------------+
%CPU     PID USER     COMMAND
 4.6    1306 zjy      /usr/bin/gnome-shell
 2.3    5893 zjy      /usr/bin/gedit --gapplication-service
 0.1     675 root     /usr/bin/vmtoolsd
 0.1    6659 root     [kworker/1:1-events]
 0.1     633 systemd+ /lib/systemd/systemd-oomd
 0.1    2342 zjy      /usr/libexec/gnome-terminal-server
 0.1    1680 zjy      /usr/bin/vmtoolsd -n vmusr --blockFd 3 --uinputFd 4
 0.0       9 root     [kworker/0:1H-events_highpri]
 0.0      99 root     [irq/27-pciehp]