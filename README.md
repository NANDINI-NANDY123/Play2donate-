import random

# Dictionaries to store user information and donations
users = {}
donations = {}

# Function to register a new user
def register():
    username = input("Enter username: ")
    password = input("Enter password: ")
    
    if username in users:
        print("Username already exists!")
    else:
        users[username] = password
        donations[username] = 0
        print("Registration successful!")

# Function to login
def login():
    username = input("Enter username: ")
    password = input("Enter password: ")
    
    if users.get(username) == password:
        print("Login successful!")
        return username
    else:
        print("Invalid login")
        return None

# Function to play the quiz game
def play_game(username):
    print(f"Welcome {username} to Play2Donate Quiz!")

    # List of questions and answers
    questions = [
        ("Which planet is known as the Red Planet?", "Mars"),
        ("Who developed Python?", "Guido van Rossum"),
        ("Which ocean is the largest?", "Pacific")
    ]

    score = 0
    random.shuffle(questions)

    for q, ans in questions:
        user_ans = input(q + " ")
        if user_ans.strip().lower() == ans.lower():
            print("Correct!")
            score += 1
        else:
            print(f"Wrong! Correct answer is: {ans}")

    print(f"Your score: {score}")

    # Ask if user wants to donate
    donate = input("Do you want to donate your score as amount? (yes/no) ").strip().lower()
    if donate == 'yes':
        donations[username] += score
        print(f"Thank you for donating! Total donation: {donations[username]}")

# Function to view donation summary
def view_donations():
    print("\nDonation Summary")
    for user, amount in donations.items():
        print(f"{user}: {amount}")

# Main program menu
def main():
    while True:
        print("\n--- Play2Donate Menu ---")
        print("1. Register")
        print("2. Login")
        print("3. Exit")
        
        choice = input("Choose option: ")

        if choice == '1':
            register()
        elif choice == '2':
            user = login()
            if user:
                while True:
                    print("\n--- User Menu ---")
                    print("1. Play Game")
                    print("2. View Donations")
                    print("3. Logout")
                    user_choice = input("Choose option: ")
                    
                    if user_choice == '1':
                        play_game(user)
                    elif user_choice == '2':
                        view_donations()
                    elif user_choice == '3':
                        break
                    else:
                        print("Invalid option, try again!")
        elif choice == '3':
            print("Goodbye!")
            break
        else:
            print("Invalid option, try again!")

# Run the program
if __name__ == "__main__":
    main()
