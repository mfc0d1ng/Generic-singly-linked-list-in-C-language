# Generic singly linked list in C language
A shared library which provides a set of functions for handling generic singly linked list in C. Note that the library doesn't provide methods for constructing and copying the list elements because C  isn't object-oriented programming language. User is responsible for constructing and copying the list elements.

<h2> How to download? </h2>
You can download it here  <a href="https://github.com/user-attachments/files/19392877/libList.zip">here</a>

<h2> How to install? </h2>
Unzip the downloaded file and move libList.so to /usr/lib

<h2> How to link? </h2>
You can link the library to your C project as follows: gcc example.c -l List <br>
And don't forget to include linked_list.h, note that linked_list.h depends on linked_list_details.h so keep both in the same directory.
