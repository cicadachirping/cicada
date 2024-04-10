#include <iostream>
#include <cstdlib>
#include <ctime>
#include <sstream>

using namespace std;

// 生成一个指定范围内的随机整数
int generateRandomNumber(int min, int max) {
    return rand() % (max - min + 1) + min;
}

// 将整数转换为字符串
string intToString(int num) {
    stringstream ss;
    ss << num;
    return ss.str();
}

// 生成加法运算式
string generateAdditionExpression(int grade) {
    int num1 = generateRandomNumber(1, grade == 1 ? 20 : (grade == 2 ? 50 : 1000));
    int num2 = generateRandomNumber(1, grade == 1 ? 20 : (grade == 2 ? 50 : 1000));
    return intToString(num1) + " + " + intToString(num2);
}

// 生成减法运算式
string generateSubtractionExpression(int grade) {
    int num1 = generateRandomNumber(1, grade == 1 ? 20 : (grade == 2 ? 50 : 1000));
    int num2 = generateRandomNumber(1, grade == 1 ? 20 : (grade == 2 ? 50 : 1000));
    return intToString(num1) + " - " + intToString(num2);
}

// 生成乘法运算式
string generateMultiplicationExpression(int grade) {
    int num1 = generateRandomNumber(1, grade == 3 ? 1000 : 100);
    int num2 = generateRandomNumber(1, grade == 3 ? 1000 : 100);
    return intToString(num1) + " * " + intToString(num2);
}

// 生成除法运算式
string generateDivisionExpression(int grade) {
    int num1 = generateRandomNumber(1, grade == 4 ? 100 : 1000);
    int num2 = generateRandomNumber(1, grade == 4 ? 100 : 1000);
    return intToString(num1) + " / " + intToString(num2);
}

// 生成混合运算式
string generateMixedExpression(int grade) {
    // 随机确定运算符数量
    int num_operators = 3;
    if (grade >= 4 && grade <= 6) {
        num_operators = generateRandomNumber(3, 5);
    }
    
    string expression;
    for (int i = 0; i < num_operators; ++i) {
        // 随机选择运算符
        int op = generateRandomNumber(0, 3);
        switch(op) {
            case 0: // 加法
                expression += generateAdditionExpression(grade);
                break;
            case 1: // 减法
                expression += generateSubtractionExpression(grade);
                break;
            case 2: // 乘法
                expression += generateMultiplicationExpression(grade);
                break;
            case 3: // 除法
                expression += generateDivisionExpression(grade);
                break;
        }
        expression += " ";
    }
    return expression;
}

int main() {
    srand(time(0)); // 初始化随机数种子
    
    int grade, num_questions;
    cout << "请输入年级（1-6）：";
    cin >> grade;
    cout << "请输入题目数量：";
    cin >> num_questions;
    
    cout << "生成的" << grade << "年级的" << num_questions << "道题目如下：" << endl;
    for (int i = 0; i < num_questions; ++i) {
        string expression;
        if (grade == 1 || grade == 2) {
            expression = generateAdditionExpression(grade);
        } else if (grade == 3) {
            int op = generateRandomNumber(0, 1);
            if (op == 0) {
                expression = generateAdditionExpression(grade);
            } else {
                expression = generateSubtractionExpression(grade);
            }
        } else {
            expression = generateMixedExpression(grade);
        }
        cout << expression << endl;
    }
    
    return 0;
}
