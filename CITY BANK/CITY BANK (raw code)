#include <stdio.h>
#include <string.h>
#include <stdlib.h>
#include <ctype.h>
#include <time.h>


#define MAX_ACCOUNTS 100
#define MAX_PASSWORD_ATTEMPTS 5
#define SCREEN_WIDTH 60
#define SCREEN_HEIGHT 20


typedef struct {
    int accountNumber;
    char username[50];
    char password[50];
    double balance;
    char ownerName[100];
    char fathersName[100];
    int age;
    char dob[20];
    char panNumber[20];
    int isLocked;
} Account;


typedef struct {
    int accountNumber;
    char description[100];
    double amount;
} Transaction;

void registerUser();
void getFathersName();
void getOwnerName(char *fullName, size_t size);
int loginUser(Account *loggedInAccount);
void dashboard(Account *account);
void transferFunds(Account *account);
void displayBalance(const Account *account);
void viewTransactionHistory(const Account *account);
void viewDetails(const Account *account);
void closeAccount(Account *account);
void saveAccount(const Account *account);
int loadAccounts(Account accounts[], int max);
void recordTransaction(int accountNumber, const char *description, double amount);
int validateUsername(const char *username);
int validatePassword(const char *password);
int validatePAN(const char *panNumber);
int validateOwnerName(const char *name);
void saveToCSV(const Account *account);
void clearScreen();
void printRectangleBorder();
void printInRectangle(const char *content);
int isUsernameUnique(const char *username);
int isPanNumberUnique(const char *panNumber);
int calculateAge(int day, int month, int year);

#define MAX_ACCOUNTS 100
#define MAX_PASSWORD_ATTEMPTS 5

int main() {
    int choice;
    Account accounts[MAX_ACCOUNTS];
    Account loggedInAccount;
    int accountCount = loadAccounts(accounts, MAX_ACCOUNTS);        
    printf("  _____                                                         _____ \n");
    printf(" ( ___ )-------------------------------------------------------( ___ )\n");
    printf("  |   |                                                         |   | \n");
    printf("  |   |      ____ ___ _______   __  ____    _    _   _ _  __    |   | \n");
    printf("  |   |     / ___|_ _|_   _\\ \\ / / | __ )  / \\  | \\ | | |/ /    |   | \n");
    printf("  |   |    | |    | |  | |  \\ V /  |  _ \\ / _ \\ |  \\| | ' /     |   | \n");
    printf("  |   |    | |___ | |  | |   | |   | |_) / ___ \\| |\\  | . \\     |   | \n");
    printf("  |   |     \\____|___| |_|   |_|   |____/_/   \\_\\_| \\_|_|\\_\\    |   | \n");
    printf("  |___|                                                         |___| \n");
    printf(" (_____)-------------------------------------------------------(_____) \n");
    printf("\n                   WELCOME TO THE CITY BANK APP!\n");
    printf("        Manage your account, transfer funds, and much more.\n");
    printf("                     Press any key to continue          \n");
    getchar();


    while (1) {
        printInRectangle("1. Register  2. Login  3. Exit");
        printf("Enter your choice: ");
        if (scanf("%d", &choice) != 1) {
            printf("\nInvalid input. Please enter a number.\n\n");
            while (getchar() != '\n'); // Clear invalid input
            continue;
        }
        clearScreen();
        switch (choice) {
            case 1:
                registerUser();
                break;
            case 2:
                if (loginUser(&loggedInAccount)) {
                    dashboard(&loggedInAccount);
                }
                break;
            case 3:
                printInRectangle("Thanks for using CITY BANK APP.");
                return 0;
            default:
                printf("Invalid choice.\n");
        }
    }
}


 

void getOwnerName(char *fullName, size_t size) {
    char firstName[50];
    char lastName[50];
    getchar();
    do {
        printf("Enter First Name ('0' to cancel): ");
        fgets(firstName, sizeof(firstName), stdin);
        firstName[strcspn(firstName, "\n")] = '\0';
        if (strcmp(firstName, "0") == 0) {
            strncpy(fullName, "0", size);
            return;
        }
    } while (!validateOwnerName(firstName));

    do {
        printf("Enter Last Name ('0' to cancel): ");
        fgets(lastName, sizeof(lastName), stdin);
        lastName[strcspn(lastName, "\n")] = '\0';
        if (strcmp(lastName, "0") == 0) {
            strncpy(fullName, "0", size);
            return;
        }
    } while (!validateOwnerName(lastName));

    snprintf(fullName, size, "%s %s", firstName, lastName);
}

