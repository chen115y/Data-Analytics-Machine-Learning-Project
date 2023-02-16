
# Environmental Setup

## Prerequisite Installation & Configuration On Linux, Python, Spark and MySQL

### Hardware Environment
* 8 GB Memory
* 2.60GHz 2 Cores CPU
* 250 GB Hard Disk

### Install Linux Ubuntu

* [Ubuntu Linux 18.04 LTS](https://www.ubuntu.com/download/desktop)
* [Windows Subsystem for Linux - Ubuntu](https://docs.microsoft.com/en-us/windows/wsl/install-win10)

### Install basic packages

```shell
    sudo apt update
    sudo apt install tmux
    sudo apt install wget curl
    sudo apt install -y openssh-server
```

### Install Python 3.X
```shell
    # sudo add-apt-repository ppa:jonathonf/python-3.6
    sudo apt update
    sudo apt install python3

    sudo apt install python3-pip python-dev build-essential
    sudo pip3 install --upgrade pip
    sudo pip3 install --upgrade virtualenv
    # install the tool to create python application executables
    sudo pip3 install pyinstaller
```
### Install Spark
```shell
    # check Java version
    java -version
    # install java 8 
    # some applications require java 8 rather than defaul java 9 or 10
    sudo apt update
    sudo apt install openjdk-8-jdk
    # Set the Default Java Version to Java 8
    sudo update-alternatives --config java
    
    output:
    There are 3 choices for the alternative java (providing /usr/bin/java).

    Selection    Path                                            Priority   Status
    ------------------------------------------------------------
    * 0            /usr/lib/jvm/java-11-openjdk-amd64/bin/java      1101      auto mode
      1            /usr/lib/jvm/java-11-openjdk-amd64/bin/java      1101      manual mode
      2            /usr/lib/jvm/java-8-openjdk-amd64/jre/bin/java   1081      manual mode
      3            /usr/lib/jvm/java-8-oracle/jre/bin/java          1081      manual mode
      4            /usr/local/oracle-java-10/jdk-10.0.2/bin/java    1500      manual mode

    Press <enter> to keep the current choice[*], or type selection number: 2


    # download latest spark and untar it
    wget -P /tmp/ http://apache.osuosl.org/spark/spark-2.4.1/spark-2.4.1-bin-hadoop2.7.tgz
    sudo mkdir /usr/local/spark/
    sudo tar xvf /tmp/spark-2.4.1-bin-hadoop2.7.tgz -C /usr/local/spark
    
    # installing pyspark with pip
    sudo pip3 install pyspark
```
### Install Git for Source Version Control
```shell
    sudo apt install git-all
    # or install light version
    sudo apt install git
    git config --global user.email "chen115yaohua@gmail.com"
    git config --global user.name "Ivan Chen"
```
### Install a Hadoop Single Node Cluster
Please following the instructions at [apache.org](https://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-common/SingleCluster.html) to setup a single node hadoop cluster.

### Install VS Code and Pycharm
```shell
    # Virtual Studio Code
    curl -O https://go.microsoft.com/fwlink/?LinkID=760868
    sudo apt update
    sudo dpkg -i <file>.deb
    sudo apt-get install -f
    
    # Pycharm Community Edition
    wget -P /tmp/ https://download.jetbrains.com/python/pycharm-community-2018.2.4.tar.gz
    sudo snap install pycharm-community --classic
    # Or install PyCharm with tar and pycharm.sh
    tar xfz pycharm-*.tar.gz -C /usr/local/pycharm
    cd /usr/local/pycharm/pycharm-*/bin
    sh pycharm.sh
```

### Install MySQL
```shell
    sudo apt update
    sudo apt install mysql-server
    # For fresh installations, runt eh included security script to change some of less secure default options
    sudo mysql_secure_installation
    sudo pip3 pymysql
    sudo pip3 install mysql-connector-python
```
To start, stop, restart and enable MySQL at reboot, use
```shell
    sudo systemctl stop mysql
    sudo systemctl start mysql
    sudo systemctl restart mysql
    sudo systemctl enable mysql
    sudo systemctl status mysql
```
or use
```shell
    sudo service mysql start
    sudo service mysql stop
    sudo service mysql restart
    sudo service mysql status
```
To connect MySQL locally, use
```shell
    sudo mysql -u root -p
```

## Installation & Configuration of Jupyter Notebook

### Install Jupyter Notebook
```shell
    sudo pip3 install jupyter
    sudo chmod 777 ~/.local/share/jupyter/
```
### iPython Data Science and Engineering Tools Installation
```shell
    sudo pip3 install numpy pandas scipy tensorflow pymc3 keras xlrd pyarrow
    sudo pip3 install -U scikit-learn xgboost
    sudo pip3 install pillow
    sudo pip3 install h5py pytables
    # natural language processing
    sudo pip3 install nltk textblob smart_open gensim
    sudo python3 -m textblob.download_corpora
    # parallel processing
    sudo pip3 install dask dask-ml dask-searchcv numba multiprocess ipyparallel distributed joblib
    # visualization
    sudo pip3 install matplotlib seaborn clarify
    # install pytorch for latest python version 3.7
    sudo pip3 install https://download.pytorch.org/whl/cpu/torch-1.0.1.post2-cp37-cp37m-linux_x86_64.whl
    sudo pip3 install torchvision

    # sudo pip3 install optimuspyspark
    sudo pip3 install sqlalchemy
    sudo pip3 install pandas-profiling
    sudo pip3 install spark-df-profiling

    wget -P /tmp/ https://github.com/jgm/pandoc/releases/download/2.5/pandoc-2.5-1-amd64.deb
    sudo dpkg -i /tmp/pandoc-2.5-1-amd64.deb
    sudo apt install -y texlive-xetex
    # for SQL magic function
    sudo pip3 install ipython-sql
    # for R magic function
    sudo pip3 install rpy2 tzlocal
    # for notebook extensions
    sudo pip3 install jupyter_contrib_nbextensions
    sudo pip3 install autopep8
    # install and enable jupyter themes, especially dark one
    # for web scrawler
    sudo pip3 install scrapy beautifulsoup4

    # time Series
    sudo pip3 install pystan statsmodels fbprophet

    # Optional: install jupyter extensions
    sudo pip3 install jupyter_contrib_nbextensions # for python 3
    sudo pip install jupyter_contrib_nbextensions # for python 2 if your ipython jupyter support both 2 & 3
    sudo pip3 install autopep8 # for enable autopep8 extension
```
### Jupyter Notebook Extension Configuration
```shell
    sudo jupyter contrib nbextension install --user
    # grant juypter extension to write data in this json file to load extensions later
    sudo chmod a+rw ~/.jupyter/nbconfig/notebook.json 
```
The eventual installed python packages include: pytz, python-dateutil, numpy, pandas, findspark, h5py, setuptools, kiwisolver, pyparsing,cycler, matplotlib, scipy, seaborn, keras-applications, keras-preprocessing, keras, pillow, pyarrow, multipledispatch, wrapt, deprecated, pyspark, atomicwrites, pluggy, py, more-itertools, pytest, nose, tabulate, ratelimit, ipython, vine, amqp, kombu, requests, pika, pymongo, backoff, itsdangerous, Werkzeug, flask, humanize, future, colorama, h2o-pysparkling-2.3, psutil, fastnumbers, protobuf, markdown, tensorboard, grpcio, termcolor, astor, gast, absl-py, tensorflow, tqdm, optimuspyspark, clarify, sqlalchemy, ipython-sql

### Validating ipython jupyter notebook
For validating if jupyter notebook is working well with SQL, Python and Shell commands, you can run the [Notebook_Validation.ipynb](./jupyter_notes/Notebook_Validation.ipynb) notebook [[pdf]](./jupyter_notes/Notebook_Validation.pdf). It should look like as the following screen shot:
<a><img src="./Capture.PNG" alt="Jupyter Notebook"></a>

# Appendix

The following appendixes may be useful during environmental setup.

## Java 8 Environment Configuration
```shell
    sudo nano /etc/environment
    # add the following line at the end of file
    JAVA_HOME="/usr/lib/jvm/java-8-openjdk-amd64"
    # apply the change
    source /etc/environment
    # verify the JAVA_HOME environment variable
    echo $JAVA_HOME
    output:
    /usr/lib/jvm/java-8-openjdk-amd64
```

## Install Anaconda on Linux for light data science and engineering tools
```shell
    # Step 1: Download Anaconda bash script
    curl -O https://repo.anaconda.com/archive/Anaconda3-5.2.0-Linux-x86_64.sh

    # Step 2: Verify the data integrity of the installer
    sha256sum Anaconda3-5.2.0-Linux-x86_64.sh

    # Step 3: Run the Anaconda script and complete installation process as prompted
    bash Anaconda3-5.2.0-Linux-x86_64.sh

    # Step 4: Activate and test installation
    source ~/.bashrc
    conda list

    # Step 5: Setup Anaconda environments
    conda create --name my_env python=3
    source activate my_env
```

## BASH Configuration
    In the ~/.bashrc file, add 
```bash
    export DISPLAY=localhost:0.0
    alias pycharm="/mnt/c/'Program Files'/JetBrains/'PyCharm Community Edition 2018.2.4'/bin/pycharm64.exe"
    alias jnb="~/.local/bin/jupyter-notebook --no-browser"
    alias vscode="/mnt/c/Users/yaohua.chen/AppData/Local/Programs/'Microsoft VS Code'/Code.exe"
    SPARK_HOME=/usr/local/spark/spark-2.4.0-bin-hadoop2.7
    export SPARK_HOME=$SPARK_HOME
    export PATH=$SPARK_HOME/bin:$PATH
```
    and then use the command
```
    source ~/.bashrc
```
    to activate the config then type the command
```shell
    jupyter-notebook
```
    to start jupyter notebook service. Copy the prompted jupyter URL or use 127.0.0.1:8888 to access web UI.
    Then use 
```shell
    pyspark 
```
    to access spark shell in python and use
```shell
    sh $SPARK_HOME/sbin/start-all.sh
```
    to start the spark service. The web ui will be available at 127.0.1.1:8080 port.

## Vim Configuration    
* Use the [vimrc](./vim/vimrc) in the folder [vim](vim/) to replace `~/.vim/vimrc`

## Install web Scrape tools
```shell
    sudo pip3 install scrapy beautifulsoup4
```

## Install SQL Server 2017 on Ubuntu 16.04 LTS
Note: the Windows Subsystem for Linux for Windows 10 is not supported as an installation target.
```shell
    sudo apt update
    wget -qO- https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
    sudo add-apt-repository "$(wget -qO- https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-2017.list)"
    # Register the Microsoft Ubuntu repository.
    curl https://packages.microsoft.com/config/ubuntu/16.04/prod.list | sudo tee /etc/apt/sources.list.d/msprod.list
    sudo apt install -y mssql-server
    sudo /opt/mssql/bin/mssql-conf setup
    sudo apt update
    sudo apt install mssql-tools unixodbc-dev
    # A cross-platform command-line interface for running Transact-SQL commands.
    sudo apt install mssql-cli # or pip3 install mssql-cli
```
To start, stop, restart and enable SQL Server at reboot, use
```shell
    sudo systemctl stop mssql-server
    sudo systemctl start mssql-server
    sudo systemctl restart mssql-server
    sudo systemctl enable mssql-server
    sudo systemctl status mssql-server
```
or use
```shell
    sudo service mssql-server start
    sudo service mssql-server stop
    sudo service mssql-server restart
    sudo service mssql-server status
```
To connect SQL Server locally, use
```shell
    sqlcmd -S localhost -U SA -p
```
To use mssql-cli, use
```shell
    mssql-cli -S localhost -U sa -d <database>
```

## Install PostgreSQL on Ubuntu 18.04 LTS
Add PostgreSQL repository to Ubuntu 18.04
```shell
    wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo apt-key add -
    sudo sh -c 'echo "deb http://apt.postgresql.org/pub/repos/apt/ $(lsb_release -sc)-pgdg main" > /etc/apt/sources.list.d/PostgreSQL.list'
```
Update and install PostgreSQL and additional utilities and funcitonality
```shell
    sudo apt update
    sudo apt install postgresql postgresql-contrib
    # optional - install postgresql web client phpmyadmin
    sudo apt install pgadmin3
```
After isntalling PostgreSQL, the commands below can be used to stop, start, enable and check its status
```shell
    sudo systemctl start postgresql.service
    sudo systemctl stop postgresql.service
    sudo systemctl enable postgresql.service
    sudo systemctl status postgresql.service
```
or
```shell
    sudo service postgresql start
    sudo service postgresql stop
    sudo update-rc.d postgresql enable
    sudo service postgresql status
```
