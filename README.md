# CMPSC 472 Project 1
# Project Description
This project involves developing a program to read through seven large files using multiple processes and multiple threads. Each process is assigned to read one file, and each thread is assigned to a specific portion of the file to read through concurrently with other threads. The goal is to identify, count, and display the 50 most-used words with each word displaying its frequency. 

Note: For this project, I could not get the program to accurately find the top 50 most used words throughout all the files. Instead of doing this, I created an array to store 50 of the most commonly used words in the English language. From here, each process read in one word at a time and compared to all 50 words in the array. If the word matched one of the 50 words in that array, I incremented a counter that keeps track of that word's frequency. In other words, I hardcoded an array containing 50 common words, and these words may not actually be the 50 most common words used throughout all seven files.

In the program where no multi-threading is used, the program starts the timer to measure how much time the entire program execution takes. Then, multiple processes are created using the fork() function. Seven fork() calls are made as seven child processes are needed to read through each of the seven files. My implementation has the children processes created in a for-loop where the loop runs a total of seven times, and within each iteration the process ID is checked. If the process ID is a negative value, an error statement is printed as the child process failed to be created. Otherwise, if the process ID is equal to 0, then this is the child process. The child process then creates a file pointer to open a specific file. All the files are stored within an array, so each iteration of the for-loop specifies a different file for each new process. If the file pointer fails to open the file, an error statement gets printed out. After a file pointer is successfully created, a while-loop uses the fgets() function to read in each string from the file. Next, the string is tokenized using the strtok() function to remove spaces, newline and tab characters, and puntuation. This tokenized string is an array of all the words within that line that was just read in from the file. To iterate through all words, a while-loop is used. Then within, this while-loop, a for-loop is used to compare the token to each of the 50 hardcoded string values I entered. If a match was found, a frequency-counter was updated by one. After reading in all lines of the file, the fclose() function is used to free up memory space. After the fclose() call, the word frequencies are sent from the child pipe to the parent pipe. The parent collects the data from the child processes and accumulates the values. After each child is done sending the data through the pipe, the child terminates and returns its status to the parent process. The parent process uses a while-loop to wait for all children processes to terminate. After this, the program stops the timer and evaluates how long the program execution took in microseconds. After this, the getrusage() function retrieves information from the terminated child processes. The metrics are displayed down below, along with the 50 most commonly used words and their corresponding frequencies.

# Structure of Code
![image](/fork_diagram.jpg)
**Explanation**: The parent process calls fork() to create a child process, and the return value of the fork() function call is a process ID. 

![image](/thread_diagram.jpg)

![image](/pipe_diagram.jpg)

# Instructions on How to Use the Program


# Verification of Code Functionality


# Discussion of Findings