void registerUser() {
    Account newAccount;
    FILE *fp = fopen("accounts.dat", "ab");
    if (fp == NULL) {
        printf("Error opening file!\n");
        return;
    }
    printf(" _____                                                                         _____ \n");
    printf("( ___ )-----------------------------------------------------------------------( ___ )\n");
    printf(" |   |                                                                         |   | \n");
    printf(" |   |    ____  _____ ____ ___ ____ _____ ____      _  _____ ___ ___  _   _    |   | \n");
    printf(" |   |   |  _ \\| ____/ ___|_ _/ ___|_   _|  _ \\    / \\|_   _|_ _/ _ \\| \\ | |   |   | \n");
    printf(" |   |   | |_) |  _|| |  _ | |\\___ \\ | | | |_) |  / _ \\ | |  | | | | |  \\| |   |   | \n");
    printf(" |   |   |  _ <| |__| |_| || | ___) || | |  _ <  / ___ \\| |  | | |_| | |\\  |   |   | \n");
    printf(" |   |   |_| \\_\\_____\\____|___|____/ |_| |_| \\_\\/_/   \\_\\_| |___\\___/|_| \\_|   |   | \n");
    printf(" |___|                                                                         |___| \n");
    printf("(_____)-----------------------------------------------------------------------(_____) \n\n");

    getOwnerName(newAccount.ownerName, sizeof(newAccount.ownerName));
    if (strcmp(newAccount.ownerName, "0") == 0) {
        fclose(fp);
        printf("Registration cancelled.\n");
        return;
    }

    getFathersName(newAccount.fathersName, sizeof(newAccount.fathersName));
    if (strcmp(newAccount.fathersName, "0") == 0) {
        fclose(fp);
        printf("Registration cancelled.\n");
        return;
    }

    int day, month, year;
    while (1) {
        printf("Enter Date of Birth (DD/MM/YYYY) ('0' to cancel): ");
        scanf("%s", newAccount.dob);
        if (strcmp(newAccount.dob, "0") == 0) {
            fclose(fp);
            printf("Registration cancelled.\n");
            return;
        }
        if (sscanf(newAccount.dob, "%d/%d/%d", &day, &month, &year) == 3 &&
            day > 0 && day <= 31 && month > 0 && month <= 12 && year > 1900 && year <= 2024) {
            break;
        } else {
            printf("Invalid date of birth format. Please try again.\n");
        }
    }

    newAccount.age = calculateAge(day, month, year);
    if (newAccount.age < 18 || newAccount.age > 110) {
        fclose(fp);
        return;
    }

    printf("Enter PAN Number ('0' to cancel): ");
    while (1) {
        scanf("%s", newAccount.panNumber);
        if (strcmp(newAccount.panNumber, "0") == 0) {
            fclose(fp);
            printf("Registration cancelled.\n");
            return;
        }
        if (validatePAN(newAccount.panNumber) && isPanNumberUnique(newAccount.panNumber)) {
            break;
        } else {
            printf("Invalid or duplicate PAN Number! Try again ('0' to cancel): ");
        }
    }

    printf("Enter Username ('0' to cancel): ");
    while (1) {
        scanf("%s", newAccount.username);
        if (strcmp(newAccount.username, "0") == 0) {
            fclose(fp);
            printf("Registration cancelled.\n");
            return;
        }
        if (validateUsername(newAccount.username) && isUsernameUnique(newAccount.username)) {
            break;
        } else {
            printf("Invalid or duplicate username! Try again ('0' to cancel): ");
        }
    }

    printf("Enter Password ('0' to cancel): ");
    while (1) {
        scanf("%s", newAccount.password);
        int passwordResult = validatePassword(newAccount.password);
        if (passwordResult == -1) {
            fclose(fp);
            printf("Registration cancelled.\n");
            return;
        } else if (passwordResult == 1) {
            break;
        } else {
            printf("Invalid password! Try again ('0' to cancel): ");
        }
    }

    printf("Enter Initial Deposit ('0' to cancel): ");
    while (scanf("%lf", &newAccount.balance) != 1 || newAccount.balance <= 0) {
        if (newAccount.balance == 0) {
            fclose(fp);
            printf("Registration cancelled.\n");
            return;
        }
        printf("Invalid deposit amount. Enter a valid amount ('0' to cancel): ");
        while (getchar() != '\n');
    }
    clearScreen();

    newAccount.accountNumber = rand() % 100000 + 1;
    newAccount.isLocked = 0;
    fwrite(&newAccount, sizeof(Account), 1, fp);
    fclose(fp);

    recordTransaction(newAccount.accountNumber, "Initial Deposit", newAccount.balance);

    printf("Account created successfully! Your account number is %d\n\n", newAccount.accountNumber);
}


