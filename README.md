# python-guess-game
import random
import os
from datetime import datetime

def numguess():

    """The main number guessing game logic."""

    print("Very Well, your number to guess in between from 1 to 10.Good luck!")
    realnum = random.randint(1,10)
    score = 0
    while True: 
        try:
            guessnum = int(input("Enter the guess number:- "))

            if guessnum == realnum:
                score += 1
                print(f"🎉 Congratulations! You guessed the correct number: {realnum}")
                print(f"you guessed the number {score} times")
                with open ("guessgamescore.txt", "a") as f:
                    now = datetime.now().strftime("%Y-%m-%d %H:%M:%S")
                    f.write(f"[{now}] Number of guesses: {str(score)}\n")
                break
            elif guessnum > realnum:
                print("📉 Too high! Try a lower number.")
                score += 1
            else:
                print("📈 Too low! Try a higher number.")
                score += 1

        except ValueError:
                print("Invalid input! Please enter a valid number.")
def main():
    """Main menu loop for the game."""
    print("Welcome to Number Guessing Game...")
    while True:
        check = input("Type p for play the game..\nType s for see your all score you play\nType e for exit the game...\n")
        if (check.lower() == "p"):
            numguess()
        elif check.lower() == "e":
                print("I hope we meet soon! Goodbye! 👋")
                try:
                    os.remove("guessgamescore.txt")
                    break
                except FileNotFoundError:
                    break
        elif check.lower()== "s":
            try:
                with open("guessgamescore.txt") as f:
                        data = f.readlines()
                        if data:
                            print("\nYour Scores:")
                            for idx, line in enumerate(data, start=1):
                                print(f"{idx}. {line.strip()}")
                        else:
                            print("No scores to display.")
            except FileNotFoundError:
                print("You haven't play the game yet, please play the game first then you are free to see your score.")
        else:
            print("Invalid option! Please type 'p' to play or 'e' to exit.")

# Start the game
if __name__ == "__main__":
    main()
