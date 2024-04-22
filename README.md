# holbertonschool-shell
Shell Project:

The functions that we use for this project are:

Getline: We use Getline to get the imput writed by the user.

How it works: 

Initialization: When getline is called, it is passed three arguments: a pointer to a pointer to char (which is where the read line of text will be stored), a pointer to a size (which represents the size of the buffer), and an object FILE (representing the input stream).

Memory allocation: If the buffer pointed to by the first argument is NULL or if the buffer is not large enough to hold the line of text, getline automatically allocates (or reallocates) memory for the buffer. This means you don't have to worry about allocating memory for the string before calling getline.
Reading characters: getline starts reading characters from the input stream one by one. Each character is added to the end of the buffer.

End-of-line detection: getline continues reading characters until it encounters a newline character ('\n') or until the end of the file is reached. When one of these characters is encountered, getline stops reading.

`strtok`: We use `strtok` to separete the imput get by get line so execve can process it and understand wich part is the program to execute and the arguments.

How it works:

1. `strtok` maintains an **internal state**¹. This means that it keeps an internal reference to the last string it parsed⁴.
2. In the first call to `strtok`, you pass the string you want to tokenize and the delimiters as arguments. `strtok` looks for the first delimiter in the string and replaces it with a null character (`\0`), essentially splitting the string in two¹.
3. `strtok` returns a pointer to the start of the string⁵. This pointer points to the first "word" or token in the string².
4. In subsequent calls to `strtok`, you pass `NULL` as the first argument instead of the string. This tells `strtok` to continue tokenizing the same string from where it last left off¹⁵.
5. `strtok` continues this process, looking for the next delimiter, replacing it with a `\0`, and returning a pointer to the next token¹.
6. When there are no more tokens left to retrieve, `strtok` returns `NULL`²⁵.

`execve`: we use execve to start a program in the current proces so the commands can work in our shell using the current command.

How it works: 1. **Initialization**: When `execve` is called, three arguments are passed: a pointer to a file name (which is the new program to execute), a pointer to an array of pointers (which are the arguments to the new program) and a pointer to an array of pointers (which are the environment variables for the new program)¹.

2. **Process replacement**: `execve` asks the operating system to replace the current process with the new specified program¹. This involves loading the new program into memory and starting its execution¹.

3. **Process ID Preservation**: Although the program is replaced, the process ID (PID) remains the same¹. This means that from the operating system's point of view, it is still the same process, but it is now running a different program¹.

4. **Removing allocated memory**: Before calling `execve`, memory is allocated to hold the arguments and environment variables of the new program from the memory mapping of the current process³. But after `execve`, all text, data, stack segment of the current process are overwritten with the new program, and all memory mappings of the old process are not preserved (including memory for arguments and environment variables passed )³.

5. **Return**: If `execve` succeeds, it returns nothing because the current process has been completely replaced¹. If there is an error (for example, the program file is not found), `execve` returns `-1` and sets the `errno` variable to indicate the error¹.