int loginUser(Account *loggedInAccount) {
    int loginChoice;
    char username[50], password[50];
    int accountNumber;
    char choiceInput[10];

    FILE *fp = fopen("accounts.dat", "rb");
    if (fp == NULL) {
        printf("Error opening file!\n");
        return 0;
    }

    Account temp;
    int found = 0;

    while (1) {
        printInRectangle("1 : Username 2 : Account Number 3 : Exit");
        printf("Enter choice: ");
        scanf("%s", choiceInput);

        if (sscanf(choiceInput, "%d", &loginChoice) != 1 || (loginChoice != 1 && loginChoice != 2 && loginChoice != 3)) {
            printf("Invalid choice. Please enter 1, 2 or 3.\n");
            continue;
        }

        if (loginChoice == 1 || loginChoice == 2 || loginChoice == 3) {
            break;
        }
    }

    if (loginChoice == 1) {
        while (1) {
            printf("Enter Username ('0' to cancel): ");
            scanf("%s", username);

            if (strcmp(username, "0") == 0) {
                fclose(fp);
                printf("Login cancelled.\n");
                return 0;
            }

            rewind(fp);
            found = 0;

            while (fread(&temp, sizeof(Account), 1, fp)) {
                if (strcmp(temp.username, username) == 0) {
                    found = 1;
                    break;
                }
            }

            if (found) {
                break;
            } else {
                printf("Username not found. Please try again.\n");
            }
        }
    } else if (loginChoice == 2) {
        while (1) {
            printf("Enter Account Number ('0' to cancel): ");
            scanf("%d", &accountNumber);

            if (accountNumber == 0) {
                fclose(fp);
                printf("Login cancelled.\n");
                return 0;
            }

            rewind(fp);
            found = 0;

            while (fread(&temp, sizeof(Account), 1, fp)) {
                if (temp.accountNumber == accountNumber) {
                    found = 1;
                    break;
                }
            }

            if (found) {
                break;
            } else {
                printf("Account number not found. Please try again.\n");
            }
        }
    } else if (loginChoice == 3) {
        fclose(fp);
        return 0;
    }

    if (temp.isLocked) {
        printf("Account is locked due to multiple failed login attempts.\n");
        fclose(fp);
        return 0;
    }

    int attempts = 0;
    while (attempts < MAX_PASSWORD_ATTEMPTS) {
        printf("Enter Password ('0' to cancel): ");
        scanf("%s", password);

        if (strcmp(password, "0") == 0) {
            fclose(fp);
            printf("Login cancelled.\n");
            return 0;
        }

        if (strcmp(temp.password, password) == 0) {
            *loggedInAccount = temp;
            fclose(fp);
            printf("Login successful!\n");
            return 1;
        } else {
            printf("Incorrect password. Attempts remaining: %d\n", MAX_PASSWORD_ATTEMPTS - attempts - 1);
        }
        attempts++;
    }

    temp.isLocked = 1;
    saveAccount(&temp);
    printf("Account locked due to multiple failed attempts.\n");
    fclose(fp);
    return 0;
}

