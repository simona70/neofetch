## Description

## Features

In my .bashrc I output:

Uptime:   12:50:36 up 8 min,  1 user,  load average: 1,72, 1,10, 0,62   
Term Cols:  256 . CPU govr:  intel_pstate  /  powersave . CPU sched:  CFS 
I/O sched: nvme0n1> none  sda> mq-deadline  sdb> mq-deadline  sdc> bfq  sdd> mq-deadline  sde> bfq  sdf> bfq 

with comands

    echo -e -n "Term Cols: \e[1;39;41m" `   tput colors   ` "\e[0m."

    [[ -r /usr/bin/cpupower ]] && echo -e -n " CPU govr: \e[1;39;41m"   `  cpupower frequency-info | grep "driver:" | awk '{ print $2 }'     `  "\e[0m / \e[1;39;41m"   `     cpupower frequency-info | grep "Il gestore" | awk '{ print $3 }'  | sed s/\"//g     `   "\e[0m."

    echo -e -n " "
    #echo -e -n "\n"

    echo -e -n "CPU sched: \e[1;39;41m"    `     dmesg | grep -i "CPU scheduler"  |  awk '{ print $3 " " $6 " " $9 }'      `   "\e[0m"
    echo -e -n "\n"

    #cat /sys/block/sd*/queue/scheduler
    #echo -e -n "\n"
    echo -e -n "I/O sched: "
    if [[ -d /sys/block/nvme0n1 ]] ; then
      for device in /sys/block/nvme*/queue/scheduler ; do
      echo -e -n "nvme${device:15:3}>\e[1;39;41m"   `      cat /sys/block/nvme${device:15:4}/queue/scheduler | cut -d "[" -f2 | cut -d "]" -f1     `   "\e[0m "
      done
    fi
    if [[ -d /sys/block/sda ]] ; then
      for device in /sys/block/sd*/queue/scheduler ; do
      echo -e -n "sd${device:13:1}>\e[1;39;41m"   `      cat /sys/block/sd${device:13:1}/queue/scheduler | cut -d "[" -f2 | cut -d "]" -f1     `   "\e[0m "
      done
    fi
    echo -e -n "\n "


## Issues

## TODO
