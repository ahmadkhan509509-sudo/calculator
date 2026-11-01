#include <iostream>
#include <limits>
#include <cmath>

class Calculator {
public:
    void printWelcomeMessage() const {
        std::cout << "=========================================\n";
        std::cout << "         Advanced C++ Calculator         \n";
        std::cout << "=========================================\n";
        std::cout << "Supported operations:\n";
        std::cout << "  + : Addition\n";
        std::cout << "  - : Subtraction\n";
        std::cout << "  * : Multiplication\n";
        std::cout << "  / : Division\n";
        std::cout << "  ^ : Power (x^y)\n";
        std::cout << "=========================================\n\n";
    }

    double getValidNumber(const std::string& prompt) const {
        double num;
        while (true) {
            std::cout << prompt;
            if (std::cin >> num) {
                return num;
            }
            std::cout << "Invalid input. Please enter a valid numerical value.\n";
            clearInputBuffer();
        }
    }

    char getValidOperator() const {
        char op;
        while (true) {
            std::cout << "Enter an operator (+, -, *, /, ^): ";
            std::cin >> op;
            if (op == '+' || op == '-' || op == '*' || op == '/' || op == '^') {
                return op;
            }
            std::cout << "Invalid operator! ";
            clearInputBuffer();
        }
    }

    void calculate(double num1, char op, double num2) const {
        std::cout << "\n-----------------------------------------\n";
        std::cout << "Result: ";
        switch (op) {
            case '+':
                std::cout << num1 << " + " << num2 << " = " << (num1 + num2) << "\n";
                break;
            case '-':
                std::cout << num1 << " - " << num2 << " = " << (num1 - num2) << "\n";
                break;
            case '*':
                std::cout << num1 << " * " << num2 << " = " << (num1 * num2) << "\n";
                break;
            case '/':
                if (num2 == 0) {
                    std::cout << "Error! Division by zero is undefined.\n";
                } else {
                    std::cout << num1 << " / " << num2 << " = " << (num1 / num2) << "\n";
                }
                break;
            case '^':
                std::cout << num1 << " ^ " << num2 << " = " << std::pow(num1, num2) << "\n";
                break;
            default:
                std::cout << "Unknown error occurred.\n";
        }
        std::cout << "-----------------------------------------\n\n";
    }

    bool askToContinue() const {
        char choice;
        std::cout << "Do you want to perform another calculation? (y/n): ";
        std::cin >> choice;
        clearInputBuffer();
        return (choice == 'y' || choice == 'Y');
    }

private:
    void clearInputBuffer() const {
        std::cin.clear();
        std::cin.ignore(std::limits<std::streamsize>::max(), '\n');
    }
};

int main() {
    Calculator calc;
    calc.printWelcomeMessage();

    bool keepRunning = true;
    while (keepRunning) {
        double num1 = calc.getValidNumber("Enter the first number: ");
        char op = calc.getValidOperator();
        double num2 = calc.getValidNumber("Enter the second number: ");

        calc.calculate(num1, op, num2);
        keepRunning = calc.askToContinue();
    }

    std::cout << "\nThank you for using Advanced C++ Calculator. Goodbye!\n";
    return 0;
}