void dashboard(Account *account) {
    int choice;
    clearScreen();
    do {
        printf(" _____                                                               _____ \n");
        printf("( ___ )-------------------------------------------------------------( ___ )\n");
        printf(" |   |                                                               |   | \n");
        printf(" |   |    ____    _    ____  _   _ ____   ___    _    ____  ____     |   | \n");
        printf(" |   |   |  _ \\  / \\  / ___|| | | | __ ) / _ \\  / \\  |  _ \\|  _ \\    |   | \n");
        printf(" |   |   | | | |/ _ \\ \\___ \\| |_| |  _ \\| | | |/ _ \\ | |_) | | | |   |   | \n");
        printf(" |   |   | |_| / ___ \\ ___) |  _  | |_) | |_| / ___ \\|  _ <| |_| |   |   | \n");
        printf(" |   |   |____/_/   \\_\\____/|_| |_|____/ \\___/_/   \\_\\_| \\_\\____/    |   | \n");
        printf(" |___|                                                               |___| \n");
        printf("(_____)-------------------------------------------------------------(_____) \n\n");
        printf("1. Transfer Funds\n");
        printf("2. Display Balance\n");
        printf("3. View Transaction History\n");
        printf("4. View Account Details\n");
        printf("5. Close Account\n");
        printf("6. Logout\n");
        printf("Enter your choice: ");
        scanf("%d", &choice);

        switch (choice) {
            case 1:
                transferFunds(account);
                break;
            case 2:
                displayBalance(account);
                break;
            case 3:
                viewTransactionHistory(account);
                break;
            case 4:
                viewDetails(account);
                break;
            case 5:
                closeAccount(account);
                return;
            case 6:
                saveAccount(account);
                printf("Logging out...\n");
                break;
            default:
                printf("Invalid choice.\n");
        }
    } while (choice != 6);
}

void transferFunds(Account *account) {
    clearScreen();
    printInRectangle("Transfer Fund");
    printf("\n\n");
    int targetAccountNumber;
    double amount;
    FILE *fp = fopen("accounts.dat", "rb+");
    if (fp == NULL) {
        printf("Error opening file!\n");
        return;
    }

    printf("Enter target account number (or '0' to cancel): ");
    scanf("%d", &targetAccountNumber);
    if (targetAccountNumber == 0) {
        clearScreen();
        fclose(fp);
        return;
    }

    if (targetAccountNumber == account->accountNumber) {
        printf("You cannot transfer money to your own account.\n");
        fclose(fp);
        return;
    }

    printf("Enter amount to transfer: ");
    scanf("%lf", &amount);

    if (amount > 0 && amount <= account->balance) {
        Account temp;
        while (fread(&temp, sizeof(Account), 1, fp)) {
            if (temp.accountNumber == targetAccountNumber) {
                account->balance -= amount;
                temp.balance += amount;
                fseek(fp, -sizeof(Account), SEEK_CUR);
                fwrite(&temp, sizeof(Account), 1, fp);

                recordTransaction(account->accountNumber, "Amount Debited", -amount);
                recordTransaction(temp.accountNumber, "Amount Credited", amount);

                printf("Transfer successful!\n");
                fclose(fp);
                return;
            }
        }
        clearScreen();
        printf("Target account not found.\n");
    } else {
        clearScreen();
        printf("Invalid amount or insufficient balance.\n");
    }

    fclose(fp);
}

void displayBalance(const Account *account) {
    clearScreen();
    getchar();
    printf(" _____                                          _____ \n");
    printf("( ___ )----------------------------------------( ___ )\n");
    printf(" |   |                                          |   | \n");
    printf(" |   |    ____        _                         |   | \n");
    printf(" |   |   | __ )  __ _| | __ _ _ __   ___ ___    |   | \n");
    printf(" |   |   |  _ \\ / _` | |/ _` | '_ \\ / __/ _ \\   |   | \n");
    printf(" |   |   | |_) | (_| | | (_| | | | | (_|  __/   |   | \n");
    printf(" |   |   |____/ \\__,_|_|\\__,_|_| |_|\\___\\___|   |   | \n");
    printf(" |___|                                          |___| \n");
    printf("(_____)----------------------------------------(_____)\n\n");
    printf("Your current balance is: %.2lf\n\n", account->balance);
    printf("Press any key to continue...");
    getchar();
    clearScreen();
}

