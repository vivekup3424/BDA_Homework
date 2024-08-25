Here is the properly formatted version of your instructions:

# Hadoop Setup Instructions

## Basic Introduction to Hadoop
The Apache Hadoop software library is a framework that allows for the
distributed processing of large data sets across clusters of computers
using simple programming models. It is designed to scale up from 
single servers to thousands of machines, each offering local
computation and storage. Rather than rely on hardware to deliver 
high-availability, the library itself is designed to detect and
handle failures at the application layer, so delivering a 
highly-available service on top of a cluster of computers, 
each of which may be prone to failures.

## 1. Create a New User on the Linux Machine

```bash
sudo adduser hadoop # I have provided the password "hadoop"
```

You can leave the rest of the user data empty. Simply skip over the 
fields by pressing `Enter` continuously.

## 2. Log in as the Hadoop User

```bash
su - hadoop
```

### `su (switch user)`
The `-`, `-l`, or `--login` options start the shell as a login shell with 
an environment similar to a real login:

- Clears all environment variables except `TERM` and variables specified
by `--whitelist-environment`.
- Initializes the environment variables `HOME`, `SHELL`, `USER`, `LOGNAME`, and `PATH`.
- Changes to the target user’s home directory.
- Sets `argv[0]` of the shell to `'-'` to make the shell a login shell.

## 3. Single Node setup instruction for mongodb
- https://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-common/SingleCluster.html

```bash
    wget https://dlcdn.apache.org/hadoop/common/hadoop-3.4.0/hadoop-3.4.0.tar.gz
    tar -xzf hadoop-3.4.0.tar.gz 
    cd ./hadoop-3.4.0/
```
## 4. Setting up system configurations and environment variables


