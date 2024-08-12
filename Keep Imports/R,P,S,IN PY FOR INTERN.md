[[Keep/Colour/DEFAULT]] [[Keep/Archived]] 

import random

def game(user_choice, system_choice):
    if user_choice == system_choice:
        return "It's a tie!"
    elif user_choice == "rock":
        if system_choice == "paper":
            return "You lose! Paper covers rock."
        else:
            return "You win! Rock smashes scissors."
    elif user_choice == "paper":
        if system_choice == "scissors":
            return "You lose! Scissors cut paper."
        else:
            return "You win! Paper covers rock."
    elif user_choice == "scissors":
        if system_choice == "rock":
            return "You lose! Rock smashes scissors."
        else:
            return "You win! Scissors cut paper."
    else:
        return "Invalid input. Please choose rock, paper, or scissors."

def main():
    choices = ["rock", "paper", "scissors"]
    
    while True:
        print("Rock, Paper, Scissors Game")
        user_choice = input("Enter your choice (rock/paper/scissors): ").lower()
        
        if user_choice in choices:
            system_choice = random.choice(choices)
            result = game(user_choice, system_choice)
            print(f"System chose: {system_choice}")
            print(result)
        else:
            print("Invalid choice. Please choose rock, paper, or scissors.")
        
        play_again = input("Do you want to play again? (yes/no): ").lower()
        if play_again != "yes":
            print("Thanks for playing! Goodbye!")
            break

if __name__ == "__main__":
    main()