void viewTransactionHistory(const Account *account) {
    FILE *fp = fopen("transactions.dat", "rb");
    if (fp == NULL) {
        printf("Error opening transaction file!\n");
        return;
    }
    clearScreen();
    getchar();
    printf(" _____                                                             _____ \n");
    printf("( ___ )-----------------------------------------------------------( ___ )\n");
    printf(" |   |                                                             |   | \n");
    printf(" |   |    _____                               _   _                |   | \n");
    printf(" |   |   |_   _| __ __ _ _ __  ___  __ _  ___| |_(_) ___  _ __     |   | \n");
    printf(" |   |     | || '__/ _` | '_ \\/ __|/ _` |/ __| __| |/ _ \\| '_ \\    |   | \n");
    printf(" |   |     | || | | (_| | | | \\__ \\ (_| | (__| |_| | (_) | | | |   |   | \n");
    printf(" |   |     |_||_|  \\__,_|_| |_|___/\\__,_|\\___|\\__|_|\\___/|_| |_|   |   | \n");
    printf(" |   |               _   _ _     _                                 |   | \n");
    printf(" |   |              | | | (_)___| |_ ___  _ __ _  _                |   | \n");
    printf(" |   |              | |_| | / __| __/ _ \\| '__| | | |              |   | \n");
    printf(" |   |              |  _  | \\__ \\ || (_) | |  | |_| |              |   | \n");
    printf(" |   |              |_| |_|_|___/\\__\\___/|_|   \\__, |              |   | \n");
    printf(" |   |                                         |___/               |   | \n");
    printf(" |___|                                                             |___| \n");
    printf("(_____)-----------------------------------------------------------(_____)\n\n");

    Transaction temp;
    int found = 0;

    while (fread(&temp, sizeof(Transaction), 1, fp)) {
        if (temp.accountNumber == account->accountNumber) {
            printf("%s: %.2lf\n", temp.description, temp.amount);
            found = 1;
        }
    }

    if (!found) {
        printf("No transactions found.\n");
    }
    printf("\nPress Enter to continue...");
    fclose(fp);
    getchar();
    clearScreen();
}

void viewDetails(const Account *account) {
    clearScreen();
    getchar();
    printf(" _____                                                                    _____ \n");
    printf("( ___ )------------------------------------------------------------------( ___ )\n");
    printf(" |   |                                                                    |   | \n");
    printf(" |   |    ___ _   _ _____ ___  ____  __  __    _  _____ ___ ___  _   _    |   | \n");
    printf(" |   |   |_ _| \\ | |  ___/ _ \\|  _ \\|  \\/  |  / \\|_   _|_ _/ _ \\| \\ | |   |   | \n");
    printf(" |   |    | ||  \\| | |_ | | | | |_) | |\\/| | / _ \\ | |  | | | | |  \\| |   |   | \n");
    printf(" |   |    | || |\\  |  _|| |_| |  _ <| |  | |/ ___ \\| |  | | |_| | |\\  |   |   | \n");
    printf(" |   |   |___|_| \\_|_|   \\___/|_| \\_\\_|  |_/_/   \\_\\_| |___\\___/|_| \\_|   |   | \n");
    printf(" |___|                                                                    |___| \n");
    printf("(_____)------------------------------------------------------------------(_____)\n\n");
    printf("Owner Name: %s\n", account->ownerName);
    printf("Father's Name: %s\n", account->fathersName);
    printf("Age: %d\n", account->age);
    printf("Date of Birth: %s\n", account->dob);
    printf("PAN Number: %s\n", account->panNumber);
    printf("Account Number: %d\n", account->accountNumber);
    printf("Total Balance: %.2lf\n", account->balance);
    printf("\n\nPress any key to continue...");
    getchar();
    clearScreen();
}

