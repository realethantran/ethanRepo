---
toc: True
comments: True
layout: post
title: Linux Install & Version Check
description: Check for tool installations and versions
type: hacks
courses: {'csa': {'week': 1}}
---

```bash
# check for Python3 version
if command -v python3 &>/dev/null; then
    echo "Python3 is installed"
    python3 --version
else
    echo "Python3 is not installed"
fi

# check for Jupyter version
if command -v jupyter &>/dev/null; then
    echo "Jupyter is installed"
    jupyter --version
else
    echo "Jupyter is not installed"
fi

# check for Node.js (JavaScript) version
if command -v node &>/dev/null; then
    echo "JavaScript is installed"
    node -v
else
    echo "JavaScript is not installed"
fi

# check for Java version
if command -v java &>/dev/null; then
    echo "Java is installed"
    java -version
else
    echo "Java is not installed"
fi

# check for Docker version
if command -v docker &>/dev/null; then
    echo "Docker is installed"
    docker --version
else
    echo "Docker is not installed"
fi

```

    Python3 is installed
    Python 3.9.12
    Jupyter is installed
    Selected Jupyter core packages...
    IPython          : 8.2.0
    ipykernel        : 6.9.1
    ipywidgets       : 7.6.5
    jupyter_client   : 6.1.12
    jupyter_core     : 4.9.2
    jupyter_server   : 1.13.5
    jupyterlab       : 3.3.2
    nbclient         : 0.5.13
    nbconvert        : 6.4.4
    nbformat         : 5.3.0
    notebook         : 6.4.8
    qtconsole        : 5.3.0
    traitlets        : 5.1.1
    JavaScript is installed
    v6.11.2
    Java is installed
    openjdk version "11.0.20" 2023-07-18
    OpenJDK Runtime Environment (build 11.0.20+8-post-Ubuntu-1ubuntu120.04)
    OpenJDK 64-Bit Server VM (build 11.0.20+8-post-Ubuntu-1ubuntu120.04, mixed mode, sharing)
    Docker is installed
    Docker version 24.0.5, build ced0996

