FROM centos:7

RUN yum -y install openssh-server

RUN useradd centos7 && \
    
    # set password
    echo "12345" | passwd remote_user  --stdin && \   
    
    mkdir /home/centos7/.ssh && \    
    # chmod 700 (chmod a+rwx,g-rwx,o-rwx) sets permissions so that, (U)ser / owner can read, can write and can execute. (G)roup can't read, can't write and can't execute. (O)thers can't read, can't write and can't execute.
    chmod 700 /home/centos7/.ssh

# ssh-keygen -f remote-key  --> copy the public key to a directory on container
COPY remote-key.pub /home/censot7/.ssh/authorized_keys

# owner : remote_user, group : remote_user by default   recusively
# RUN chown remote_user:remote_user   -R /home/remote_user/.ssh/ && \
#     chmod 600 /home/remote_user/.ssh/authorized_keys

# To apply ownership recursively on all files and directories under a given directory use -R option
RUN chown centos7:centos7   -R /home/centos7 && \
    chmod 400 /home/centos7/.ssh/authorized_keys

# The program is usually located at /usr/sbin/sshd
# RUN /usr/sbin/sshd-keygen to RUN ssh
# for centos 8, command underneath
# -A : generate the host keys with the default key file path, an empty passphrase, default bits for the key type, and default comment. If -f has also been specified, its argument is used as a prefix to the default path for the resulting host key files.
RUN ssh-keygen -A

# -D
# to start the ssh service, which command the container needs to execute
CMD /usr/sbin/sshd -D
