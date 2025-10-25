# skill-assessment-1/mpmc

Write an assembly language program in 8086 to search for a given number in an array of N elements and display whether the number is found or not found.

AIM:

To write an 8086 Assembly Language Program to search for a given number in an array of N elements and display whether the number is FOUND or NOT FOUND.

ALGORITHM:

1.Start the program.

2.Initialize the Data Segment.

3.Store an array of numbers in memory.

4.Store the number to be searched in a register (say AL).

5.Initialize a counter (CL) with the total number of array elements (N).

6.Load the base address of the array into SI.

7.Compare the number to be searched (AL) with each element in the array:

If equal, display the message “NUMBER FOUND” and stop.

If not equal, increment the pointer (SI) and decrement the counter (CL).

8.Repeat the comparison until all elements are checked.

9.If the counter becomes zero and the number is not found, display the message “NUMBER NOT FOUND”.

10.Stop the program.

PROGRAM:
```
DATA SEGMENT
    ARRAY DB 12H, 25H, 34H, 56H, 78H, 9AH  ; Array of elements
    N DB 06H                               ; Number of elements
    KEY DB 56H                             ; Number to be searched
    MSG1 DB 'NUMBER FOUND$'
    MSG2 DB 'NUMBER NOT FOUND$'
DATA ENDS

CODE SEGMENT
ASSUME CS:CODE, DS:DATA

START:
    MOV AX, DATA
    MOV DS, AX              ; Initialize data segment

    MOV CL, N               ; CL = number of elements
    MOV SI, OFFSET ARRAY    ; Point to start of array
    MOV AL, KEY             ; AL = number to be searched

SEARCH_LOOP:
    CMP AL, [SI]            ; Compare current element with key
    JE FOUND                ; If equal → jump to FOUND
    INC SI                  ; Move to next element
    DEC CL                  ; Decrease count
    JNZ SEARCH_LOOP         ; If not zero, repeat loop

NOTFOUND:
    LEA DX, MSG2
    MOV AH, 09H
    INT 21H                 ; Display "NUMBER NOT FOUND"
    JMP EXIT

FOUND:
    LEA DX, MSG1
    MOV AH, 09H
    INT 21H                 ; Display "NUMBER FOUND"

EXIT:
    MOV AH, 4CH
    INT 21H                 ; Return to DOS

CODE ENDS
END START
```
OUTPUT:
<img width="600" height="400" alt="Screenshot (36)" src="https://github.com/user-attachments/assets/8b889ac5-c3c1-4759-b916-e40503ad600b" />



RESULT:

The program successfully searches the given number in an array of N elements and displays one of the following messages:

If the number exists in the array:

NUMBER FOUND!

If the number does not exist in the array:

NUMBER NOT FOUND!

