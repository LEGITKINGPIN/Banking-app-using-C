# City Bank App

This is a console-based banking application that allows users to register, log in, manage their accounts, transfer funds, view transaction history, and more. The application is implemented in C and uses file I/O for storing account and transaction data.

## Features

- **User Registration**: Users can create a new account by providing personal details and initial deposit.
- **User Login**: Users can log in to their accounts using either their username or account number.
- **Dashboard**: After logging in, users can access various features such as transferring funds, viewing balance, viewing transaction history, and viewing account details.
- **Fund Transfer**: Users can transfer funds to another account.
- **View Balance**: Users can check their account balance after entering their password.
- **View Transaction History**: Users can view their transaction history.
- **Close Account**: Users can close their account and transfer remaining funds to another account.
- **Password Encryption**: Passwords are encrypted before storing in the file for security.
- **CSV Export**: Account details are saved in a CSV file for easy viewing and management.

## File Structure

- **main.c**: Contains the main logic and functions for the banking application.
- **accounts.dat**: Binary file used to store account information.
- **transactions.dat**: Binary file used to store transaction information.
- **accounts.csv**: CSV file used to store account information in a readable format.

## Functions

### Main Functions

- **registerUser()**: Handles user registration.
- **loginUser(Account *loggedInAccount)**: Handles user login.
- **dashboard(Account *account)**: Displays the user dashboard after login.
- **transferFunds(Account *account)**: Allows users to transfer funds to another account.
- **displayBalance(const Account *account)**: Displays the user's account balance.
- **viewTransactionHistory(const Account *account)**: Displays the user's transaction history.
- **viewDetails(const Account *account)**: Displays the user's account details.
- **closeAccount(Account *account)**: Closes the user's account and transfers remaining funds.

### Utility Functions

- **getOwnerName(char *fullName, size_t size)**: Gets the owner's full name.
- **getFathersName(char *fullName, size_t size)**: Gets the father's full name.
- **validateUsername(const char *username)**: Validates the username.
- **validatePassword(const char *password)**: Validates the password.
- **validatePAN(const char *panNumber)**: Validates the PAN number.
- **validateOwnerName(const char *name)**: Validates the owner's name.
- **encryptPassword(char *password)**: Encrypts the password.
- **decryptPassword(char *password)**: Decrypts the password.
- **clearScreen()**: Clears the console screen.
- **printRectangleBorder()**: Prints a rectangle border on the console.
- **printInRectangle(const char *content)**: Prints content inside a rectangle.
- **initializeCSV()**: Initializes the CSV file for storing account information.
- **updateCSV(const Account accounts[], int count)**: Updates the CSV file with account information.
- **generateUniqueAccountNumber(const Account accounts[], int accountCount)**: Generates a unique account number.
- **recordTransaction(int accountNumber, const char *description, double amount)**: Records a transaction.
- **saveAccount(const Account *account)**: Saves the account information to the file.
- **loadAccounts(Account accounts[], int max)**: Loads the account information from the file.
- **calculateAge(int day, int month, int year)**: Calculates the age of the user.

## Getting Started

### Prerequisites

- A C compiler (e.g., GCC)
- A terminal or command prompt

### Compilation

To compile the application, run the following command:
```bash
gcc -o city_bank main.c
```

### Running the Application

After compilation, run the application using the following command:
```bash
./city_bank
```

## Usage

1. **Register**: Create a new account by providing the necessary details.
2. **Login**: Log in using your username or account number.
3. **Dashboard**: Access various features such as transferring funds, viewing balance, viewing transaction history, and viewing account details.
4. **Close Account**: Close your account and transfer remaining funds to another account.

## Security

- Passwords are encrypted before storing in the file to ensure security.
- Users have a maximum of 3 attempts to enter the correct password before the account is locked.

## Contributing

Contributions are welcome! Please open an issue or submit a pull request for any improvements or bug fixes.


<!-- 

## Hi there 👋


**LEGITKINGPIN/LEGITKINGPIN** is a ✨ _special_ ✨ repository because its `README.md` (this file) appears on your GitHub profile.

Here are some ideas to get you started:

- 🔭 I’m currently working on ...
- 🌱 I’m currently learning ...
- 👯 I’m looking to collaborate on ...
- 🤔 I’m looking for help with ...
- 💬 Ask me about ...
- 📫 How to reach me: ...
- 😄 Pronouns: ...
- ⚡ Fun fact: ...
-->
