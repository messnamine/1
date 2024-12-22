import random

class Player:
    def __init__(self, name):
        self.name = name
        self.position = 0
        self.money = 1500  # Starting money
        self.properties = []

    def move(self, steps):
        self.position = (self.position + steps) % len(board)
        print(f"{self.name} moves to {board[self.position].name}")

    def buy_property(self):
        current_property = board[self.position]
        if not current_property.owner and self.money >= current_property.price:
            self.properties.append(current_property)
            self.money -= current_property.price
            current_property.owner = self
            print(f"{self.name} buys {current_property.name} for ${current_property.price}")
        else:
            print(f"{self.name} cannot buy {current_property.name}")

class Property:
    def __init__(self, name, price):
        self.name = name
        self.price = price
        self.owner = None

class Board:
    def __init__(self):
        self.spaces = [
            Property("Go", 0), Property("Mediterranean Avenue", 60), 
            Property("Community Chest", 0), Property("Baltic Avenue", 60),
            Property("Income Tax", 0), Property("Reading Railroad", 200),
            Property("Oriental Avenue", 100), Property("Chance", 0),
            Property("Vermont Avenue", 100), Property("Connecticut Avenue", 120)
        ]

    def __getitem__(self, index):
        return self.spaces[index]

# Initialize game components
board = Board()
players = [Player("Player 1"), Player("Player 2")]

# Simple game loop
for turn in range(10):
    for player in players:
        input(f"{player.name}'s turn. Press Enter to roll the dice...")
        dice_roll = random.randint(1, 6)
        print(f"{player.name} rolls a {dice_roll}")
        player.move(dice_roll)
        player.buy_property()
        print(f"{player.name}'s money: ${player.money}")
        print(f"{player.name}'s properties: {[prop.name for prop in player.properties]}")
        print("-" * 20)
        
