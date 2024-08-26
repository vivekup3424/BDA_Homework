Here's the full documentation with the necessary SSH key generation steps added:

---

# Hadoop Setup Instructions

## Basic Introduction to Hadoop
The Apache Hadoop software library is a framework that allows for the distributed processing of large data sets across clusters of computers using simple programming models. It is designed to scale up from single servers to thousands of machines, each offering local computation and storage. Rather than rely on hardware to deliver high-availability, the library itself is designed to detect and handle failures at the application layer, delivering a highly-available service on top of a cluster of computers, each of which may be prone to failures.

## 1. Create a New User on the Linux Machine

```bash
sudo adduser hadoop # I have provided the password "hadoop"
```

You can leave the rest of the user data empty. Simply skip over the fields by pressing `Enter` continuously.

## 2. Log in as the Hadoop User

```bash
su - hadoop
```

### `su (switch user)`
The `-`, `-l`, or `--login` options start the shell as a login shell with an environment similar to a real login:

- Clears all environment variables except `TERM` and variables specified by `--whitelist-environment`.
- Initializes the environment variables `HOME`, `SHELL`, `USER`, `LOGNAME`, and `PATH`.
- Changes to the target user’s home directory.
- Sets `argv[0]` of the shell to `'-'` to make the shell a login shell.

## 3. Single Node Setup Instruction for Hadoop
Follow the official Apache Hadoop single-node setup guide:

[Single Node Setup Guide](https://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-common/SingleCluster.html)

Alternatively, you can use the following commands to download and extract Hadoop:

```bash
wget https://dlcdn.apache.org/hadoop/common/hadoop-3.4.0/hadoop-3.4.0.tar.gz
tar -xzf hadoop-3.4.0.tar.gz 
cd ./hadoop-3.4.0/
```

## 4. Setting up System Configurations and Environment Variables

### Adding SSH and OpenSSH-Server

The error message `ssh: connect to host localhost port 22: Connection refused` typically occurs when the SSH server is not running on the localhost, or it is configured to listen on a different port.

Here’s how you can troubleshoot this issue:

1. **Check if SSH Server is Installed:**
   Ensure that the SSH server (`sshd`) is installed on your machine. On Ubuntu or Debian-based systems, you can check this by running:
   ```bash
   sudo systemctl status ssh
   ```
   If it’s not installed, you can install it using:
   ```bash
   sudo apt-get install openssh-server
   ```

2. **Start the SSH Service:**
   If SSH is installed but not running, start it with:
   ```bash
   sudo systemctl start ssh
   ```

3. **Check SSH Configuration:**
   Make sure the SSH server is configured to listen on port 22. You can check this in the SSH configuration file `/etc/ssh/sshd_config`:
   ```bash
   sudo nano /etc/ssh/sshd_config
   ```
   Look for the line that starts with `Port`. If it's set to a different port, either change it to 22 or specify the correct port when connecting via SSH:
   ```bash
   ssh -p <port_number> hadoop@localhost # make sure to use port 22
   ```

4. **Restart SSH Service:**
   After making any changes, restart the SSH service to apply them:
   ```bash
   sudo systemctl restart ssh
   ```

5. **Verify SSH is Running:**
   To confirm SSH is running and listening on port 22, you can use:
   ```bash
   sudo netstat -tnlp | grep ssh
   ```

6. **SSH into localhost:**

   ```bash
   ssh hadoop@localhost
   ```

## 5. Generating SSH Keys for Passwordless Authentication

To enable passwordless SSH login for the Hadoop user, you need to generate an SSH key pair.

1. **Generate SSH Key Pair:**
   ```bash
   ssh-keygen -t rsa
   ```

   - **Enter file in which to save the key**: Press `Enter` to save the key to the default location (`/home/hadoop/.ssh/id_rsa`).
   - **Enter passphrase**: Leave this blank and press `Enter` for no passphrase.
   - **Enter same passphrase again**: Press `Enter`.

   Output:
   ```
   Your identification has been saved in /home/hadoop/.ssh/id_rsa
   Your public key has been saved in /home/hadoop/.ssh/id_rsa.pub
   The key fingerprint is:
   SHA256:9sUCIBHgVtR1BZ76KA69QGnJRPHEHU/x9pLLqcF+BeM hadoop@vivekup3424-Nitro-ANV15-51
   The key's randomart image is:
   +---[RSA 3072]----+
   |  .oO*ooo.=+.    |
   | . o +o..= o     |
   |  o . . . + o    |
   | . o o   o ooo   |
   |    *   S ..=o.  |
   |   o . . = +E+.  |
   |    o o . = +.   |
   |     + o . o.    |
   |      o   o.     |
   +----[SHA256]-----+
   ```

2. **Add the SSH Key to the Authorized Keys:**
   ```bash
   cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys
   chmod 600 ~/.ssh/authorized_keys
   ```

3. **Test the SSH Connection:**
   Test the connection by SSHing into localhost:
   ```bash
   ssh hadoop@localhost
   ```
   If everything is set up correctly, it should not ask for a password.


- Hadoop Single Node Setup configuation steps
```bash
cd hadoop-3.4.0/etc/hadoop
```

`vim core-site.xml`
```xml
<?xml version="1.0" encoding="UTF-8"?>
<?xml-stylesheet type="text/xsl" href="configuration.xsl"?>
<configuration>
        <property>
                <name>fs.defaultFS</name>
                <value>hdfs://localhost:9000</value>
        </property>
</configuration>
```


