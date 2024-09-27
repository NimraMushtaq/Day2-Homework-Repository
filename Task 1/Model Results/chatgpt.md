# Day 1: Calorie Counting (2022)
## Code (Correct):
    def find_max_calories_with_elf_number(file_path):
        # Read the input data from the file
        with open(file_path, 'r') as file:
            elf_data = file.read().strip().split("\n\n")

        # Initialize variables to hold the maximum calories and the corresponding elf number
        max_calories = 0
        elf_with_max_calories = 0

        for elf_index, elf in enumerate(elf_data, start=1):  # Start indexing from 1 for Elf numbers
            # Sum the calories for the current Elf
            calories = sum(int(item) for item in elf.splitlines() if item.strip().isdigit())

            # Update max calories and elf number if the current Elf has more
            if calories > max_calories:
                max_calories = calories
                elf_with_max_calories = elf_index

        return max_calories, elf_with_max_calories

    # Specify the path to your input file
    file_path = 'calories_file.txt'

    # Call the function with the input file
    max_calories, elf_number = find_max_calories_with_elf_number(file_path)
    print(f"Elf {elf_number} is carrying the most calories: {max_calories}")  

## Output: 
Elf 113 is carrying the most calories: 71506
# Day 10: Syntax Scoring (2021)
## Code (Correct):
    def calculate_syntax_score(file_path):def calculate_syntax_error_score(filename):
        # Define matching pairs and error points
        matching_pairs = {
            '(': ')',
            '[': ']',
            '{': '}',
            '<': '>'
        }

        error_points = {
            ')': 3,
            ']': 57,
            '}': 1197,
            '>': 25137
        }

        total_score = 0

        # Read lines from the input file
        with open(filename, 'r') as file:
            lines = file.readlines()

        for line in lines:
            line = line.strip()  # Remove any leading/trailing whitespace
            stack = []
            for char in line:
                if char in matching_pairs:  # If it's an opening character
                    stack.append(char)
                elif char in error_points:  # If it's a closing character
                    if stack and matching_pairs[stack[-1]] == char:
                        stack.pop()  # Correct match, pop from stack
                    else:
                        # Illegal character found
                        total_score += error_points[char]
                        break  # Stop checking this line

        return total_score

    # Specify the input file
    input_file = 'navigation_input.txt'

    # Calculate the total syntax error score
    result = calculate_syntax_error_score(input_file)
    print(f"Total Syntax Error Score: {result}")

## Output:
Total Syntax Error Score: 296535
# Day 7: Camel Cards (2023)
## Code (Incorrect):
    from collections import Counter

    # Card rankings
    card_values = {'A': 14, 'K': 13, 'Q': 12, 'J': 11, 'T': 10, '9': 9, '8': 8, '7': 7, '6': 6, '5': 5, '4': 4, '3': 3, '2': 2}

    # Function to categorize hand
    def categorize_hand(hand):
        counts = Counter(hand)
        values = sorted(counts.items(), key=lambda x: (-x[1], -card_values[x[0]]))
        if len(counts) == 1:  # Five of a kind
            return (7, values)
        elif len(counts) == 2 and values[0][1] == 4:  # Four of a kind
            return (6, values)
        elif len(counts) == 2 and values[0][1] == 3:  # Full house
            return (5, values)
        elif len(counts) == 3 and values[0][1] == 3:  # Three of a kind
            return (4, values)
        elif len(counts) == 3 and values[0][1] == 2:  # Two pair
            return (3, values)
        elif len(counts) == 4:  # One pair
            return (2, values)
        else:  # High card
            return (1, values)

    # Function to calculate total winnings
    def calculate_winnings(file_path):
        # Read hands and bids from file
        with open(file_path, 'r') as file:
            hands_with_bids = file.readlines()

        # Parse hands and bids
        hands = [(line.split()[0], int(line.split()[1])) for line in hands_with_bids]

        # Categorize and sort hands
        categorized_hands = [(hand, bid, categorize_hand(hand)) for hand, bid in hands]
        sorted_hands = sorted(categorized_hands, key=lambda x: (x[2][0], x[2][1]))

        # Assign ranks and calculate total winnings
        total_winnings = 0
        num_hands = len(sorted_hands)

        for i, (_, bid, _) in enumerate(sorted_hands):
            rank = i + 1
            total_winnings += bid * rank

        return total_winnings

    # Example usage
    file_path = 'hands.txt'  # Replace with the path to your file
    total_winnings = calculate_winnings(file_path)
    print(f"Total winnings: {total_winnings}")
## Output:
Total winnings: 249009627