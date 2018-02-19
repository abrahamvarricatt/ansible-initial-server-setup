# Initial server setup

When I rent a server online, an IP with username/password credentails for the
root account are given to me. Most of the time, I find myself running the same
initialization steps over and over again. This ansible playbook is going to be
my short-cut to getting the basic initialization done quickly.

At the time of writing,

```
ansible 2.4.3.0
```

This playbook is specific to Ubuntu >= 16.04

Following instructions have been tested on an Ubuntu LTS system.

## Step 1: Generate SSH private/public key pair

Move to `roles/ansible-user-account/files` directory and run the following command
to generate the SSH key pair. Enter `ansible` when it asks for a name. That will
generate 2 files - `ansible` and `ansible.pub` in the current folder.

```shell
$ cd roles/ansible-user-account/files
$ ssh-keygen -t rsa -b 2048 -v
Generating public/private rsa key pair.
Enter file in which to save the key (PATH_REMOVED): ansible
...
```

Rename `ansible` to `ansible.pem`,

```shell
$ mv ansible ansible.pem
```

## Step 2: Initialize the server

Update `inventory.ini` with server details. Then you can run the following,

```shell
$ ansible-playbook -i inventory.ini initial-setup.yml --extra-vars "new_password=abcd"
```
