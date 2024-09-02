#include <iostream>
#include <fstream>
#include <iomanip>
#include <string>  // Include for using std::string
#include <cstdlib> // Include for using system() function
#include <conio.h> // Windows-specific header for getch()

using namespace std;

class student
{
    int rollno;
    string name; // Use string instead of char array
    int p_marks, c_marks, m_marks, e_marks, cs_marks;
    float per;
    char grade;
    void calculate();

public:
    void showdata();
    void getdata();
    int retrollno();
};
void student::getdata()
{
    system("CLS");
    cout << "\nEnter The roll number of student: ";
    cin >> rollno;
    cin.ignore(); // Ignore newline character left in the buffer
    cout << "\nEnter The Name of Student: ";
    getline(cin, name); // Use getline for strings to allow spaces
    cout << "\nEnter The marks in physics out of 100: ";
    cin >> p_marks;
    cout << "\nEnter The marks in chemistry out of 100: ";
    cin >> c_marks;
    cout << "\nEnter The marks in maths out of 100: ";
    cin >> m_marks;
    cout << "\nEnter The marks in English out of 100: ";
    cin >> e_marks;
    cout << "\nEnter The marks in computer science out of 100: ";
    cin >> cs_marks;
    calculate();
}
void write_student()
{
    student st;
    ofstream outFile("student.dat", ios::binary | ios::app);
    
    if (!outFile) // Check if file opened successfully
    {
        cerr << "Error: Could not open file for writing!" << endl;
        return;
    }

    st.getdata();
    outFile.write(reinterpret_cast<char*>(&st), sizeof(student));

    if (!outFile) // Check if write operation was successful
    {
        cerr << "Error: Could not write to file!" << endl;
   }
    else
    {
        cout << "\n\nStudent record has been created ";
    }

    outFile.close();
    cin.ignore();
    getch();
}
int password()
{
    system("CLS");
    string pass = "";
    char ch;
    cout << "\n\n\n\n\n\n\t--------------------------------------------";
    cout << "\n\tSTUDENT REPORT CARD MANAGEMENT SYSTEM LOGIN\n";
    cout << "\t--------------------------------------------\n";
    cout << "\n\n\tEnter Password: ";

    ch = getch(); // Use getch() only if it's necessary; otherwise, consider a portable method

    while (ch != 13) // ASCII 13 is the Enter key
    {
        pass.push_back(ch);
        cout << '*'; // Mask the input
        ch = getch();
    }
    if (pass == "12345")
    {
        cout << "\n\n\n\tAccess Granted \n\n\n";
        system("PAUSE");
    }
    else
    {
        cout << "\n\n\n\tAccess Aborted...Please Try Again!\n";
        system("PAUSE");
        password();
    }
}
int main()
{
    int password();
    password();
    char ch;
    cout.setf(ios::fixed | ios::showpoint);
    cout << setprecision(2);

    do
    {
        system("CLS");
        cout << "\t--------------------------------------------";
        cout << "\n\t  STUDENT REPORT CARD MANAGEMENT SYSTEM\n";
        cout << "\t--------------------------------------------";
        cout << "\n\n\t\t**MAIN MENU**";
        cout << "\n\n\t01. RESULT MENU";
        cout << "\n\n\t02. CRUD MENU";
        cout << "\n\n\t03. EXIT";
        cout << "\n\n\tPlease Select Your Option : ";
        cin >> ch;

        switch (ch)
        {
            case '1': 
                result();
                break;
            case '2': 
                entry_menu();
                break;
            case '3':
                system("CLS");
                cout << "\n\nSTUDENT REPORT CARD MANAGEMENT SYSTEM \n\n";
                return 0;
            default:
                cout << "\n\n\tError...!!!...Wrong Choice Entered...!!!";
        }
    } while (ch != '3');

    return 0; // Explicit return statement for clarity
}
void clearConsole()
{
    #ifdef _WIN32
        system("CLS");
    #else
        system("clear");
    #endif
}


