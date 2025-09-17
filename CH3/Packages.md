## Package Installation

1. Downloaded packages and patches will need to be stored somewhere that is conveniently available throughout the entire build. 

    * A working directory is also required to unpack the sources and build them. 

    * $LFS/sources can be used both as the place to store the tarballs and patches and as a working directory. 

    * By using this directory, the required elements will be located on the LFS partition and will be available during all stages of the building process.

    * To create this directory, execute the following command, as user root, before starting the download session:

        ```
        mkdir -v $LFS/sources
        ```

2. Make this directory writable and sticky. “Sticky” means that even if multiple users have write permission on a directory, only the owner of a file can delete the file within a sticky directory. 

    * The following command will enable the write and sticky modes:

        ```
        chmod -v a+wt $LFS/sources
        ```

3. The necessary packages and patches to build LFS are given (wget-list-sysv):

    * To download all of the packages and patches by using wget-list-sysv as an input to the wget command, use:

        ```
        wget --input-file=wget-list-sysv --continue --directory-prefix=$LFS/sources
        ```

4. Additionally, there is a separate file, md5sums, which can be used to verify that all the correct packages are available before proceeding. 
    
    * Place that file in $LFS/sources and run:

        ```
        pushd $LFS/sources
            md5sum -c md5sums
        popd
        ```

    * This check can be used after retrieving the needed files with any of the methods listed above.

5. If the packages and patches are downloaded as a non-root user, these files will be owned by the user. The file system records the owner by its UID, and the UID of a normal user in the host distro is not assigned in LFS. So the files will be left owned by an unnamed UID in the final LFS system. If you won't assign the same UID for your user in the LFS system, change the owners of these files to root now to avoid this issue:
    
    ```
    chown root:root $LFS/sources/*
    ```