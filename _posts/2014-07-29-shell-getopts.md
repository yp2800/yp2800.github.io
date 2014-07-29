---
layout: post
title: "shell getopts选项传参"
description: ""
category: shell
tags: []
---
{% include JB/setup %}

####getopts sample example 

    #!/bin/bash
    STATE_OK=0
    STATE_WARNING=1
    STATE_CRITICAL=2
    STATE_UNKNOWN=3
    process=
    lock=
    
    Usage()
    {
        echo "check_cron.sh v1.0"
            echo ""
            echo "Usage:"
            echo "check_cron.sh -p process_name -l lock_name"
            echo -e "\nfor example:\ncheck_cron.sh -p apache -l .lock.apache"
            echo ""
            echo "check the cron running state"
            echo ""
            echo "Copyright (C) 2014 ChuanZ and Cursor and Pengy Modify "
            exit
    }
    
    [ $# -eq 0 ] && usage
    
    #option_string以冒号开头表示屏蔽脚本的系统提示错误，自己处理错误提示。
    #后面接合法的单字母选项，选项后若有冒号，则表示该选项必须接具体的参数
    while getopts :p:l: OPTION
    do
        case $OPTION in
            p)
                process=$OPTARG
                ;;
            l)
                lock=$OPTARG
                ;;
            \?)                       #如果出现错误，则解析为?
                Usage
                ;;
        esac
    done
    
    lock_file=/home/XXXX/XX/xxX/../../logs//$lock
    
    ps -ef |grep $process |grep -v grep |grep -v $0 > /dev/null 2>&1
    run_status=$?
    if [ $run_status -ne 0 ] && [ -f $lock_file ];then
        SERVICEOUTPUT="cron script $process run exception, process don't run but lock_file is exist"
        SERVICESTAT=$STATE_WARNING
        echo $SERVICEOUTPUT
        exit $SERVICESTAT
    else
        SERVICEOUTPUT="cron script run normal"
        SERVICESTAT=$STATE_OK
        echo $SERVICEOUTPUT
        exit $SERVICESTAT
    fi

