
Author: Amit Choudhary<br>
Email: amitchoudhary0523 AT gmail DOT com<br>
<br>
<br>
**C++ has a big flaw. You can change the values of the private member variables directly by getting the pointer to the object. So, private member variables are actually not private, they are public. Below is the example code:**
```

#include <iostream>

using namespace std;

class MyClass
{

private:
    int i;
    int j;

public:
    MyClass(int a, int b)
    {
        i = a;
        j = b;
    }

    void print_data()
    {
        cout << endl;
        cout << "i = " << i << ", j = " << j;
    }

}; // end of class MyClass

int main(void)
{

    MyClass myobj(1, 4);

    myobj.print_data();

    MyClass *m = &myobj;

    //int *i_ptr = (int *)(m); // this works too
    int *i_ptr = reinterpret_cast <int *>(m);
    int *j_ptr = i_ptr + 1;
    
    *i_ptr = 10;
    *j_ptr = 20;

    myobj.print_data();

    cout << endl << endl;

    return 0;

} // end of function main()

The output is:

i = 1, j = 4
i = 10, j = 20

So, you see that the values of the private member variables ('i' and 'j') were changed
directly by using pointers. So, the 'private' keyword actually didn't serve its purpose.

```
