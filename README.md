# To-Do-list
“A simple Python-based To-Do List application to manage tasks, set deadlines, and track completion.”
import json
tasks = []
def show_menu():
    print("\n=== To-Do List Menu ===")
    print("1. Add Task")
    print("2. View Task")
    print("3. Delete Task")
    print("4. Mark Task as Complete")
    print("5. Set Deadline")
    print("6. View Task by Deadline")
    print("7. Search Task")
    print("8. Load Task from File")
    print("9. Save Task to File")

    
def add_task():
    task_name = input("Enter the task name: ")
    task = {"name": task_name, "completed": False, "deadline": None}
    tasks.append(task)   # ✅ यहाँ tasks है (list), न कि task
    print(f"👍 Task '{task_name}' added!")


def view_tasks():
    if not tasks:
        print("🖨️ no tasks found.")
        return
    print("\n📃 All Tasks:")
    for i, task in enumerate(tasks, start=1):
        status = "✔️" if task["completed"] else"❌"
        deadline = task["deadline"] if task["deadline"] else "No deadline"
        print(f"{i}, {task['name']} [{status}] - Deadline:{deadline}")

def delete_task():
    view_tasks()
    try:
        index = int(input("Enter task number to delete: ")) - 1
        if 0 <= index < len(tasks):
            removed = tasks.pop(index)
            print(f"❌Deleted task: {removed['name']}")
        else:
            print("⚠️Invalid task number.")
    except:
        print("⚠️Please enter a valid number.")

def mark_complete():
    view_tasks()
    try:
        index = int(input("Enter task number to mark complete: ")) - 1
        if 0 <= index < len(tasks):
            tasks[index]["completed"] = True
            print(f"✅Task '{tasks[index]['name']}' marked as complete.")
        else:
            print("⚠️ Invalid task number.")
    except:
        print("⚠️ Please enter a valid number.")


def Set_deadline():
    view_tasks()
    try:
        index = int(input("Enter task number to set deadline: ")) - 1
        if 0 <= index < len(tasks):
            deadline = input("Enter deadline (e.g., 2025-07-10): ")
            tasks[index]["deadline"] = deadline
            print(f"⏰ deadline set for task: {tasks[index]['name']}")
        else:
            print("⚠️ Invalid task number.")
    except:
        print("⚠️ Please enter a valid number.")


def view_by_deadline():
    sorted_tasks = sorted(tasks, key=lambda x: (x["deadline"] is None, x["deadline"]))
    print("\n🗓️ Tasks by Deadline:")
    for i, task in enumerate(sorted_tasks, start=1):
        status = "✔️" if task["completed"] else"❌"
        deadline = task["deadline"] if task["deadline"] else "No deadline"
        print(f"{i}, {task['name']} [{status}] - Deadline:{deadline}")


def Search_task():
    keyboard = input("Enter keyboard to search: ").lower()
    found = [t for t in tasks if keyboard in t["name"].lower()]
    if not found:
        print("🔍No matching tasks found.")
    else:
        print("🔍Search Results:")
        for i, task in enumerate(found, start=1):
            status = "✔️" if task["completed"] else"❌"
            deadline = task["deadline"] if task["deadline"] else "No deadline"
            print(f"{i}, {task['name']} [{status}] - Deadline:{deadline}")

def load_tasks():
    global tasks
    try:
        with open("tasks.json", "r")as file:
            tasks = json.load(file)
            if not isinstance(tasks, list):
                tasks = []
        print("🌤️ Tasks loaded from tasks.json.")
    except FileNotFoundError:
        print("⚠️ No saved file found. Starting fresh.")
        task=[]
    
def save_tasks():
    with open("tasks.json", "w") as f:
        json.dump(tasks, f)
    print("💾 Tasks saved to tasks.json.")
if __name__ == "__main__":
    load_tasks()
    while True:
        show_menu()
        choice = input("Enter your choice:")
        if choice == '1':
            add_task()
        elif choice == '2':
            view_tasks()
        elif choice == '3':
            delete_task()
        elif choice == '4':
            mark_complete()
        elif choice == '5':
            Set_deadline()
        elif choice == '6':
            view_by_deadline()
        elif choice == '7':
            Search_task()
        elif choice == '8':
            load_tasks()
        elif choice == '9':
            save_tasks()
        else:
            print("⚠️ Invalid choice. Try again.")
    
  
        
