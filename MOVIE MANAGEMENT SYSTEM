#include <iostream>
#include <fstream>
#include <sstream>
#include <string>
#include <iomanip>
#include <cstdlib>  // Include cstdlib for system("CLS")
// Function to delete a movie from the file
#include <chrono>
#include <thread>

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

class Movie {
public:
    string name;
    int ratings;
    string feedback;
    bool completed;
    int hours;
    int minutes;

    Movie(const string& name, int ratings, const string& feedback, bool completed, int hours, int minutes)
        : name(name), ratings(ratings), feedback(feedback), completed(completed), hours(hours), minutes(minutes) {}
};

// Function to delete a movie from the file
void deleteMovie(const string& filename, int movieIndex);

// Function to add a movie to the file
void addMovie(const string& filename) {
    ofstream fout(filename, ios::app);

    if (!fout.is_open()) {
        cout << "Error opening file for writing!" << endl;
        return;
    }

    string name, feedback;
    int ratings;
    bool completed;
    int hours, minutes;

    cin.ignore(); // Ignore newline character from previous input
    cout << "Enter the movie name: ";
    getline(cin, name);

    cout << "Enter the ratings (1-5): ";
    cin >> ratings;

    cin.ignore(); // Consume the newline character

    cout << "Enter your feedback: ";
    getline(cin, feedback);

    cout << "Have you completed the movie? (y/n): ";
    char completionChoice;
    cin >> completionChoice;

    if (completionChoice == 'y' || completionChoice == 'Y') {
        completed = true;
        hours = 0;
        minutes = 0;
    } else {
        completed = false;
        cout << "Enter the hours where you left off: ";
        cin >> hours;

        cout << "Enter the minutes where you left off: ";
        cin >> minutes;
    }

    Movie newMovie(name, ratings, feedback, completed, hours, minutes);

    fout << newMovie.name << "|" << newMovie.ratings << "|" << newMovie.feedback << "|" << newMovie.completed << "|" << newMovie.hours << "|" << newMovie.minutes << endl;

    fout.close();
}

// Function to view movies from the file
void viewMovies(const string& filename) {
    ifstream fin(filename);

    if (!fin.is_open()) {
        cout << "Error opening file for reading!" << endl;
        return;
    }

    string line;

    int sequenceNumber = 1; // Initialize sequence number
    system("CLS");
    cout << setw(5) << "Number" << setw(40) << "Movie Name" << endl;
    cout << "-----------------------------------------------------" << endl;

    while (getline(fin, line)) {
        stringstream ss(line);
        string name, feedback;
        int ratings, hours, minutes;
        bool completed;

        getline(ss, name, '|');
        ss >> ratings;
        ss.ignore(); // Consume the delimiter
        getline(ss, feedback, '|');
        ss >> completed;
        ss.ignore(); // Consume the delimiter
        ss >> hours;
        ss.ignore(); // Consume the delimiter
        ss >> minutes;

        //Movie movie(name, ratings, feedback, completed, hours, minutes);

        // Display sequence number and movie name
        cout << setw(5) << sequenceNumber << setw(40) << name << endl;

        sequenceNumber++;
    }

    fin.close();

    int choice;

    cout << endl << endl << endl << "Enter the number of the movie to view details (0 to go back): ";
    cin >> choice;
    int dog;
    dog=choice;

    if (choice >= 1 && choice <= sequenceNumber - 1) {
        system("CLS");
        cout << "Details for movie " << choice << ":" << endl;

        // Reopen the file to move to the selected line
        fin.open(filename);

        for (int i = 1; i <= choice; ++i)
            getline(fin, line);

        stringstream ss(line);
        string name, feedback;
        int ratings, hours, minutes;
        bool completed;

        getline(ss, name, '|');
        ss >> ratings;
        ss.ignore(); // Consume the delimiter
        getline(ss, feedback, '|');
        ss >> completed;
        ss.ignore(); // Consume the delimiter
        ss >> hours;
        ss.ignore(); // Consume the delimiter
        ss >> minutes;

        Movie selectedMovie(name, ratings, feedback, completed, hours, minutes);

        cout << "Name: " << selectedMovie.name << endl;
        cout << "Ratings: " << selectedMovie.ratings << endl;
        cout << "Feedback: " << selectedMovie.feedback << endl;

        if (selectedMovie.completed) {
            cout << "Status: Completed" << endl;
        } else {
            cout << "Status: Incomplete" << endl;
            cout << "Time where you left off: " << selectedMovie.hours << " hours and " << selectedMovie.minutes << " minutes" << endl;
        }

        // Additional options for deleting and going back
        cout << endl << "Options:" << endl;
        cout << "1. Delete Movie" << endl;
        cout << "0. Go back" << endl << endl;
        cout << "Enter your choice: ";
        cin >> choice;

        switch (choice) {
            case 1:
                // Delete Movie
                deleteMovie(filename, dog);
                break;
            case 0:
                // Go back
                break;
            default:
                cout << "Invalid choice. Going back to the main menu." << endl;
        }
    } else if (choice != 0) {
        cout << "Sorry, the number isn't valid. Please try again." << endl;
    }
}

