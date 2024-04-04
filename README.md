#include <iostream>
#include <fstream>
#include <cmath>
#include <stdexcept>
// Функція для обчислення T(x) з таблиці
double computeT(double x) {
    // Ваша реалізація для зчитування даних та обчислення T(x)
    double t; // Припустимо, що t - значення T(x) зчитане з файлу
    return t; // Повертаємо значення T(x)
}
// Функція для обчислення U(x) з таблиці
double computeU(double x) {
    // Ваша реалізація для зчитування даних та обчислення U(x)
    double u; // Припустимо, що u - значення U(x) зчитане з файлу
    return u; // Повертаємо значення U(x)
}
// Функція для обчислення функції fun(x, y, z) за алгоритмами 1, 2 або 3
double computeFun(double x, double y, double z) {
    double fun;
    if (x < 0) {
        fun = (y * z * x * y * z) + (y * x * z - (83891 * y * x * z));
    } else if (x >= 0.1 && x <= 1) {
        fun = (x * y * y * z * z * computeT(x) * computeT(x) * computeT(x) * computeT(x)) + (5 * (y / 5) * (y / 5) * (y / 5) * z * z * z * z * z);
    } else {
        if ((y * z * z) > (x * x))
            fun = (sqrt(pow(y, 2) + pow(x, 2))) + (441 * pow(y, 2) * z);
        else
            fun = (sqrt(pow(y, 2) + pow(x, 2))) + (441 * pow(y, 2) * z) + (441 * pow(x, 2) * z);
    }
    return fun;
}
int main() {
    double x, y, z;
    std::cout << "Введіть значення x, y та z: ";
    std::cin >> x >> y >> z;

    try {
        double result = computeFun(x, y, z);
        std::cout << "Результат обчислення fun(x, y, z): " << result << std::endl;
    } catch (const std::runtime_error& e) {
        std::cerr << "Помилка: " << e.what() << std::endl;
    }
    return 0;
}
