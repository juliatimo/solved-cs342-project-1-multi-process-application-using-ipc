Download Link: https://assignmentchef.com/product/solved-cs342-project-1-multi-process-application-using-ipc
<br>
<strong>Part A)</strong> In this project you will write a multi-process application called <strong>pwc</strong> that will read a set of ascii text files containing words and generate  word frequency information into an output file. The application will create multiple child processes, and processes will communicate using Linux message queues. You will use POSIX message queues.

The program will be invoked as follows:

pwc N f1 f2 … fN  outfile

f1, f2, fN are N input files. The main process will create N  child processes. Each child process will process  another input file. Each input file contains a sequence of words. A line of input file may contain multiple words. A word is just a sequence of non-whitespace characters between two whitespace characters. A whitespace  character can be space, tab, or newline character (you can use fscanf(“%s”) to read a word). The maximum size of a word can be  1024 characters including the NULL character at the end. For each child process, the parent will also create a message queue, so that the child process will be able to send information to the parent process. The message queues should better be created earlier than the child processes in the parent.




Each child process will read and process its own input file and will create a sorted linked list distinct words in memory (you can use insertion sort) in ascending order. For each distinct word, the list will have a node that will keep the word count as well, besides the word itself. Since the string-length of the word,  can be anything between 1 and 1023, you should dynamically allocate memory for a node of the list using malloc(). After reading the input file completely and generating the list meanwhile, the child process will start sending the words in ascending  sorted order to the parent process using the respective message queue. Two words can be compared using the strcmp() function.




The parent process will receive the incoming words and their counts from children as messages, one by one in sorted order, and will write them into  the output file. Note that the parent process will not sort again. It should retrieve the words from children in sorted order. This can be achieved by first receiving one word from each child (through the respective message queues), and then finding the word that is the first in ascending order, and then writing it out to the output file. Then the parent can receive another word from the child whose word has just been written out, and compare it  again with the already received words, find the word that is first in ascending order, and write it out. If the words received form multiple messages queues are the same, their counts will be summed up and the word will be written to the output file once. The output file will have one word and its count per a line. The word and its count will be separated with a space character.




The maximum number of child processes will be 5. The maximum number of message queues will be 5 as well.




<strong>Part B) </strong>This time you will implement the same program using multiple threads. This program will be called <strong>twc</strong>. For each input file, you will create another thread, that can be called a worker thread, that will process the file. A worker thread the put the words read into a sorted linked list (again you can use insertion sort). The main thread will wait until all worker threads finished generating the linked lists. Then the main thread will access the linked lists generated worker threads, and will write the words and their counts to output file in sorted order, as in part A. You will use POSIX threads (also called Pthreads).




<h1>Experiments</h1>




After developing and testing the programs, you will do some timing experiments. For each program, conduct timing experiments that will measure the time it takes to complete the program for various number of children, sizes of input files, etc. Plot the results in graphs. Compare thread performance with child-process performance. Try to interpret the results. Compare thread performance with child-process performance.  Put all these into a report.