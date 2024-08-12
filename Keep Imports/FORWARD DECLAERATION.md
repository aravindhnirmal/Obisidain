[[Keep/Colour/DEFAULT]] [[Keep/Attachments]] [[Keep/Archived]] 

You can easily create function declarations by copy/pasting your function’s header and adding a semicolon.

[[include]] <iostream>
int add(int x, int y); // forward declaration using function prototype
int main()
{
    std::cout << "The sum of 3 and 4 is " << add(3, 4) << '\n';
    return 0;
}
int add(int x, int y)
{
    return x + y;
}



![[1664813208430.1842900776.png]]

![[1664813671626.426338859.png]]