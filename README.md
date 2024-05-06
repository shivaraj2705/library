# to-do list
this is my first repository <br> name = shivaraj


#include <stdio.h>
#include <string.h>
#define MAX_TASKS 100
#define MAX_DESCRIPTION_LENGTH 100

struct Task {
    char description[MAX_DESCRIPTION_LENGTH];
    int completed;
};
struct Task tasks[MAX_TASKS];
int numTasks = 0;
void addTask();
void displayTasks();
void markTaskCompleted();
void deleteTask();

int main() {
    int choice;

    do {
        printf("\nTo-Do List\n");
        printf("1. Add Task\n");
        printf("2. Display All Tasks\n");
        printf("3. Mark Task as Completed\n");
        printf("4. Delete Task\n");
        printf("5. Exit\n");
        printf("Enter your choice: ");
        scanf("%d", &choice);

        switch(choice) {
            case 1:
                addTask();
                break;
            case 2:
                displayTasks();
                break;
            case 3:
                markTaskCompleted();
                break;
            case 4:
                deleteTask();
                break;
            case 5:
                printf("Exiting program...\n");
                break;
            default:
                printf("Invalid choice. Please try again.\n");
        }
    } while(choice != 5);

    return 0;
}

void addTask() {
    if (numTasks == MAX_TASKS) {
        printf("To-Do List is full. Cannot add more tasks.\n");
        return;
    }

    struct Task newTask;
    printf("Enter description of the task: ");
    scanf(" %[^\n]", newTask.description);
    newTask.completed = 0;

    tasks[numTasks] = newTask;
    numTasks++;

    printf("Task added successfully.\n");
}

void displayTasks() {
    if (numTasks == 0) {
        printf("No tasks in the To-Do List.\n");
        return;
    }

    printf("To-Do List:\n");
    for (int i = 0; i < numTasks; i++) {
        printf("%d. [%s] %s\n", i+1, tasks[i].completed ? "X" : " ", tasks[i].description);
    }
}

void markTaskCompleted() {
    if (numTasks == 0) {
        printf("No tasks in the To-Do List.\n");
        return;
    }

    int taskNumber;
    printf("Enter the number of the task to mark as completed: ");
    scanf("%d", &taskNumber);

    if (taskNumber < 1 || taskNumber > numTasks) {
        printf("Invalid task number.\n");
        return;
    }

    tasks[taskNumber - 1].completed = 1;
    printf("Task marked as completed.\n");
}

void deleteTask() {
    if (numTasks == 0) {
        printf("No tasks in the To-Do List.\n");
        return;
    }

    int taskNumber;
    printf("Enter the number of the task to delete: ");
    scanf("%d", &taskNumber);

    if (taskNumber < 1 || taskNumber > numTasks) {
        printf("Invalid task number.\n");
        return;
    }

    for (int i = taskNumber - 1; i < numTasks - 1; i++) {
        tasks[i] = tasks[i + 1];
    }
    numTasks--;

    printf("Task deleted successfully.\n");
}
