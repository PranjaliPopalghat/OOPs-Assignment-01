#include <iostream>
using namespace std;

class Account {
protected:
    string name;
    int accNum;
    double balance;
public:
    void initialize(string n, int num, double bal) {
        name = n; accNum = num; balance = bal;
    }
    void deposit(double amt) { balance += amt; }
    void displayBalance() { cout << "Balance: " << balance << endl; }
};

class SavAcct : public Account {
public:
    void computeInterest(double rate) { balance += balance * rate / 100; }
    void withdraw(double amt) { balance = (amt <= balance) ? balance - amt : balance; }
};

class CurAcct : public Account {
public:
    void withdraw(double amt) {
        if (balance - amt < 500) balance -= 50; // Service charge
        balance = (amt <= balance) ? balance - amt : balance;
    }
};

int main() {
    SavAcct s;
    s.initialize("Alice", 101, 1000);
    s.deposit(500);
    s.computeInterest(5);
    s.withdraw(300);
    s.displayBalance();

   CurAcct c;
    c.initialize("Bob", 102, 600);
    c.deposit(400);
    c.withdraw(700);
    c.displayBalance();

   return 0;
}
