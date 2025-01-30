# grademanagment-system
1grade managment system
#include <stdio.h>
#include <string.h>

#define MAX_STUDENTS 100
#define MAX_SUBJECTS 5

typedef struct {
    int id;
    char name[50];
    float scores[MAX_SUBJECTS];
    float total;
    float average;
    char grade;
} Student;

Student students[MAX_STUDENTS];
int studentCount = 0;
const char *subjects[MAX_SUBJECTS] = {"Calculus", "Programming", "English", "ICT", "Physics"};

char calculateGrade(float average) {
    if (average >= 90) return 'A';
    else if (average >= 80) return 'B';
    else if (average >= 70) return 'C';
    else if (average >= 60) return 'D';
    else return 'F';
}

void addStudent() {
    if (studentCount >= MAX_STUDENTS) {
        printf("Maximum student limit reached.\n");
        return;
    }

    Student s;
    printf("Enter Student ID: ");
    scanf("%d", &s.id);
    printf("Enter Student Name: ");
    scanf(" %[^\n]", s.name);

    s.total = 0;
    for (int i = 0; i < MAX_SUBJECTS; i++) {
        printf("Enter marks for %s: ", subjects[i]);
        scanf("%f", &s.scores[i]);
        s.total += s.scores[i];
    }

    s.average = s.total / MAX_SUBJECTS;
    s.grade = calculateGrade(s.average);

    students[studentCount++] = s;
    printf("Student added successfully!\n");
}

void viewStudents() {
    if (studentCount == 0) {
        printf("No students to display.\n");
        return;
    }

    printf("\nID\tName\t\tTotal\tAverage\tGrade\n");
    printf("-----------------------------------------------\n");
    for (int i = 0; i < studentCount; i++) {
        printf("%d\t%s\t\t%.2f\t%.2f\t%c\n", 
               students[i].id, students[i].name, 
               students[i].total, students[i].average, 
               students[i].grade);
    }
}

void menu() {
    int choice;

    while (1) {
        printf("\n--- Grade Management System ---\n");
        printf("1. Add Student Grades\n");
        printf("2. View Student Grades\n");
        printf("3. Exit\n");
        printf("Enter your choice: ");
        scanf("%d", &choice);

        switch (choice) {
            case 1:
                addStudent();
                break;
            case 2:
                viewStudents();
                break;
            case 3:
                printf("Exiting..\n");
                return;
            default:
                printf("Incorrect choice. Please try again.\n");
        }
    }
}

int main() {
    menu();
    return 0;
}
