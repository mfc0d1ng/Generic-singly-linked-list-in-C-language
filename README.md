# Generic singly linked list in C language
A shared library which provides a set of functions for handling the singly linked list in C.

<h2> How to download? </h2>
You can download it here  <a href="https://github.com/user-attachments/files/21771845/libList.zip">here</a>

<h2> How to install? </h2>
Unzip the downloaded file and move libList.so to /usr/lib

<h2> How to link? </h2>
You can link the library to your C project as follows: gcc example.c -l List

<br>
<h2> Examples </h2>

* Example A:

<pre>
<code class="language-c">
#include &lt;stdio.h&gt;
#include &lt;stdlib.h&gt;
#include "List.h"

int main()
{
    /* Construct integers */
    List integers = List_new();

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
    
    return EXIT_SUCCESS;
}
</code>
</pre>

* Example B:

<pre>
<code class="language-c">
#include &lt;stdio.h&gt;
#include &lt;stdlib.h&gt;
#include &lt;string.h&gt;    
#include "List.h"

/* Sort predicate */
int sort_fruits_predicate(const void* __ls, const void* __rs)
{
    return strcmp(*(const char **)__ls, *(const char **)__rs) > 0;
}

int main()
{
    /* Construct fruits */
    List* fruits = List_object();

    /* Add fruits to List fruits */
    List_push_back(const char*, fruits, "strawberry");
    List_push_back(const char*, fruits, "apple");
    List_push_back(const char*, fruits, "pineapple");
    List_push_back(const char*, fruits, "banana");

    /* Sort fruits in ascending order */
    List_sort(fruits, sort_fruits_predicate);

    /* Print contents of fruits */
    printf("List fruits after sorting: ");
    for (List_iterator it = List_begin(fruits); it != NULL; it = it->next)
    {
        printf("%s ", List_data(const char*, it));
    }

    /* Erase fruits */
    List_delete(fruits);
    
    return EXIT_SUCCESS;   
}
</code>
</pre>

