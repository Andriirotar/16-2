#include <iostream>
#include <fstream>
#include <vector>
#include <stdexcept>
// Функція для зчитування даних з файлу та побудови таблиці
std::vector<std::vector<double>> readTableFromFile(const std::string& filename) {
    std::ifstream file(filename);
    if (!file.is_open()) {
        throw std::runtime_error("Помилка відкриття файлу " + filename);
    }
    std::vector<std::vector<double>> table;
    double x, T, U;
    while (file >> x >> T >> U) {
        table.push_back({x, T, U});
    }
    return table;
}
// Функція для обчислення T(x) з таблиці
double computeT(const std::vector<std::vector<double>>& table, double x) {
    for (const auto& row : table) {
        if (row[0] == x) {
            return row[1];
        }
    }
    throw std::runtime_error("Немає значення T для введеного x");
}
// Функція для обчислення U(x) з таблиці
double computeU(const std::vector<std::vector<double>>& table, double x) {
    for (const auto& row : table) {
        if (row[0] == x) {
            return row[2];
        }
    }
    throw std::runtime_error("Немає значення U для введеного x");
}
// Алгоритм 1
double algorithm1(double x, double y, double z) {
    return (y * z * x * y * z) + (y * x * z - (x * y * z * 83891.));
}
// Алгоритм 2
double algorithm2(double x, double y, double z) {
    return (y * z * x * y * z) - (x * y * z * 13890.) + (y * z * x * y * z) - (x * y * z * 83891.);
}
// Алгоритм 3
double algorithm3(double x, double y, double z, const std::vector<std::vector<double>>& table) {
    double T, U;
    if (x <= 1) {
        T = computeT(table, x);
        U = computeU(table, x);
    } else {
        x = 1 / x;
        T = computeT(table, x);
        U = computeU(table, x);
    }
    return (y * x * z * U * T) + (z * U);
}
int main() {
    double x, y, z;
    std::cout << "Введіть значення x, y та z: ";
    std::cin >> x >> y >> z;
    try {
        std::vector<std::vector<double>> table1 = readTableFromFile("dat_X_1_1.dat");
        std::vector<std::vector<double>> table2 = readTableFromFile("dat_X1_00.dat");
        std::vector<std::vector<double>> table3 = readTableFromFile("dat_X00_1.dat");
        double result;
        if (x <= -1) {
            result = algorithm1(x, y, z);
        } else if (x > -1 && x <= 0) {
            result = algorithm2(x, y, z);
        } else if (x > 0) {
            result = algorithm3(x, y, z, table1);
        }
        std::cout << "Результат обчислення fun(x, y, z): " << result << std::endl;
    } catch (const std::runtime_error& e) {
        std::cerr << "Помилка: " << e.what() << std::endl;
    }
    return 0;
}
