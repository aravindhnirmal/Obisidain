[[Keep/Colour/DEFAULT]] [[Keep/Archived]] 

class ATM:
    def display_menu(self):
        print("1. Check Balance")
        print("2. Deposit Money")
        print("3. Withdraw Money")
        print("4. Exit")

    def check_balance(self, balance):
        print(f"Your current balance is: ${balance:.2f}")

    def deposit_money(self, balance):
        while True:
            try:
                deposit_amount = float(input("Enter the amount to deposit: "))
                if deposit_amount <= 0:
                    print("Invalid amount. Please enter a positive value.")
                else:
                    balance += deposit_amount
                    print(f"${deposit_amount:.2f} deposited successfully.")
                    break
            except ValueError:
                print("Invalid input. Please enter a valid amount.")

        return balance

    def withdraw_money(self, balance):
        while True:
            try:
                withdraw_amount = float(input("Enter the amount to withdraw: "))
                if withdraw_amount <= 0:
                    print("Invalid amount. Please enter a positive value.")
                elif withdraw_amount > balance:
                    print("Insufficient balance.")
                else:
                    balance -= withdraw_amount
                    print(f"${withdraw_amount:.2f} withdrawn successfully.")
                    break
            except ValueError:
                print("Invalid input. Please enter a valid amount.")

        return balance

    def main(self):
        print("Welcome to the ATM Simulator!")
        account_number = input("Enter your account number: ")
        pin = input("Enter your PIN: ")
        initial_balance = float(input("Enter your initial balance: "))

        balance = initial_balance

        print("Account created successfully.")

        authenticated = False
        while not authenticated:
            entered_account_number = input("Enter your account number: ")
            entered_pin = input("Enter your PIN: ")

            if entered_account_number == account_number and entered_pin == pin:
                print("Authentication successful.")
                authenticated = True
            else:
                print("Authentication failed. Please try again.")

        while True:
            self.display_menu()
            choice = input("Enter your choice (1/2/3/4): ")

            if choice == "1":
                self.check_balance(balance)
            elif choice == "2":
                balance = self.deposit_money(balance)
            elif choice == "3":
                balance = self.withdraw_money(balance)
            elif choice == "4":
                print("Thank you for using the ATM. Goodbye!")
                break
            else:
                print("Invalid choice. Please select a valid option.")


if __name__ == "__main__":
    atm = ATM()
    atm.main()

