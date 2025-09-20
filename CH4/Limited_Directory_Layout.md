## Creating a Limited Directory Layout in the LFS Filesystem 

1. In this section, we begin populating the LFS filesystem with the pieces that will constitute the final Linux system. 
    
    * The first step is to create a limited directory hierarchy, so that the programs compiled in Chapter 6 (as well as glibc and libstdc++ in Chapter 5) can be installed in their final location. 
    
    * We do this so those temporary programs will be overwritten when the final versions are built in Chapter 8. 

2. Create the required directory layout by issuing the following commands as root: 

    ```
    mkdir -pv $LFS/{etc,var} $LFS/usr/{bin,lib,sbin}

    for i in bin lib sbin; do
        ln -sv usr/$i $LFS/$i
    done

    case $(uname -m) in
    x86_64) mkdir -pv $LFS/lib64 ;;
    esac
    ```

3. Programs in Chapter 6 will be compiled with a cross-compiler. 

    * This cross-compiler will be installed in a special directory, to separate it from the other programs. 
    
    * Still acting as root, create that directory with this command: 

        ```
        mkdir -pv $LFS/tools
        ```