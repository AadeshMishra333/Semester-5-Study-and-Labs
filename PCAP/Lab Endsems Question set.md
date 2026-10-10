10 mcqs OMP


MPI: given array 10 20 30 ... 80, 90
find global sum
global sum of squares
mean (average)
variance


CUDA: input is CUDA2026LAB
output is CUDA****LAB

basically for alphanumeric input, change numeric to *, retain all remaining
Write an MPI program in C using exactly 5 processes to process an array of temperatures.
Process 0 (root) should read the following inputs:
- The number of temperatures N
- An array containing N temperature values
- A reference temperature
The root process should distribute the input data to all processes. The remaining four processes should perform the following operations:
1. Process 1: Find the temperature in the array that is closest to the reference temperature and send the result to Process 0.
2. Process 2: Find all temperatures that are within ±2°C of the reference temperature and send the results to Process 0.
3. Process 3: Find the maximum temperature using MPI_Reduce with the MPI_MAX operation.
4. Process 4: Find the minimum temperature using MPI_Reduce with the MPI_MIN operation.
Since MPI_Reduce is a collective operation, all processes must participate in the reduction. The maximum result should be available at Process 3, and the minimum result should be available at Process 4.
Finally, Processes 1–4 should send their respective results to Process 0, and Process 0 should display all the results.
CUDA question: 
Write a CUDA C program that takes a string and a reference character as input from the user. Use the GPU to count the number of occurrences of the reference character in the given string. Each CUDA thread should examine one character of the string, and the atomicAdd() function should be used to safely increment a global counter whenever a thread finds a character matching the reference character. Finally, copy the count from the GPU back to the CPU and display the total number of occurrences.
Omp 10 mcqs
MPI:
Array of temperature readings: {10,12,14,16,18,20,22,24,27,28}. Reference temp = 25
Send pieces of array to other processes using routine communication. Send back closest temperature, farthest temperature from each chunk back to master using point to point communication. Master displays Global closest temp, Global farthest temp, difference of both from reference temp. Broadcast Global closest temp to all processes. Each process counts temp readings in Global closest temp - 2 to Global closest temp + 2 range. Use mpi function to calculate global count. Master broadcasts the global count.
CUDA:
Use program to find instances of a user input character in a user input sentence. Calculate total no of instances using atomic function.
1) MPI: given array 10 20 30 ... 80, 90
find global sum
global sum of squares
mean (average)
variance


CUDA: input is CUDA2026LAB
output is CUDA****LAB

basically for alphanumeric input, change numeric to *, retain all remaining

2) our question was
you have an array of sensor readings which is passed through 2 convolution filters of odd length
1)find the resultants
2)find difference between them
3) for each element in the difference array if the element is greater than t1 then that element in the array c is 1 if it is less than t1 then -1 otherwise 0

MPI question was SMTH like 
you are given an array of transactions with negative transactions meaning withdrawal and positive meaning deposit 

Divide the work equally. Add all the divided transactions. After dividing calculate the transactions in such a way that each process has the cumulative balance till that process (eg P1 balance = P1 local + p0 final). Each process should wait for the process before it before executing its own calculations.
The last process should display the local balance and the final balance

MPI:
Array of temperature readings: {10,12,14,16,18,20,22,24,27,28}. Reference temp = 25
Send pieces of array to other processes using routine communication. Send back closest temperature, farthest temperature from each chunk back to master using point to point communication. Master displays Global closest temp, Global farthest temp, difference of both from reference temp. Broadcast Global closest temp to all processes. Each process counts temp readings in Global closest temp - 2 to Global closest temp + 2 range. Use mpi function to calculate global count. Master broadcasts the global count.
CUDA:
Use program to find instances of a user input character in a user input sentence. Calculate total no of instances using atomic function.

now these were the questions from previous exams. give me 6 questions on CUDA that are very hard based on this
