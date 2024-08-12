[[Keep/Colour/DEFAULT]] [[Keep/Archived]] 

[[include]] <iostream>

int main()
{
    int count{ 1 };
    while (count <= 10) // this condition will never be false
    {
        std::cout << count << ' '; // so this line will repeatedly execute
    }

    std::cout << '\n'; // this line will never execute

    return 0; // this line will never execute
} 

\\in this count is always less than 10 so ,it inifinte print and  logic works and no incremental
