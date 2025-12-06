# parking-toll-project
#include <iostream>
#include <string>
using namespace std;

struct Record {
    string number;
    int entry;
    int exit;
    int fee;
};

int main() {
    Record r[50];      // max 50 records
    int count = 0;
    int choice;

    while (true) {
        cout << "\n===== PARKING TOLL SYSTEM =====\n";
        cout << "1. Vehicle Entry\n";
        cout << "2. Vehicle Exit\n";
        cout << "3. Show History\n";
        cout << "4. Exit\n";
        cout << "Enter choice: ";
        cin >> choice;

        // Vehicle Entry
        if (choice == 1) {
            cout << "\nEnter Vehicle Number: ";
            cin >> r[count].number;

            cout << "Enter Entry Time (0-24): ";
            cin >> r[count].entry;

            r[count].exit = -1;  // not exited yet
            r[count].fee = 0;

            cout << "Entry Added!\n";
            count++;
        }

        // Vehicle Exit
        else if (choice == 2) {
            string num;
            cout << "\nEnter Vehicle Number: ";
            cin >> num;

            bool found = false;
            for (int i = 0; i < count; i++) {
                if (r[i].number == num && r[i].exit == -1) {

                    cout << "Enter Exit Time (0-24): ";
                    cin >> r[i].exit;

                    int hours = r[i].exit - r[i].entry;
                    if (hours <= 0) hours = 1;

                    r[i].fee = hours * 50; // flat 50 Rs/hour for simplicity

                    cout << "Parking Fee: " << r[i].fee << " Rs\n";
                    found = true;
                    break;
                }
            }
            if (!found) cout << "Vehicle not found or already exited!\n";
        }

        // History
        else if (choice == 3) {
            cout << "\n---- PARKING HISTORY ----\n";
            for (int i = 0; i < count; i++) {
                cout << "Vehicle: " << r[i].number
                     << " | Entry: " << r[i].entry
                     << " | Exit: " << (r[i].exit == -1 ? 0 : r[i].exit)
                     << " | Fee: " << r[i].fee << " Rs\n";
            }
        }

        // Exit Program
        else if (choice == 4) {
            cout << "\nProgram Ended.\n";
            break;
        }

        else {
            cout << "Invalid choice!\n";
        }
    }

    return 0;
}
