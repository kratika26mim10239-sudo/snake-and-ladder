# snake-and-ladder
a python program that implements a game
import random

# Positions of Snakes (Head -> Tail)
snakes = {
    17: 7,
    54: 34,
    62: 19,
    64: 60,
    87: 24,
    93: 73,
    95: 75,
    99: 78
}

# Positions of Ladders (Bottom -> Top)
ladders = {
    4: 14,
    9: 31,
    20: 38,
    28: 84,
    40: 59,
    51: 67,
    63: 81,
    71: 91
}

def roll_dice():
    return random.randint(1, 6)

def move_player(player_name, current_pos):
    input(f"\n{player_name}, press Enter to roll the dice...")
    dice = roll_dice()
    print(f"🎲 You rolled a {dice}!")
    
    new_pos = current_pos + dice
    
    # Player cannot go beyond position 100
    if new_pos > 100:
        print(f"You need exact points to reach 100. Staying at position {current_pos}.")
        return current_pos
    
    # Check for Ladders
    if new_pos in ladders:
        print(f"🚀 Great! You landed on a ladder at {new_pos} and climbed up to {ladders[new_pos]}!")
        new_pos = ladders[new_pos]
        
    # Check for Snakes
    elif new_pos in snakes:
        print(f"🐍 Oops! A snake bit you at {new_pos}! Going down to {snakes[new_pos]}.")
        new_pos = snakes[new_pos]
    else:
        print(f"Moved to position {new_pos}.")
        
    return new_pos

def play_game():
    print("====================================")
    print("   WELCOME TO SNAKE AND LADDER!     ")
    print("====================================")
    
    player1 = input("Enter Player 1 Name: ")
    player2 = input("Enter Player 2 Name: ")
    
    pos1 = 0
    pos2 = 0
    
    while True:
        # Player 1 Turn
        pos1 = move_player(player1, pos1)
        if pos1 == 100:
            print(f"\n🎉 CONGRATULATIONS! {player1} won the game! 🎉")
            break
            
        # Player 2 Turn
        pos2 = move_player(player2, pos2)
        if pos2 == 100:
            print(f"\n🎉 CONGRATULATIONS! {player2} won the game! 🎉")
            break

# Start the game
play_game()
