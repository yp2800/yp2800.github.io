---
layout: post
title: "debian 6 64位安装HP Loadrunner Linux agent"
description: ""
category: shell 
tags: []
---
{% include JB/setup %}
    
    将文件　Linux-agent.tar放到当前的~目录
    安装csh,rpm及32位库文件
    sudo apt-get udpate;apt-get install -y rpm ia32-libs csh
    
    添加　higkoo用户
    sudo useradd -g 0 -s /bin/csh higkoo;sudo mkdir -p /home/higkoo;sudo chown higkoo /home/higkoo
    
    安装Linux-agent
    tar xvf Linux-agent.tar;sudo ./Linux-agent/installer.sh
    环境变量配置
    sudo bash -c ' cat /opt/HP/HP_LoadGenerator/env.csh > /etc/.login;cat /opt/HP/HP_LoadGenerator/env.csh > ~higkoo/.cshrc;touch ~root/.rhosts /home/higkoo/.rhosts'
    
    测试
    sudo su - higkoo
    cd /opt/HP/HP_LoadGenerator/bin/; ./verify_generator;./m_daemon_setup start       ##有进程号则为启动成功
