# Day 1: Calorie Counting (2022)
## Code (Correct):
    def find_max_calories(filename):
        with open(filename, 'r') as file:
            max_calories = 0
            current_calories = 0
            for line in file:
                line = line.strip()  # Remove leading/trailing whitespace
                if line:  # If the line is not empty
                    current_calories += int(line)  # Add the calories to the current elf's total
                else:  # If the line is empty (new elf)
                    if current_calories > max_calories:
                        max_calories = current_calories
                    current_calories = 0  # Reset for the next elf
            # Check the last elf's calories after the loop
            if current_calories > max_calories:
                max_calories = current_calories
        return max_calories

    # Example usage:
    elf_data = "calories_file.txt"  # Replace with your input file name
    max_calories = find_max_calories(elf_data)
    print(f"The elf carrying the most calories is carrying {max_calories} calories.")


## Output: 
The elf carrying the most calories is carrying 71506 calories.
# Day 10: Syntax Scoring (2021)
##  Code (Correct):
    def get_syntax_error_score(line):
        opening_brackets = {'(': ')', '[': ']', '{': '}', '<': '>'}
        stack = []

        for char in line:
            if char in opening_brackets:
                stack.append(char)
            else:
                if not stack or opening_brackets[stack.pop()] != char:
                    if char == ')':
                        return 3
                    elif char == ']':
                        return 57
                    elif char == '}':
                        return 1197
                    elif char == '>':
                        return 25137

        return 0

    def main():
        with open('navigation_input.txt', 'r') as file:
            lines = file.readlines()

        total_score = 0
        for line in lines:
            score = get_syntax_error_score(line.strip())
            if score:
                total_score += score

        print("Total syntax error score:", total_score)

    if __name__ == "__main__":
        main()

## Output:
Total Syntax Error Score: 296535
# Day 7: Camel Cards (2023)
## Code (Incorrect):
    def get_hand_type(hand):
        counts = {}
        for card in hand:
            counts[card] = counts.get(card, 0) + 1

        if 5 in counts.values():
            return "Five of a kind"
        elif 4 in counts.values():
            return "Four of a kind"
        elif 3 in counts.values() and 2 in counts.values():
            return "Full house"
        elif 3 in counts.values():
            return "Three of a kind"
        elif 2 in counts.values() and len(counts) == 3:
            return "Two pair"
        elif 2 in counts.values():
            return "One pair"
        else:
            return "High card"

    def compare_hands(hand1, hand2):
        type1 = get_hand_type(hand1)
        type2 = get_hand_type(hand2)

        if type1 != type2:
            return type1 > type2

        for i in range(5):
            if hand1[i] != hand2[i]:
                return hand1[i] > hand2[i]

        return True

    def calculate_rank(hands):
        sorted_hands = sorted(hands, key=lambda x: (get_hand_type(x), x))
        return [sorted_hands.index(hand) + 1 for hand in hands]

    def calculate_winnings(hands, bids):
        ranks = calculate_rank(hands)
        total_winnings = 0
        for hand, bid, rank in zip(hands, bids, ranks):
            total_winnings += bid * rank
        return total_winnings

    # Read input from a text file
    with open("hands.txt", "r") as file:
        hands = []
        bids = []
        for line in file:
            hand, bid = line.strip().split()
            hands.append(hand)
            bids.append(int(bid))

    # Calculate total winnings
    total_winnings = calculate_winnings(hands, bids)
    print("Total winnings:", total_winnings)
## Output:
Total winnings: 249475442