void deleteMovie(const string& filename, int movieIndex) {
    fstream file(filename, ios::in | ios::out);

    if (!file.is_open()) {
        cout << "Error opening file for reading and writing!" << endl;
        return;
    }

    ofstream fout("temp.txt");

    if (!fout.is_open()) {
        cout << "Error opening temporary file for writing!" << endl;
        file.close();
        return;
    }

    string line;
    int currentLine = 1;

    // Copy all lines except the one to be deleted to the temporary file
    while (getline(file, line)) {
        if (currentLine != movieIndex) {
            fout << line << endl;
        }
        currentLine++;
    }

    file.clear();  // Clear the end-of-file flag
    file.seekg(0, ios::beg);  // Move the file pointer back to the beginning

    fout.close();

    // Introduce a short delay
    this_thread::sleep_for(chrono::milliseconds(100));

    // Overwrite the original file with the content of the temporary file
    ofstream fileOut(filename, ios::trunc);
    ifstream tempIn("temp.txt");

    if (fileOut && tempIn) {
        fileOut << tempIn.rdbuf();
        cout << "Movie successfully deleted." << endl;
    } else {
        cout << "Error overwriting file" << endl;
    }

    tempIn.close();
}

void console() {

    int choice;
    char continueChoice;

    do {
        cout << "Select language:" << endl;
        cout << "1. Bollywood" << endl;
        cout << "2. Hollywood" << endl;
        cout << "3. Nepali" << endl;
        cout << "0. Exit" << endl << endl << endl;
        cout << "Enter your choice: ";
        cin >> choice;

        if (choice >= 1 && choice <= 3) {
            string filename;

            switch (choice) {
                case 1:
                    filename = "bollywood.txt";
                    break;
                case 2:
                    filename = "hollywood.txt";
                    break;
                case 3:
                    filename = "nepali.txt";
                    break;
            }

            do {
                system("CLS");
                string filmindustry;
                filmindustry = filename.substr(0, filename.length() - 4);
                cout << filmindustry << endl << endl;
                cout << "Options:" << endl;
                cout << "1. Add Movie" << endl;
                cout << "2. View Movies" << endl;
                cout << "0. Go back to language selection" << endl << endl << endl;
                cout << "Enter your choice: ";
                int noice;
                cin >> noice;

                switch (noice) {
                    case 1:
                        addMovie(filename);
                        break;
                    case 2:
                        viewMovies(filename);
                        break;
                    case 0:
                        break; // Go back to language selection
                    default:
                        cout << "Invalid choice. Please try again." << endl;
                }
            if(noice==0)break;
                cout << endl << endl << "Do you want to continue for " << filmindustry << "? (y/n): ";
                cin >> continueChoice;
            } while (continueChoice == 'y' || continueChoice == 'Y');
        } else if (choice != 0) {
            cout << "Invalid choice. Please try again." << endl;
        }
    } while (choice != 0);

    cout << "Exiting program." << endl;


}


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
        system("CLS");
       console();


    } else {
        cout << "Invalid username or password. Login failed.\n";
    }

    return 0;
}
