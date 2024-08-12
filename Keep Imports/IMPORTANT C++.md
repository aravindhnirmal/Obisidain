[[Keep/Colour/DEFAULT]] [[Keep/Archived]] 

[[include]] <iostream>
int getValueFromUser()
{
 	std::cout << "Enter an integer: ";
	int input{};
	std::cin >> input;
	return input;//return input thaan purila nalla paaru main fun la return pannanum
}
void printDouble(int value) // This function now has an integer parameter
{
	std::cout << value << " doubled is: " << value * 2 << '\n';
}

int main()
{
	int num { getValueFromUser() };// num is taken by a parameter as calling getValueFromUser() ,
	//we create two variable first num nu one ,2rd getValueFromUser() athula oru variable name input

	printDouble(num);//intDouble la num ma include panurom
	return 0;
}
