class ToDoList:
    def __init__(self):
        self.tasks = []

    def add_task(self, task):
        self.tasks.append({'task': task, 'completed': False})
        print(f"Added task: {task}")

    def mark_completed(self, task_number):
        if 0 <= task_number < len(self.tasks):
            self.tasks[task_number]['completed'] = True
            print(f"Marked task {task_number} as completed.")
        else:
            print("Invalid task number.")

    def remove_completed_tasks(self):
        self.tasks = [task for task in self.tasks if not task['completed']]
        print("Removed all completed tasks.")

    def view_tasks(self):
        if not self.tasks:
            print("No tasks available.")
        else:
            for i, task in enumerate(self.tasks):
                status = "Completed" if task['completed'] else "Not Completed"
                print(f"{i}: {task['task']} - {status}")


def main():
    todo_list = ToDoList()

    while True:
        print("\nTo-Do List Application")
        print("1. Add Task")
        print("2. Mark Task as Completed")
        print("3. Remove Completed Tasks")
        print("4. View Tasks")
        print("5. Exit")

        choice = input("Enter your choice: ")

        if choice == '1':
            task = input("Enter the task: ")
            todo_list.add_task(task)
        elif choice == '2':
            task_number = int(input("Enter the task number to mark as completed: "))
            todo_list.mark_completed(task_number)
        elif choice == '3':
            todo_list.remove_completed_tasks()
        elif choice == '4':
            todo_list.view_tasks()
        elif choice == '5':
            print("Exiting the application.")
            break
        else:
            print("Invalid choice. Please try again.")


if __name__ == "__main__":
    main()
