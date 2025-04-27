#include <iostream>
#include <limits>
#include <iomanip>

using namespace std;

int main() {
    double initialInvestment, monthlyDeposit, annualInterest;
    int numberOfYears;
    char continueReport;

    while (true) {
        // Get initial investment amount
        cout << "Enter initial investment amount: ";
        cin >> initialInvestment;

        // Validate initial investment
        while (cin.fail()) {
            cout << "Invalid Input! Please input a numerical value: ";
            cin.clear();
            cin.ignore(numeric_limits<streamsize>::max(), '\n');
            cin >> initialInvestment;
        }

        if (initialInvestment < 0) {
            cout << "Cannot compute with negative value." << endl;
            continue;  // Skip this iteration and ask for input again
        }

        // Get monthly deposit
        cout << "Enter monthly deposit: ";
        cin >> monthlyDeposit;

        // Validate monthly deposit
        while (cin.fail()) {
            cout << "Invalid Input! Please input a numerical value: ";
            cin.clear();
            cin.ignore(numeric_limits<streamsize>::max(), '\n');
            cin >> monthlyDeposit;
        }

        if (monthlyDeposit < 0) {
            cout << "Cannot compute with negative value." << endl;
            continue;  // Skip this iteration and ask for input again
        }

        // Get annual interest rate
        cout << "Enter annual interest rate (in percentage): ";
        cin >> annualInterest;

        // Validate annual interest
        while (cin.fail()) {
            cout << "Invalid Input! Please input a numerical value: ";
            cin.clear();
            cin.ignore(numeric_limits<streamsize>::max(), '\n');
            cin >> annualInterest;
        }

        if (annualInterest < 0) {
            cout << "Cannot compute with negative value." << endl;
            continue;  // Skip this iteration and ask for input again
        }

        // Get number of years
        cout << "Enter number of years: ";
        cin >> numberOfYears;

        // Validate number of years
        while (cin.fail()) {
            cout << "Invalid Input! Please input a numerical value: ";
            cin.clear();
            cin.ignore(numeric_limits<streamsize>::max(), '\n');
            cin >> numberOfYears;
        }

        if (numberOfYears <= 0) {
            cout << "Cannot compute with negative value." << endl;
            continue;  // Skip this iteration and ask for input again
        }

        // Ask user to press any key to continue
        cout << "Press any key to continue: ";
        cin >> continueReport;

        // Calculate year-end balance and earned interest
        if (continueReport) {
            double balanceNoDeposit = initialInvestment;
            double earnedInterestNoDeposit = 0;
            double balanceWithDeposit = initialInvestment;
            double earnedInterestWithDeposit = 0;

            double monthlyInterestRate = annualInterest / 100 / 12;

            // For each year, calculate the balance and interest
            for (int year = 1; year <= numberOfYears; ++year) {
                double interestNoDeposit = 0;
                double interestWithDeposit = 0;

                // Calculate year-end balance and earned interest without monthly deposits
                for (int month = 1; month <= 12; ++month) {
                    interestNoDeposit = balanceNoDeposit * monthlyInterestRate;
                    balanceNoDeposit += interestNoDeposit;
                }

                // Calculate year-end balance and earned interest with monthly deposits
                for (int month = 1; month <= 12; ++month) {
                    interestWithDeposit = balanceWithDeposit * monthlyInterestRate;
                    balanceWithDeposit += interestWithDeposit + monthlyDeposit;
                }

                // Display yearly report without monthly deposits
                cout << fixed << setprecision(2);
                cout << "Year " << year << " (No Monthly Deposits):" << endl;
                cout << "Year-End Balance: $" << balanceNoDeposit << endl;
                cout << "Year-End Earned Interest: $" << earnedInterestNoDeposit << endl;

                // Display yearly report with monthly deposits
                cout << "Year " << year << " (With Monthly Deposits):" << endl;
                cout << "Year-End Balance: $" << balanceWithDeposit << endl;
                cout << "Year-End Earned Interest: $" << earnedInterestWithDeposit << endl;
            }
        }

        // Ask user if they want to run another report or exit
        cout << "Do you want to run another report? (y/n): ";
        cin >> continueReport;

        if (continueReport != 'y' && continueReport != 'Y') {
            break;  // Exit the program if the user does not want to continue
        }
    }

    return 0;
}
