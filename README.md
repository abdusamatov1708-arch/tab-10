# tab-10
tasks = []
completed_tasks = []


def show_statistics():
    total = len(tasks) + len(completed_tasks)
    done = len(completed_tasks)
    remaining = len(tasks)
    percentage = (done / total * 100) if total > 0 else 0

    print("\n--- Statistika ---")
    print(f"Jami vazifalar: {total}")
    print(f"Bajarilgan: {done}")
    print(f"Qolgan: {remaining}")
    print(f"Bajarilish foizi: {percentage:.1f}%")


def add_task():
    title = input("Vazifa matnini kiriting: ")
    priority = input("Muhimlik darajasi (low/medium/high): ").lower()
    while priority not in ["low", "medium", "high"]:
        print("Xato! Iltimos, low, medium yoki high deb kiriting.")
        priority = input("Muhimlik darajasi (low/medium/high): ").lower()

    tasks.append({"title": title, "priority": priority})
    print(f"'{title}' vazifasi qo'shildi.")


def complete_task():
    if not tasks:
        print("Bajariladigan vazifalar yo'q.")
        return

    print("\n--- Qolgan vazifalar ---")
    for index, task in enumerate(tasks):
        print(f"{index + 1}. {task['title']} [{task['priority'].upper()}]")

    choice = int(input("Bajarilgan vazifa raqamini kiriting: ")) - 1
    if 0 <= choice < len(tasks):
        done_task = tasks.pop(choice)
        completed_tasks.append(done_task)
        print(f"'{done_task['title']}' bajarilganlar ro'yxatiga ko'chirildi.")
    else:
        print("Noto'g'ri raqam.")


def delete_task():
    all_items = tasks + completed_tasks
    if not all_items:
        print("Ro'yxat bo'sh.")
        return

    print("\n--- Barcha vazifalar ---")
    for index, task in enumerate(all_items):
        status = "Bajarilgan" if task in completed_tasks else "Kutilmoqda"
        print(f"{index + 1}. {task['title']} [{task['priority'].upper()}] - {status}")

    choice = int(input("O'chirish uchun vazifa raqamini kiriting: ")) - 1
    if 0 <= choice < len(tasks):
        removed = tasks.pop(choice)
        print(f"'{removed['title']}' o'chirildi.")
    elif len(tasks) <= choice < len(all_items):
        removed = completed_tasks.pop(choice - len(tasks))
        print(f"'{removed['title']}' o'chirildi.")
    else:
        print("Noto'g'ri raqam.")


def sort_tasks_by_priority():
    if not tasks:
        print("Saralash uchun qolgan vazifalar yo'q.")
        return

    priority_order = {"high": 0, "medium": 1, "low": 2}
    sorted_tasks = sorted(tasks, key=lambda x: priority_order.get(x['priority'], 3))

    print("\n--- Muhimlikka qarab saralangan vazifalar ---")
    for index, task in enumerate(sorted_tasks):
        print(f"{index + 1}. {task['title']} [{task['priority'].upper()}]")


def filter_uncompleted():
    if not tasks:
        print("Bajarilmagan vazifalar mavjud emas.")
        return

    print("\n--- Bajarilmagan vazifalar ---")
    for index, task in enumerate(tasks):
        print(f"{index + 1}. {task['title']} [{task['priority'].upper()}]")


def main():
    while True:
        print("\n=== VAZIFALAR MENYUSI ===")
        print("1. Vazifa qo'shish")
        print("2. Vazifani bajarilgan deb belgilash")
        print("3. Vazifani o'chirish")
        print("4. Statistika")
        print("5. Muhimlikka qarab saralash")
        print("6. Bajarilmagan vazifalarni ko'rish")
        print("7. Chiqish")

        choice = input("Tanlovingizni kiriting (1-7): ")

        if choice == '1':
            add_task()
        elif choice == '2':
            complete_task()
        elif choice == '3':
            delete_task()
        elif choice == '4':
            show_statistics()
        elif choice == '5':
            sort_tasks_by_priority()
        elif choice == '6':
            filter_uncompleted()
        elif choice == '7':
            print("Dastur tugadi. Xayr!")
            break
        else:
            print("Noto'g'ri tanlov. Iltimos, 1 dan 7 gacha raqam kiriting.")


if __name__ == "__main__":
    main()
****
