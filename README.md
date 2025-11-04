# To-do-list-using-c-
/**
 * PROJECT: TO-DO LIST (C LANGUAGE)
 * --------------------------------
 * This mini project helps to add, view, mark, and delete
 * daily tasks like a simple to-do list app.
 * 
 * Completed by :NANDANI SINGH 
 * Course: BCA AI
 * 
 * NOTE:
 * This program is made in a simple way to help beginners 
 * understand how arrays, structures, and functions work in C.
 **/

#include <stdio.h>    // used for input/output functions like printf, scanf
#include <stdlib.h>   // used for system() and other general functions
#include <string.h>   // used for string handling (like strcpy, strcmp)


// -------------------------------------------
// Step 1: Create a structure (custom datatype)
// -------------------------------------------
// "struct" keyword lets us group different data types together.
// Here, we use it to store information about each task.
struct Task {
    char description[100];  // a string to store what the task is
    int completed;          // 1 means done, 0 means not done yet
};

// -------------------------------------------
// Step 2: Declare variables globally
// -------------------------------------------
struct Task tasks[100];  // array to hold up to 100 tasks
int taskCount = 0;       // to keep track of how many tasks we added


// -------------------------------------------
// Function to add a new task
// -------------------------------------------
void addTask() {
    // "if" checks if our list is already full
    if (taskCount >= 100) {
        printf("\nSorry! Task list is full.\n");
        return;  // exit the function early
    }

    printf("\nEnter your new task: ");
    getchar(); // to clear leftover newline character from input buffer
    fgets(tasks[taskCount].description, 100, stdin);  // read full line as task

    // remove newline from fgets (common beginner issue)
    tasks[taskCount].description[strcspn(tasks[taskCount].description, "\n")] = '\0';

    // set task as not completed by default
    tasks[taskCount].completed = 0;

    taskCount++;  // increase task count after adding
    printf("✅ Task added successfully!\n");
}


// -------------------------------------------
// Function to view all tasks
// -------------------------------------------
void viewTasks() {
    if (taskCount == 0) {
        printf("\nNo tasks to show. Add something first!\n");
        return;
    }

    printf("\n------ TO-DO LIST ------\n");
    for (int i = 0; i < taskCount; i++) {
        // Here we use a ternary operator ? :
        // It’s like saying “if completed is true, print X else print space”
        printf("%d. [%c] %s\n", i + 1, tasks[i].completed ? 'X' : ' ', tasks[i].description);
    }
}


// -------------------------------------------
// Function to mark a task as completed
// -------------------------------------------
void markCompleted() {
    if (taskCount == 0) {
        printf("\nNo tasks available yet.\n");
        return;
    }

    int taskNum;
    printf("\nEnter task number to mark as completed: ");
    scanf("%d", &taskNum);

    // Check if user entered a valid number
    if (taskNum < 1 || taskNum > taskCount) {
        printf("❌ Invalid task number!\n");
        return;
    }

    // Mark the selected task as completed
    tasks[taskNum - 1].completed = 1;
    printf("✅ Task marked as completed!\n");
}


// -------------------------------------------
// Function to delete a specific task
// -------------------------------------------
void deleteTask() {
    if (taskCount == 0) {
        printf("\nNo tasks to delete.\n");
        return;
    }

    int taskNum;
    printf("\nEnter task number to delete: ");
    scanf("%d", &taskNum);

    if (taskNum < 1 || taskNum > taskCount) {
        printf("❌ Invalid task number!\n");
        return;
    }

    // Shift all tasks one step up to fill the deleted spot
    for (int i = taskNum - 1; i < taskCount - 1; i++) {
        tasks[i] = tasks[i + 1];
    }

    taskCount--;  // decrease task count
    printf("🗑️ Task deleted successfully!\n");
}


// -------------------------------------------
// Function to show main menu
// -------------------------------------------
void showMenu() {
    printf("\n==============================");
    printf("\n     SIMPLE TO-DO LIST APP     ");
    printf("\n==============================");
    printf("\n1. Add Task");
    printf("\n2. View Tasks");
    printf("\n3. Mark Task as Completed");
    printf("\n4. Delete Task");
    printf("\n5. Exit");
    printf("\n------------------------------");
    printf("\nEnter your choice: ");
}


// -------------------------------------------
// MAIN FUNCTION (Program starts here)
// -------------------------------------------
// "int main()" is where the program begins.
// It keeps showing the menu until user exits.
int main() {
    int choice;  // variable to store user’s menu choice

    while (1) {  // infinite loop until user chooses Exit
        showMenu();
        scanf("%d", &choice);

        switch (choice) {  // switch is used to handle multiple options easily
            case 1:
                addTask();
                break;
            case 2:
                viewTasks();
                break;
            case 3:
                markCompleted();
                break;
            case 4:
                deleteTask();
                break;
            case 5:
                printf("\nThank you for using this To-Do List! 😊\n");
                exit(0);  // exit the program
            default:
                printf("\n⚠️ Invalid choice! Please try again.\n");
        }
    }

    return 0; // program ends successfully
}
