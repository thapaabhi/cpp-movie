#include <iostream>
#include <fstream>
#include <string>
#include <cstdlib>

using namespace std;

class User {
public:
    User() = default;

    User(const string& username, const string& password) : username(username), password(password) {}

    bool authenticate(const string& inputPassword) const {
        return (inputPassword == password);
    }

    const string& getUsername() const {
        return username;
    }

    void setUsername(const string& newUsername) {
        username = newUsername;
    }

    const string& getPassword() const {
        return password;
    }

    void setPassword(const string& newPassword) {
        password = newPassword;
    }

private:
    string username;
    string password;
};

// Function to save users to a file
void saveUsers(const User* users, int numUsers) {
    ofstream file("users.txt");

    if (file.is_open()) {
        file << numUsers << endl;

        for (int i = 0; i < numUsers; ++i) {
            file << users[i].getUsername() << " " << users[i].getPassword() << endl;
        }

        file.close();
    } else {
        cout << "Error: Unable to open the file for writing.\n";
    }
}

// Function to load users from a file
int loadUsers(User* users, int maxUsers) {
    ifstream file("users.txt");

    int numUsers = 0;

    if (file.is_open()) {
        file >> numUsers;

        for (int i = 0; i < numUsers && i < maxUsers; ++i) {
            string username, password;

            file >> username >> password;

            users[i].setUsername(username);
            users[i].setPassword(password);
        }

        file.close();
    } else {
    }

    return numUsers;
}

int main() {
    const string masterKey = "open";  // Master key to allow adding new users
    const int maxUsers = 10;  // Maximum number of users
    User users[maxUsers];
    char c;
    string inputKey;
    char yo;
    int masterKeyAttempts = 3;

    cout<<"Do you want to set new password (y/n) ";
    cin>>yo;

    if(yo=='y'){

    // Ask the user whether they know the master key
    cout << "Do you know the master key? (y/n): ";
    cin >> inputKey;

      if (inputKey == "n"){
        cout<<"Sorry you cannot sign in without knowing the masterkey"<<endl;
        cin.ignore();

        cin.get(c);
       system("cls");
      }
    if (inputKey == "y") {
        while (masterKeyAttempts > 0) {
            // Check for master key

            cout << "Enter the master key: ";
            cin >> inputKey;

            if (inputKey == masterKey) {

                   system("cls");
                cout<<"enter your new user name and password"<<endl<<endl;
                // Proceed to the section where it asks for the username and password for login

                // Load existing users from file
                int numUsers = loadUsers(users, maxUsers);

                // Allow the user to add new users
                if (numUsers < maxUsers) {
                    cout << "Enter new username: ";
                    cin >> inputKey;
                    users[numUsers].setUsername(inputKey);

                    cout << "Enter new password: ";
                    cin >> inputKey;
                    users[numUsers].setPassword(inputKey);

                    numUsers++;

                    cout << "User added successfully.\n";
                    cin.ignore();
                    cin.get(c);
                    system("cls");

                    // Save the updated user information to file
                    saveUsers(users, numUsers);
                } else {
                    cout << "Maximum number of users reached. Cannot add more users.\n";
                }

                break;  // Exit the program after adding a new user
            } else {
                cout << "Incorrect master key. " << masterKeyAttempts - 1 << " attempts remaining. Please try again.\n";
                masterKeyAttempts--;

                if (masterKeyAttempts == 0) {
                    cout << "Sorry, you couldn't provide the correct master key. Redirecting to login section.\n";
                    cin.ignore();
                    cin.get(c);
                  system("cls");
                    break;  // Proceed to the login section
                }
            }
        }
    }}

    // If the user doesn't know the master key or failed to enter it, proceed to the login section

    // Load existing users from file
    int numUsers = loadUsers(users, maxUsers);

    // Get username and password from the user
    string username, password;
    cout<<"enter your credentials"<<endl<<endl;
    cout << "Enter username: ";
    cin >> username;

    cout << "Enter password: ";
    cin >> password;

    // Authenticate the user
    bool authenticated = false;
    for (int i = 0; i < numUsers; ++i) {
        if (users[i].getUsername() == username && users[i].authenticate(password)) {
            authenticated = true;
            break;
        }
    }

    // Display the result
    if (authenticated) {
        cout << "Login successful. Welcome, " << username << "!\n";
    } else {
        cout << "Invalid username or password. Login failed.\n";
    }

    return 0;
}
