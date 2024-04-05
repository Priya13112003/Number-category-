# Number-category-
@FunctionalInterface
interface NumberCategory {
    boolean checkNumberCategory(int number1, int number2);
}

public class NumberCategoryUtility {
    public static NumberCategory checkAmicable() {
        return (number1, number2) -> {
            int sumDivisors1 = sumDivisors(number1);
            int sumDivisors2 = sumDivisors(number2);
            return sumDivisors1 == number2 && sumDivisors2 == number1;
        };
    }

    public static NumberCategory checkPalindrome() {
        return (number1, number2) -> {
            int product = number1 * number2;
            String productString = String.valueOf(product);
            return isPalindrome(productString);
        };
    }

    private static int sumDivisors(int number) {
        int sum = 1; // Start with 1 as 1 is always a divisor
        for (int i = 2; i <= Math.sqrt(number); i++) {
            if (number % i == 0) {
                sum += i;
                if (i != number / i) { // Check for non-square divisors
                    sum += number / i;
                }
            }
        }
        return sum;
    }

    private static boolean isPalindrome(String str) {
        int i = 0;
        int j = str.length() - 1;
        while (i < j) {
            if (str.charAt(i) != str.charAt(j)) {
                return false;
            }
            i++;
            j--;
        }
        return true;
    }

    public static void main(String[] args) {
        int number1 = 220;
        int number2 = 284;

        NumberCategory amicableChecker = checkAmicable();
        NumberCategory palindromeChecker = checkPalindrome();

        System.out.println("Numbers are amicable: " + amicableChecker.checkNumberCategory(number1, number2));
        System.out.println("Product is palindrome: " + palindromeChecker.checkNumberCategory(number1, number2));
    }
}
