# Convert-Number-to-Words

You’re given a number, and your task is to express it in English words. Can you translate the numeric value into its full written form in English?

Input
The first line of the input contains a single integer n.

Constraints
0 ≤ num ≤ 231 - 1
Output
Output the English words representation of integer 'n.

def number_to_words(n):
    if n == 0:
        return "Zero"

    below_20 = ["", "One", "Two", "Three", "Four", "Five", "Six", "Seven", "Eight", "Nine", "Ten", 
                "Eleven", "Twelve", "Thirteen", "Fourteen", "Fifteen", "Sixteen", "Seventeen", 
                "Eighteen", "Nineteen"]
    tens = ["", "", "Twenty", "Thirty", "Forty", "Fifty", "Sixty", "Seventy", "Eighty", "Ninety"]
    thousands = ["", "Thousand", "Million", "Billion"]

    def three_digit_to_words(num):
        if num == 0:
            return ""
        elif num < 20:
            return below_20[num] + " "
        elif num < 100:
            return tens[num // 10] + " " + three_digit_to_words(num % 10)
        else:
            return below_20[num // 100] + " Hundred " + three_digit_to_words(num % 100)

    result = ""
    i = 0

    while n > 0:
        if n % 1000 != 0:
            result = three_digit_to_words(n % 1000) + thousands[i] + " " + result
        n //= 1000
        i += 1

    return result.strip()

# Input and output handling
try:
    n = int(input())
except EOFError:
    n = 1234567  # Default value for testing

print(number_to_words(n))
