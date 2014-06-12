---
layout: post
title: "shell 自动交互expect"
description: ""
category: 
tags: []
---
{% include JB/setup %}

#example
    #!/usr/bin/expect
    set timeout -1
    spawn sudo ./Linux-agent/installer.sh 
    expect "Next"
    send "n\r"
    expect "Agreement"
    send "a\r"
    expect "Install" 
    send "i\r" 
    exec sleep 10
    expect "Finish"
    send "f\r" 
    

    ps:sudo apt-get install expect (类似bash)
