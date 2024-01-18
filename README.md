# Phone-Directory-in-C++
code is writen in c++ using visul studio 2014.
here is main file code.
#include <iostream>
#include <string>
#include <map>

using namespace std;

class PhoneDirectory {
private:
    map<string, string> directory;

public:
    void addContact(const string& name, const string& phoneNumber) {
        directory[name] = phoneNumber;
    }

    void displayContacts() {
        cout << "Phone Directory:\n";
        for (const auto& entry : directory) {
            cout << entry.first << ": " << entry.second << endl;
        }
    }

    string getPhoneNumber(const string& name) {
        auto it = directory.find(name);
        return (it != directory.end()) ? it->second : "Contact not found";
    }

    void editContact(const string& name) {
        string newPhoneNumber;
        cout << "Enter new phone number for " << name << ": ";
        getline(cin, newPhoneNumber);
        directory[name] = newPhoneNumber;
        cout << "Contact updated successfully.\n";
    }

    void deleteContact(const string& name) {
        auto it = directory.find(name);
        if (it != directory.end()) {
            directory.erase(it);
            cout << name << "'s contact deleted successfully.\n";
        } else {
            cout << "Contact not found.\n";
        }
    }
};

int main() {
    PhoneDirectory phoneBook;

    phoneBook.addContact("John Doe", "123-456-7890");
    phoneBook.addContact("Jane Smith", "987-654-3210");
    phoneBook.addContact("Bob Johnson", "555-123-4567");

    while (true) {
        cout << "\nOptions:\n";
        cout << "1. Display Contacts\n";
        cout << "2. Search for a contact\n";
        cout << "3. Edit a contact\n";
        cout << "4. Delete a contact\n";
        cout << "5. Exit\n";
        cout << "Enter your choice (1-5): ";

        int choice;
        cin >> choice;
        cin.ignore(); // Clear the newline character from the input buffer

        switch (choice) {
            case 1:
                phoneBook.displayContacts();
                break;
            case 2: {
                cout << "Enter name to search: ";
                string searchName;
                getline(cin, searchName);
                string phoneNumber = phoneBook.getPhoneNumber(searchName);
                cout << "Phone number: " << phoneNumber << endl;
                break;
            }
            case 3: {
                cout << "Enter name to edit: ";
                string editName;
                getline(cin, editName);
                phoneBook.editContact(editName);
                break;
            }
            case 4: {
                cout << "Enter name to delete: ";
                string deleteName;
                getline(cin, deleteName);
                phoneBook.deleteContact(deleteName);
                break;
            }
            case 5:
                cout << "Exiting program.\n";
                return 0;
            default:
                cout << "Invalid choice. Please enter a number between 1 and 5.\n";
        }
    }

    return 0;
}
