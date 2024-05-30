# cse-sshfs-code-fix
Simple solution to resolve "Invalid argument" running the cmd "code" in mounted file.

# Problem
For some people, using the command "code" while SSH-FS from a linux environtment to Cse server results in an error that experience "Invalied Argument" when running code in mounted environment. According to Abiram (here)[https://abiram.me/cse-sshfs], this is a bug and we need to run "code" outside of the mounted environment. 

# Solution 
I'm reusing Abiram's solution which is to access "code" outside the mounted environment and return to the directory.

In your ~/.bashrc script, which can be accessed by 
``` code ~/.bashrc ```

At the end of the line add the following lines

```
function code() {
    val="$PWD"
    file="$1"

    # Change to the home directory and open the file in VS Code
    cd ~ && code "$val/$file"
    
    # Change back to the original directory
    cd "$val"
}
```
