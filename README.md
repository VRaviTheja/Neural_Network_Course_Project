# Neural Networks And Fuzzy control - Braille Pattern Recognition
Identifying braille characters based on images. (Optical Braille Recognition)

# Algorithm(Hamming Net):



Assuming that the image
recognition software scans the printed braille pattern and saves it as a text
file “braille.txt”



1.   Initialise necessary variables



2.  Initialise 28 exemplar vectors  of integer type



3.  Calculate 28x6 floating point weight
matrix, using 



4.  Read file “braille.txt”



5.   Copy input string e.g.
100101001011000101100101…. from “braille.txt”



6.   Start main loop, iterate till end of input
string



a.    Copy next 6 characters of input string to temporary string



b.   Convert each character of temporary
string to binary integer array ‘1’ =1, ‘0’= -1  E.g. “100101” à inp_array = {1, -1, -1, 1, -1, 1}



c.    Perform Hamming Net Algorithm, followed by MAXNET to find the exemplar most similar to inp_array.



d.   Map output binary to corresponding character A, B, C… Z, #, blank space and write to the next position in output string.



e.   If character is #, set flag ‘number’ as 1 and delete last written character in output string



f.     If character is blank space, reset flag ‘number’ as 0



g.    If ‘number’ flag equals to 1, and character is A to J, replace with corresponding number in output string 



7.   Write output string to file “deciphered.txt”.



# Implementation:

We have implemented the above hamming net algorithm
using a C++ code.

Basically here we have two phases:



## 1.    Training Phase:



a.    Here we take the binary form(digit) value of each braille letter which we already know. And convert them to bipolar forms.



b.   Now we have created a Weight matrix (6x28) using the above algorithm which can be used in testing phase.



## 2.    Testing Phase:



a.    Here we have taken a set 50 random braille letters where we don’t know what letter it corresponds to in English. Now we have to find the corresponding English letter using above algorithm.



b.   We convert these letters into binary form and then into bipolar form to perform the algorithm.



c.    Now we have used weight matrix to find the hamming distance of the input for each English letter present.



d.   We also added a bias of value 3 to hamming distance to remove the negative values.



e.   Now the letter which gives maximum hamming distance is the desired letter.



f.     We have to find the desired output for all the 50 inputs using loops.

We have attached the input photos from which we have taken input.
The code which we have used to perform this project. The output in the form of console window.
