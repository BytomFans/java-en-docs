---
id: build
title: Build Bytom
sidebar_label: 搭建节点
---

## Building from source

## Ubuntu

### 1.1 Install dependency

    sudo apt-get update
    sudo apt-get install build-essential git unzip wget vim

### 1.2 Download and extract the node

    wget https://mirrors.tuna.tsinghua.edu.cn/osdn/bytom/70718/bytom-1.0.8-linux.zip
    unzip bytom-1.0.8-linux.zip
    chmod +777 ./bytomd

### 1.3 Run node

    ./bytomd init --chain_id mainnet
    ./bytomd node --simd.enable

## windows

### 1.1 Install dependency

#### Install MinGW
Link：https://nuwen.net/mingw.html

Download link：https://nuwen.net/files/mingw/mingw-16.1.exe

#### Install Golang

Link：https://golang.org/

Download link：https://studygolang.com/dl/golang/go1.12.windows-amd64.msi

#### Install Git

Link：https://git-scm.com/

Download link：https://git-scm.com/download/win

### 1.2 Download and extract the node

Download link：https://mirrors.tuna.tsinghua.edu.cn/osdn/bytom/70718/bytom-1.0.8-linux.zipUnzip Download the zip file and modify the right-click folder permissions to read and write.

### 1.3 Run node

    ./bytomd.exe init --chain_id mainnet
    ./bytomd.exe node --simd.enable

## In Docker

Ensure your Docker version is 17.05 or higher. 

    docker pull bytom/bytom:latest

### Init node

    docker run -v ~/Bytom:/root/.bytom bytom/bytom:latest bytomd init --chain_id mainnet

### Run node

    docker run -d -p 46657:46657 -v ~/Bytom:/root/.bytom bytom/bytom:latest 

## Mac

Installing with Homebrew.

    brew install bytom