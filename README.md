# Akshay_pythan

import os

TODO_FILE = "todo.txt"

def load_tasks():
    if not os.path.exists(TODO_FILE):
        return []
    with open(TODO_FILE, "r") as file:
        tasks = file.read().splitlines()
    return tasks

def save_tasks(tasks):
    with open(TODO_FILE, "w") as file:
        for task in tasks:
            file.write(task + "\n")

def show_tasks(tasks):
    if not tasks:
        print("No tasks yet!")
    else:
        print("\nYour To-Do List:")
        for i, task in enumerate(tasks, 1):
            print(f"{i}. {task}")
    print()

def main():
    tasks = load_tasks()
    
    while True:
        print("To-Do List Menu:")
        print("1. View tasks")
        print("2. Add task")
        print("3. Delete task")
        print("4. Exit")
        
        choice = input("Choose an option (1-4): ")

        if choice == "1":
            show_tasks(tasks)
        elif choice == "2":
            new_task = input("Enter the new task: ")
            tasks.append(new_task)
            save_tasks(tasks)
            print("Task added.\n")
        elif choice == "3":
            show_tasks(tasks)
            try:
                task_num = int(input("Enter task number to delete: "))
                if 1 <= task_num <= len(tasks):
                    removed = tasks.pop(task_num - 1)
                    save_tasks(tasks)
                    print(f"Removed task: {removed}\n")
                else:
                    print("Invalid task number.\n")
            except ValueError:
                print("Please enter a valid number.\n")
        elif choice == "4":
            print("Goodbye!")
            break
        else:
            print("Invalid option. Try again.\n")

if __name__ == "__main__":
    main()
