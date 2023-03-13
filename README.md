# Nexus-Installation
guide to install Nexus


# Pre req
* Any OS 
* t2 medium (4gb RAM)
* port: 8081
* java 1.8+


# Step 0 - hostname

```shell
$ sudo hostname Nexus
```

# Step 1 - create nexus user / make admin & su
useradd nexus

```shell
$ sudo echo "nexus ALL=(ALL) NOPASSWD:ALL"|
$ sudo tee /etc/sudoers.d/nexus 
$ su - nexus
```

# Step 2 - install wget & unzip

```shell
$ cd /opt => go to opt dir
$ yum install wget unzip -y
```

# Step 3 - install java

```shell
$ sudo yum install java-11-openjdk-devel
$ java-1.8.0-openjdk-devel -y
```

# Step 4 - download Nexus 3.15

```shell
$ sudo wget http://download.sonatype.com/nexus/3/
$ nexus-3.15.2-01-unix.tar.gz
```

# Step 5 - untar / unzip file

```shell
$ sudo tar -zxvf nexus-3.15.2-01-unix.tar.gz
```

# Step 6 - rename

```shell
$ sudo rm -rf nexus-3.15.2-01-unix.tar.gz
$ sudo mv /opt/nexus-3.15.2-01/opt/nexus
```

# Step 7 - persmissions
* chnage group & owner of dir to sonar & son
* 775 permission

```shell
$ sudo chown -R nexus:nexus /opt/nexus
$ sudo chown -R nexus:nexus /opt/sonatype-work
$ sudo chmod -R 775 /opt/nexus
$ sudo chmod -R 775 /opt/sonatype-work
```

# Step 8 - set "run as user" ="nexus" user

```shell
$ vi /opt/nexus/bin/nexus.rc
run_as_user="nexus"
allows "nexus" user to use nexus
```

# Configure nexus to run as service

```shell
$ sudo In -s /opt/nexus/bin/nexus/etc/init.d/nexus (absolute path)
```

# Enable and start the nexus services

```shell
$ sudo systemctl enable nexus (1st - maybe cuz 3rd party??)
$ sudo systemctl start nexus
$ sudo systemctl status nexus
```

# Change port

```shell
NHD/etc/nexus-default.properties

application-port=<new port>
```
