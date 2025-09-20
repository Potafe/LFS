## Adding the LFS User 

- When logged in as user root, making a single mistake can damage or destroy a system. 

- Therefore, the packages in the next two chapters are built as an unprivileged user. 

- We will create a new user called lfs as a member of a new group (also named lfs) and run commands as lfs during the installation process. 

- As root, issue the following commands to add the new user: 

    ```
    groupadd lfs
    useradd -s /bin/bash -g lfs -m -k /dev/null lfs
    ```

    This is what the command line options mean:

    - -s /bin/bash: This makes bash the default shell for user lfs.
    
    - -g lfs: This option adds user lfs to group lfs.
    
    - -m: This creates a home directory for lfs.
    
    - -k /dev/null: This parameter prevents possible copying of files from a skeleton directory (the default is /etc/skel) by changing the input location to the special null device.
    
    - lfs: This is the name of the new user.

- Grant lfs full access to all the directories under $LFS by making lfs the owner: 

    ```
    chown -v lfs $LFS/{usr{,/*},var,etc,tools}
    case $(uname -m) in
        x86_64) chown -v lfs $LFS/lib64 ;;
    esac
    ```

- Next, start a shell running as user lfs. This can be done by logging in as lfs on a virtual console, or with the following substitute/switch user command: 

    ```
    su - lfs
    ```