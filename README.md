# Generic singly linked list in C language
A shared library which provides a set of functions for handling generic singly linked list in C. Note that the library doesn't provide methods for constructing and copying the list elements because C  isn't object-oriented programming language. User is responsible for constructing and copying the list elements.

<h2> How to download? </h2>
You can download it here  <a href="https://github.com/user-attachments/files/19398575/libList.zip">here</a>

<h2> How to install? </h2>
Unzip the downloaded file and move libList.so to /usr/lib

<h2> How to link? </h2>
You can link the library to your C project as follows: gcc example.c -l List <br>
And don't forget to include linked_list.h, note that linked_list.h depends on linked_list_details.h so keep both in the same directory.
<br>
<h2> Examples </h2>

* Example A:

<pre>
<code class="language-c">
#include &lt;stdio.h&gt;
#include &lt;stdlib.h&gt;
#include "linked_list.h"

int main()
{
    /* Construct chars */
    List chars = List_new(char);
    /* Construct integers */
    List integers = List_new(int);
    /* Construct strings */
    List strings = List_new(const char *);
    
    /* Add characters to chars */
    List_push_back(char, &chars, 'A');
    List_push_back(char, &chars, 'B');
    List_push_back(char, &chars, 'C');

    /* Add integer values to integers */
    List_push_back(int, &integers, 1000);
    List_push_back(int, &integers, 1001);
    List_push_back(int, &integers, 1002);

    /* Add literal strings to strings */
    List_push_back(const char *, &strings, "Hello");
    List_push_back(const char *, &strings, "world");
    List_push_back(const char *, &strings, "2025");

    printf("List chars contains: ");
    for (List_iterator it = List_begin(&chars); it; it = it->next)
    {
        printf("'%c' -> ", List_data(char, it));
    }
    puts("NULL\n");

    printf("List integers contains: ");
    for (List_iterator it = List_begin(&integers); it; it = it->next)
    {
        printf("%i -> ", List_data(int, it));
    }
    puts("NULL\n");

    printf("List strings contains: ");
    for (List_iterator it = List_begin(&strings); it; it = it->next)
    {
        printf("\"%s\" -> ", List_data(const char *, it));
    }
    puts("NULL\n");

    /* Erase chars */
    List_destructor(&chars);
    /* Erase integers */
    List_destructor(&integers);
    /* Erase strings */
    List_destructor(&strings);

    return EXIT_SUCCESS;
}
</code>
</pre>

* Example B:

<pre>
<code class="language-c">
#include &lt;stdio.h&gt;
#include &lt;stdlib.h&gt;
#include "linked_list.h"

/* Allocate memory for matrix of a size height * width */
List create_matrix(int heigh, int width)
{
    /* Construct matrix */
    List matrix = List_new(int *);
    for (int i = 0; i < heigh; i++)
    {
        List_push_back(int *, &matrix, malloc(width * sizeof(int)));
        if(List_back(int *, &matrix) == NULL)
        {
            exit(EXIT_FAILURE);
        }
    }
    return matrix;
}

int main()
{
    List matrix = create_matrix(10, 10);

    /* Populate the matrix */
    for (List_iterator it = List_begin(&matrix); it; it = it->next)
    {
        for (size_t i = 0; i < 10; i++)
        {
            List_data(int *, it)[i] = i;
        }
    }

    puts("matrix: ");
    /* Print the matrix */
    for (List_iterator it = List_begin(&matrix); it; it = it->next)
    {
        /* Print the current row in matrix */
        for (size_t i = 0; i < 10; i++)
        {
            printf("%i ", List_data(int *, it)[i]);
        }
        /* Free the current row in matrix */
        free(List_data(int *, it));
        puts("");
    }

    /* Erase matrix */
    List_destructor(&matrix);

    return EXIT_SUCCESS;
}
</code>
</pre>

