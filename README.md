#include <iostream>
#include <string>

using namespace std;

struct CourseNode {
    string courseName;
    int marks; 
    
    CourseNode* next;
    
   
};

CourseNode* head = nullptr;

void _addNode(string name, int marks); 
void displayMenu();
void addCourseUserPrompt(); 
void viewSummary();
void cleanupMemory();


int main() {
    int choice;

    cout << "Marks Anyaliser for my iet collegues" << endl;
    cout << "To improve their further marks in upcoming exams" << endl;

    
    do {
        displayMenu();
        cout << "Enter your choice: ";
       
        cin >> choice;
        
      
        if (cin.fail() || choice < 1 || choice > 3) {
            cout << "\nInvalid choice. Please try again." << endl;
           
            cin.clear();
            cin.ignore(10000, '\n');
            continue; 
        }

        switch (choice) {
            case 1: 
                addCourseUserPrompt(); 
                break;
            case 2:
                viewSummary();
                break;
            case 3:
                cout << "\nExiting Program. Cleaning up memory..." << endl;
                break;
        }
    } while (choice != 3); 
    cleanupMemory();

    return 0;
}



void displayMenu() {
    cout << "\n=========================================" << endl;
    cout << "1. Add New Subject & Marks" << endl;
    cout << "2. View Your Performance Summary " << endl;
    cout << "3. Exit & Cleanup " << endl;
    cout << "=========================================" << endl;
}


void _addNode(string name, int marks) { 
    
    CourseNode* newNode = new CourseNode; 
    
    newNode->courseName = name;
    newNode->marks = marks;
    newNode->next = nullptr; 

    if (head == nullptr) {
       
        head = newNode;
    } else {
       
        CourseNode* current = head;
        
        while (current->next != nullptr) {
            
            current = current->next; 
        }
        
       
        current->next = newNode;
    }
}


void addCourseUserPrompt() {
    string name;
    int marks;

    
    cout << "\n--- Add New Subject ---" << endl;
    cout << "Enter Subject Name: ";
    cin.ignore(10000, '\n'); 
    getline(cin, name);
    cout << "Enter Subject Marks (0-100): ";
    cin >> marks;
    
    if (cin.fail() || marks < 0 || marks > 100) {
        cout << "Error: Invalid marks entered. Subject not added." << endl;
        cin.clear();
        cin.ignore(10000, '\n');
        return;
    }
    
   
    _addNode(name, marks);
    cout << "Subject '" << name << "' added successfully!" << endl;
}



void viewSummary() {
    if (head == nullptr) {
        cout << "\nNo subjects added yet!" << endl;
        return;
    }
    
    cout << "\n--- Your Current Subject Performance ---" << endl;
    
    int courseCount = 0;
    int totalMarksSum = 0; 
    
  
    CourseNode* current = head;

   
    cout << "\n[All Subjects:]" << endl;
    while (current != nullptr) {
        
        cout << "- " << current->courseName 
             << " - Marks: " 
             << current->marks << endl; 
             
        totalMarksSum += current->marks; 
        courseCount++;
        
       
        current = current->next;
    }
   
    double averageMark = 0.0;
    if (courseCount > 0) {
        averageMark = (double)totalMarksSum / courseCount; 
    }
    
    cout << "\n-----------------------------------------" << endl;
    cout << "Total Subjects added : " << courseCount << endl;
    cout << "you scored average Mark: " << averageMark << "%" << endl; 
    
    
    cout << "\nPERFORMANCE ANALYSIS (MARKS):" << endl;
    
    
    cout << "\n[1] EXCELLENT (Above 85% - Your Strengths):" << endl;
    current = head;
    while (current != nullptr) {
        if (current->marks > 85) {
            cout << "  -> " << current->courseName << " (" << current->marks << "%)" << endl;
        }
        current = current->next;
    }

    
    cout << "\n[2] GOOD (70% - 85% - Solid Performance):" << endl;
    current = head;
    while (current != nullptr) {
        if (current->marks >= 70 && current->marks <= 85) { 
            cout << "  -> " << current->courseName << " (" << current->marks << "%)" << endl;
        }
        current = current->next;
    }
    
    
    cout << "\n[3]  YOU NEEDS IMPROVEMENT (50% - 69% - Focus Areas):" << endl;
    current = head;
    while (current != nullptr) {
        if (current->marks >= 50 && current->marks <= 69) {
            cout << "  -> " << current->courseName << " (" << current->marks << "%)" << endl;
        }
        current = current->next;
    }

    cout << "\n[4] YOU TO WORK AND FOCUS ON THIS SUBJECT TO SCORE GOOD MARKS  (Below 50% - Urgent Review):" << endl;
    current = head;
    while (current != nullptr) {
        if (current->marks < 50) {
            cout << "  -> " << current->courseName << " (" << current->marks << "%)" << endl;
        }
        current = current->next;
    }
    
    cout << "-----------------------------------------" << endl;
}


void cleanupMemory() {
    CourseNode* current = head;
    
    while (current != nullptr) {
       
        CourseNode* nextNode = current->next;
        
       
        delete current;
        
       
        current = nextNode;
    }
    
    head = nullptr; 
    cout << "[Memory cleanup successful.]" << endl;
}
