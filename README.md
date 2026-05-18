# Linux-File-IO-Systems-locking
Ex07-Linux File-IO Systems-locking
# AIM:
To Write a C program that illustrates files copying and locking

# DESIGN STEPS:

### Step 1:

Navigate to any Linux environment installed on the system or installed inside a virtual environment like virtual box/vmware or online linux JSLinux (https://bellard.org/jslinux/vm.html?url=alpine-x86.cfg&mem=192) or docker.

### Step 2:

Write the C Program using Linux IO Systems locking

### Step 3:

Execute the C Program for the desired output. 

# PROGRAM:

## 1.To Write a C program that illustrates files copying 
```
#include <stdio.h>
#include <fcntl.h>
#include <unistd.h>

int main()
{
    int source, dest, n;
    char buffer[100];

    source = open("source.txt", O_RDONLY);

    if(source < 0)
    {
        printf("Source file cannot be opened\n");
        return 1;
    }

    dest = open("destination.txt", O_WRONLY | O_CREAT, 0644);

    if(dest < 0)
    {
        printf("Destination file cannot be created\n");
        return 1;
    }

    while((n = read(source, buffer, sizeof(buffer))) > 0)
    {
        write(dest, buffer, n);
    }

    close(source);
    close(dest);

    printf("File copied successfully\n");

    return 0;
}
```






## 2.To Write a C program that illustrates files locking

```
#include <stdio.h>
#include <unistd.h>
#include <fcntl.h>

int main()
{
    int fd;
    struct flock lock;

    fd = open("sample.txt", O_RDWR);

    if(fd < 0)
    {
        printf("File cannot be opened\n");
        return 1;
    }

    lock.l_type = F_WRLCK;
    lock.l_whence = SEEK_SET;
    lock.l_start = 0;
    lock.l_len = 0;

    printf("Applying write lock...\n");

    fcntl(fd, F_SETLK, &lock);

    printf("File locked\n");
    printf("Press Enter to unlock file\n");

    getchar();

    lock.l_type = F_UNLCK;

    fcntl(fd, F_SETLK, &lock);

    printf("File unlocked\n");

    close(fd);

    return 0;
}
```


## OUTPUT


<img width="655" height="466" alt="Screenshot 2026-05-18 110054" src="https://github.com/user-attachments/assets/ad9c269f-f660-4174-90fd-6af5e0197711" />
<img width="417" height="387" alt="Screenshot 2026-05-18 110238" src="https://github.com/user-attachments/assets/2461ffb4-c0ca-4f70-84c2-70b6577258dc" />




# RESULT:
The programs are executed successfully.
