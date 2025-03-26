# Generic singly linked list in C language
A shared library which provides a set of functions for handling generic singly linked list in C. Note that the library doesn't provide methods for constructing and copying the list elements because C  isn't object-oriented programming language. User is responsible for constructing and copying the list elements.

<h2> How to download? </h2>
You can download it here  <a href="https://github.com/user-attachments/files/19465345/libList.zip">here</a>

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
    /* Construct integers */
    List integers = List_new(int);

    for (size_t i = 101; i < 110; i++)
    {
        /* Add data to integers */
        List_push_back(int, &integers, i);
    }

    /* Insert 100 at the beginning of integers */
    List_insert_after(int, &integers, List_before_begin(&integers), 100);

    /* Print contents of integers */
    printf("List integers contains: ");
    for (List_iterator it = List_begin(&integers); it != NULL; it = it->next)
    {
        printf("%i ", List_data(int, it));
    }

    /* Erase integers */
    List_destructor(&integers);    
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
List create_matrix(int width, int height)
{
    /* Construct matrix */
    List matrix = List_new(int *);
    for (int i = 0; i < height; i++)
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
    int width, height;
    printf("%s", "Enter matrix width: ");
    scanf("%i", &width);
    printf("%s", "Enter matrix height: ");
    scanf("%i", &height);
    
    List matrix = create_matrix(width, height);

    /* Populate the matrix */
    for (List_iterator it = List_begin(&matrix); it; it = it->next)
    {
        for (size_t i = 0; i < width; i++)
        {
            List_data(int *, it)[i] = i;
        }
    }

    puts("matrix: ");
    /* Print the matrix */
    for (List_iterator it = List_begin(&matrix); it; it = it->next)
    {
        /* Print the current row in matrix */
        for (size_t i = 0; i < width; i++)
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

