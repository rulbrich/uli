#!/bin/bash

# Das ist ein einfaches Template für einen check_mk Local Check
# auf bash-Basis. 
# Quelle: http://mathias-kettner.de/checkmk_localchecks.html

DIRS="/var/log /tmp"

for dir in $DIRS
do
    count=$(ls $dir | wc --lines)
    if [ $count -lt 50 ] ; then
        status=0
        statustxt=OK
    elif [ $count -lt 100 ] ; then
        status=1
        statustxt=WARNING
    else
        status=2
        statustxt=CRITICAL
    fi
    echo "$status Filecount_$dir count=$count;50;100;0; $statustxt - $count files in $dir"
done
