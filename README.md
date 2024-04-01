#include <iostream>
#include <stack>
template<typename T>
class Stack {
private:
    std::stack<T> data; // Внутрішній контейнер для зберігання даних
public:
    // Додавання елементу до стеку
    void push(const T& value) {
        data.push(value);
    }
    // Видалення елементу зі стеку
    void pop() {
        if (!data.empty()) {
            data.pop();
        }
    }
    // Виведення всіх елементів стеку в оберненому порядку
    void printReverse() {
        while (!data.empty()) {
            std::cout << data.top() << std::endl;
            data.pop();
        }
    }
};
int main() {
    Stack<double> doubleStack;
    Stack<int> intStack;
    // Читання цілих та дійсних чисел з вхідного потоку та додавання їх до стеку
    double doubleValue;
    int intValue;
    std::cout << "Введіть дійсні числа (для завершення введіть 0):\n";
    while (std::cin >> doubleValue && doubleValue != 0) {
        doubleStack.push(doubleValue);
    }
    std::cout << "Введіть цілі числа (для завершення введіть 0):\n";
    while (std::cin >> intValue && intValue != 0) {
        intStack.push(intValue);
    }
    // Виведення елементів стеку в оберненому порядку
    std::cout << "Дійсні числа у зворотньому порядку:\n";
    doubleStack.printReverse();
    std::cout << "Цілі числа у зворотньому порядку:\n";
    intStack.printReverse();
    return 0;
}