void closeAccount(Account *account) {
    clearScreen();
    printf(" _____                                                _____ \n");
    printf("( ___ )----------------------------------------------( ___ )\n");
    printf(" |   |                                                |   | \n");
    printf(" |   |     ____ _     ___  ____ ___ _   _  ____       |   | \n");
    printf(" |   |    / ___| |   / _ \\/ ___|_ _| \\ | |/ ___|      |   | \n");
    printf(" |   |   | |   | |  | | | \\___ \\| ||  \\| | |  _       |   | \n");
    printf(" |   |   | |___| |__| |_| |___) | || |\\  | |_| |      |   | \n");
    printf(" |   |    \\____|_____\\___/|____/___|_| \\_|\\____|      |   | \n");
    printf(" |   |       _    ____ ____ ___  _   _ _   _ _____    |   | \n");
    printf(" |   |      / \\  / ___/ ___/ _ \\| | | | \\ | |_   _|   |   | \n");
    printf(" |   |     / _ \\| |  | |  | | | | | | |  \\| | | |     |   | \n");
    printf(" |   |    / ___ \\ |__| |__| |_| | |_| | |\\  | | |     |   | \n");
    printf(" |   |   /_/   \\_\\____\\____\\___/ \\___/|_| \\_| |_|     |   | \n");
    printf(" |___|                                                |___| \n");
    printf("(_____)----------------------------------------------(_____)\n\n");

    if (account->balance > 0) {
        int targetAccountNumber;
        while (1) {
            printf("Your account has a balance of %.2lf. Enter target account number to transfer funds (or '0' to cancel): ", account->balance);
            scanf("%d", &targetAccountNumber);

            if (targetAccountNumber == 0) {
                printf("Transfer cancelled. Returning to Dashboard...\n");
                dashboard(account);
                return;
            }

            FILE *fp = fopen("accounts.dat", "rb+");
            if (fp == NULL) {
                printf("Error opening file!\n");
                return;
            }

            Account temp;
            int found = 0;
            while (fread(&temp, sizeof(Account), 1, fp)) {
                if (temp.accountNumber == targetAccountNumber) {
                    found = 1;
                    temp.balance += account->balance;
                    fseek(fp, -sizeof(Account), SEEK_CUR);
                    fwrite(&temp, sizeof(Account), 1, fp);

                    // Record the transaction for both accounts
                    recordTransaction(account->accountNumber, "Account Closed - Transfer Out", -account->balance);
                    recordTransaction(temp.accountNumber, "Funds Received from Closed Account", account->balance);

                    account->balance = 0;
                    printf("Funds transferred successfully! Press any key to continue...");
                    getchar();
                    getchar();  // To consume the newline character left by scanf
                    break;
                }
            }
            fclose(fp);

            if (found) {
                break;
            } else {
                printf("Target account number not found. Please try again.\n");
            }
        }
    }

    // Read all accounts into memory except the one to be closed
    Account accounts[MAX_ACCOUNTS];
    int accountCount = 0;

    FILE *fp = fopen("accounts.dat", "rb");
    if (fp == NULL) {
        printf("Error opening file!\n");
        return;
    }

    while (fread(&accounts[accountCount], sizeof(Account), 1, fp)) {
        if (accounts[accountCount].accountNumber != account->accountNumber) {
            accountCount++;
        }
    }
    fclose(fp);

    // Write the remaining accounts back to the file
    fp = fopen("accounts.dat", "wb");
    if (fp == NULL) {
        printf("Error opening file!\n");
        return;
    }

    for (int i = 0; i < accountCount; i++) {
        fwrite(&accounts[i], sizeof(Account), 1, fp);
    }
    fclose(fp);

    clearScreen();
    printf("Account closed successfully.\n");
}

void recordTransaction(int accountNumber, const char *description, double amount) {
    FILE *fp = fopen("transactions.dat", "ab");
    if (fp == NULL) {
        printf("Error opening transaction file!\n");
        return;
    }

    Transaction newTransaction;
    newTransaction.accountNumber = accountNumber;
    strncpy(newTransaction.description, description, sizeof(newTransaction.description) - 1);
    newTransaction.description[sizeof(newTransaction.description) - 1] = '\0';
    newTransaction.amount = amount;

    fwrite(&newTransaction, sizeof(Transaction), 1, fp);
    fclose(fp);
}

void saveAccount(const Account *account) {
    FILE *fp = fopen("accounts.dat", "rb+");
    if (fp == NULL) {
        printf("Error opening file!\n");
        return;
    }

    Account temp;
    while (fread(&temp, sizeof(Account), 1, fp)) {
        if (temp.accountNumber == account->accountNumber) {
            fseek(fp, -sizeof(Account), SEEK_CUR);
            fwrite(account, sizeof(Account), 1, fp);
            break;
        }
    }

    fclose(fp);
}

int loadAccounts(Account accounts[], int max) {
    FILE *fp = fopen("accounts.dat", "rb");
    if (fp == NULL) {
        return 0;
    }

    int count = 0;
    while (fread(&accounts[count], sizeof(Account), 1, fp) && count < max) {
        count++;
    }

    fclose(fp);
    return count;
}

int validateUsername(const char *username) {
    int length = strlen(username);

    // Check length requirement
    if (length < 3 || length > 20) {
        return 0;
    }

    // Check for lowercase letters only
    for (int i = 0; i < length; i++) {
        if (!islower(username[i]) && !isdigit(username[i]) && username[i] != '_') {
            return 0;
        }
    }

    return 1;
}

