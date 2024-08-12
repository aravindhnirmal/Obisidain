[[Keep/Colour/DEFAULT]] [[Keep/Archived]] 

def fahrenheit_to_celsius(fahrenheit):
    return (fahrenheit - 32) * 5/9

def celsius_to_fahrenheit(celsius):
    return celsius * 9/5 + 32

def main():
    while True:
        print("Temperature Converter")
        print("1. Convert Fahrenheit to Celsius")
        print("2. Convert Celsius to Fahrenheit")
        print("3. Exit")

        choice = input("Enter your choice (1/2/3): ")

        if choice == "1":
            fahrenheit = float(input("Enter temperature in Fahrenheit: "))
            celsius = fahrenheit_to_celsius(fahrenheit)
            print(f"{fahrenheit:.2f}°F is equivalent to {celsius:.2f}°C")
        elif choice == "2":
            celsius = float(input("Enter temperature in Celsius: "))
            fahrenheit = celsius_to_fahrenheit(celsius)
            print(f"{celsius:.2f}°C is equivalent to {fahrenheit:.2f}°F")
        elif choice == "3":
            print("Exiting the temperature converter. Goodbye!")
            break
        else:
            print("Invalid choice. Please select a valid option.")

if __name__ == "__main__":
    main()

