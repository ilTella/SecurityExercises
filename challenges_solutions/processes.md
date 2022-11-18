# Processes exercises

## ex 29

```
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <sys/types.h>
#include <sys/wait.h>

void pwncollege(void) {
        pid_t my_pid;
        int status, timeout;

        char **argv = calloc(5, sizeof(char*));
        argv[0] = "challenge_path";

        if ((my_pid = fork()) == 0) {
                execve(argv[0], (char **)argv, NULL);
        }

        timeout = 1000;
        while ((waitpid(my_pid, &status, WNOHANG) == 0)) {
                if (--timeout < 0) {
                        perror("timeout");
                        //return -1;
                }
                sleep(1);
        }

}

int main(void) {
        pwncollege();
        return 0;
}
```

## ex 30

same as 29

# ex 31

same as 29 but with
```
argv[1] = "password";
```