int validatePAN(const char *panNumber) {
    if (strlen(panNumber) != 10) return 0;
    for (int i = 0; i < 5; i++) {
        if (!isupper(panNumber[i])) return 0;
    }
    for (int i = 5; i < 9; i++) {
        if (!isdigit(panNumber[i])) return 0;
    }
    return isupper(panNumber[9]);
}

int validateOwnerName(const char *name) {
    for (int i = 0; name[i] != '\0'; i++) {
        if (!isalpha(name[i]) && name[i] != ' ') return 0;
    }
    return 1;
}

int validatePassword(const char *password) {
    if (strcmp(password, "0") == 0) {
        return -1; 
    }

    int length = strlen(password);
    int hasUpper = 0, hasLower = 0, hasDigit = 0, hasSpecial = 0;

    if (length < 8 || length > 20) {
        return 0;
    }

    for (int i = 0; i < length; i++) {
        if (isupper(password[i])) hasUpper = 1;
        if (islower(password[i])) hasLower = 1;
        if (isdigit(password[i])) hasDigit = 1;
        if (strchr("!@#$%^&*()-_=+[]{}|;:'\",.<>?/", password[i])) hasSpecial = 1;
    }

    if (hasUpper && hasLower && hasDigit && hasSpecial) {
        return 1;
    }

    return 0; 
}

void clearScreen() {
    #ifdef _WIN32
        system("cls");
    #else
        system("clear");
    #endif
}

void printRectangleBorder() {
    printf("+");
    for (int i = 0; i < SCREEN_WIDTH - 2; i++) printf("-");
    printf("+\n");
}

void printInRectangle(const char *content) {
    clearScreen();
    printRectangleBorder();
    for (int i = 0; i < SCREEN_HEIGHT - 2; i++) {
        printf("|");
        if (i == (SCREEN_HEIGHT - 2) / 2) {
            int padding = (SCREEN_WIDTH - 2 - strlen(content)) / 2;
            for (int j = 0; j < padding; j++) printf(" ");
            printf("%s", content);
            for (int j = 0; j < SCREEN_WIDTH - 2 - padding - strlen(content); j++) printf(" ");
        } else {
            for (int j = 0; j < SCREEN_WIDTH - 2; j++) printf(" ");
        }
        printf("|\n");
    }
    printRectangleBorder();
}

void getFathersName(char *fullName, size_t size) {
    char firstName[50];
    char lastName[50];
    do {
        printf("Enter Father's First Name ('0' to cancel): ");
        fgets(firstName, sizeof(firstName), stdin);
        firstName[strcspn(firstName, "\n")] = '\0';
        if (strcmp(firstName, "0") == 0) {
            strncpy(fullName, "0", size);
            return;
        }
    } while (!validateOwnerName(firstName));

    do {
        printf("Enter Father's Last Name ('0' to cancel): ");
        fgets(lastName, sizeof(lastName), stdin);
        lastName[strcspn(lastName, "\n")] = '\0';
        if (strcmp(lastName, "0") == 0) {
            strncpy(fullName, "0", size);
            return;
        }
    } while (!validateOwnerName(lastName));

    snprintf(fullName, size, "%s %s", firstName, lastName);
}

int calculateAge(int day, int month, int year) {
    time_t t = time(NULL);
    struct tm *current = localtime(&t);

    int currentYear = current->tm_year + 1900;
    int currentMonth = current->tm_mon + 1;
    int currentDay = current->tm_mday;

    int age = currentYear - year;
    if (currentMonth < month || (currentMonth == month && currentDay < day)) {
        age--;
    }
    return age;
}

int isUsernameUnique(const char *username) {
    FILE *fp = fopen("accounts.dat", "rb");
    if (fp == NULL) {
        printf("Error opening file!\n");
        return 0;
    }

    Account temp;
    while (fread(&temp, sizeof(Account), 1, fp)) {
        if (strcmp(temp.username, username) == 0) {
            fclose(fp);
            return 0;
        }
    }

    fclose(fp);
    return 1;
}

int isPanNumberUnique(const char *panNumber) {
    FILE *fp = fopen("accounts.dat", "rb");
    if (fp == NULL) {
        printf("Error opening file!\n");
        return 0;
    }

    Account temp;
    while (fread(&temp, sizeof(Account), 1, fp)) {
        if (strcmp(temp.panNumber, panNumber) == 0) {
            fclose(fp);
            return 0;
        }
    }

    fclose(fp);
    return 1;
}
