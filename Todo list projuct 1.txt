todo_list = []

def display_menu():
  print("Menu:")
  print("1. Add a new task")
  print("2. View all tasks")
  print("3. Mark a task as Done")
  print("4. Update a task")
  print("5. Remove a task")
  print("6. Exit")
  print()

def add_task():
  task_name = input("Enter the task name: ")
  due_date = input("Enter the Due Date: ")
  todo_list.append({"Task": task_name, "Status": "not Done", "Due Date": due_date})
  print("Task added successfully\U0001F44D")
  print()

def view_task():
    sorted_list = sorted(todo_list, key=lambda x: x.get("Due Date", ""))
    print("\u2605")
    print("-" * 98)
    print("| {:<5} | {:<50} | {:<20} | {:<10} |".format("Slno", "Task", "Due Date", "Status"))
    print("=" * 98)

    for i, task in enumerate(sorted_list, start=1):
        task_description = task["Task"]
        status = "Done" if task.get("Status") == "Done" else "not Done"
        due_date = task.get("Due Date", "")

        print("| {:<5} | {:<50} | {:<20} | {:<10} |".format(i, task_description, due_date, status))

    print("-" * 98)
    print()

def mark_task():
    view_task()
    task_number = int(input("Enter the task Slno to mark as done: "))

    if 1 <= task_number <= len(todo_list):
        sorted_list = sorted(todo_list, key=lambda x: x.get("Due Date", ""))
        marked_task = sorted_list[task_number - 1]
        marked_task["Status"] = "Done"
        print(f"Task '{marked_task['Task']}' marked as Done \u2705")
    else:
        print("Invalid task number\U0001F634")
    print()



def update_task():
    view_task()
    task_number = int(input("Enter the task Slno to update: "))

    if 1 <= task_number <= len(todo_list):
        sorted_list = sorted(todo_list, key=lambda x: x.get("Due Date", ""))
        task = sorted_list[task_number - 1]

        new_description = input("Enter new task description (press Enter to keep the same): ")
        new_date = input("Enter new Due Date (press Enter to keep the same): ")

        if new_description:
            task["Task"] = new_description
        if new_date:
            task["Due Date"] = new_date

        print("Task updated successfully\U0001F44D")
    else:
        print("Invalid task number\U0001F613")
    print()

def remove_task():
    view_task()
    task_number = int(input("Enter the task Slno to remove: "))

    if 1 <= task_number <= len(todo_list):
        removed_task = todo_list.pop(task_number - 1)
        print(f"Task '{removed_task['Task']}' removed successfully\U0001F44D.")
    else:
        print("Invalid task number\U0001F644.")
    print()

def exit_task():
    print("Thanks for using the todo list program. Bye!\U0001F607")

display_menu()

while True:
    choice = input("Enter the task number : ")

    if choice == "6":
        break

    try:
        choice = int(choice)

        if choice == 1:
            add_task()
        elif choice == 2:
            view_task()
        elif choice == 3:
            mark_task()
        elif choice == 4:
            update_task()
        elif choice == 5:
            remove_task()
        else:
            print("Invalid choice. Choose the correct task number\U0001F611.")
            print()
    except ValueError:
        print("Invalid input. Please enter a number\U0001F635.")
        print()

exit_task()
