# Day 1: Calorie Counting (2022)
## Code (Correct):
    def find_max_calories(input_file):
    """Finds the Elf carrying the most calories.

    Args:
        input_file: The path to the input file containing calorie counts.

    Returns:
        The maximum number of calories carried by an Elf.
    """

    with open(input_file, 'r') as f:
        lines = f.readlines()

    elf_calories = []
    current_elf_calories = 0
    for line in lines:
        if line.strip():
            current_elf_calories += int(line.strip())
        else:
            elf_calories.append(current_elf_calories)
            current_elf_calories = 0
    elf_calories.append(current_elf_calories)  # Add the last Elf's calories

    return max(elf_calories)

    # Replace 'input.txt' with the actual path to your input file
    max_calories = find_max_calories('calories_file.txt')
    print(max_calories)
  

## Output: 
71506
# Day 10: Syntax Scoring (2021)
## Code (Incorrect):
    def calculate_syntax_error_score(lines):
        """Calculates the total syntax error score for a list of lines.

        Args:
            lines: A list of strings representing the lines of the navigation subsystem.

        Returns:
            The total syntax error score.
        """

        scores = {')': 3, ']': 57, '}': 1197, '>': 25137}
        total_score = 0

        for line in lines:
            stack = []
            for char in line:
                if char in ['(', '[', '{', '<']:
                    stack.append(char)
                else:
                    if not stack or char != stack.pop():
                        total_score += scores[char]
                        break  # Exit the loop after finding the first error

        return total_score

    def read_input_from_file(filename):
        """Reads the input from a file and returns a list of lines.

        Args:
            filename: The name of the input file.

        Returns:
            A list of strings representing the lines of the input file.
        """

        with open(filename, 'r') as f:
            lines = f.readlines()
        return lines

    if __name__ == '__main__':
        filename = 'data.txt'  # Replace with the actual filename
        lines = read_input_from_file(filename)
        score = calculate_syntax_error_score(lines)
        print(score)
## Output:
55182 
# Day 7: Camel Cards (2023)
## Code (Incorrect):
    def hand_type(hand):
        """Determines the type of a given hand."""
        counts = {}
        for card in hand:
            counts[card] = counts.get(card, 0) + 1
        if len(counts) == 1:
            return "Five of a kind"
        elif len(counts) == 2:
            if max(counts.values()) == 4:
                return "Four of a kind"
            else:
                return "Full house"
        elif len(counts) == 3:
            if max(counts.values()) == 3:
                return "Three of a kind"
            else:
                return "Two pair"
        elif len(counts) == 4:
            return "One pair"
        else:
            return "High card"

    def compare_hands(hand1, hand2):
        """Compares two hands and returns 1 if hand1 is stronger, -1 if hand2 is stronger, and 0 if they are equal."""
        type1 = hand_type(hand1)
        type2 = hand_type(hand2)
        if type1 > type2:
            return 1
        elif type1 < type2:
            return -1
        else:
            for i in range(5):
                if hand1[i] > hand2[i]:
                    return 1
                elif hand1[i] < hand2[i]:
                    return -1
            return 0

    def calculate_total_winnings(hands):
        """Calculates the total winnings for a given list of hands."""
        hands.sort(key=lambda hand: (hand_type(hand), hand), reverse=True)
        total_winnings = 0
        for i, hand in enumerate(hands):
            total_winnings += (i + 1) * int(hand.split()[1])
        return total_winnings

    # Read the input data
    with open("hands.txt") as f:
        hands = f.readlines()

    # Calculate and print the total winnings
    print(calculate_total_winnings(hands))
## Output:
245768408