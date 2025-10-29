# college_event_system.py

class Event:
    def init(self, event_id, title, date, description):
        self.event_id = event_id
        self.title = title
        self.date = date
        self.description = description

    def str(self):
        return f"{self.event_id} | {self.title} | {self.date} | {self.description}"

class Student:
    def init(self, name, email, event_id):
        self.name = name
        self.email = email
        self.event_id = event_id

    def str(self):
        return f"{self.name} | {self.email} | Event ID: {self.event_id}"

EVENT_FILE = "events.txt"
REG_FILE = "registrations.txt"

def add_event():
    eid = input("Enter Event ID: ")
    title = input("Enter Event Title: ")
    date = input("Enter Event Date (YYYY-MM-DD): ")
    desc = input("Enter Description: ")
    event = Event(eid, title, date, desc)
    with open(EVENT_FILE, "a") as f:
        f.write(str(event) + "\n")
    print("✅ Event added successfully!")

def view_events():
    print("\n📅 All Events:")
    try:
        with open(EVENT_FILE, "r") as f:
            events = f.readlines()
            if not events:
                print("No events found.")
            for line in events:
                print(line.strip())
    except FileNotFoundError:
        print("No events file found.")

def register_student():
    name = input("Enter Student Name: ")
    email = input("Enter Email: ")
    eid = input("Enter Event ID to register: ")
    student = Student(name, email, eid)
    with open(REG_FILE, "a") as f:
        f.write(str(student) + "\n")
    print("✅ Registration successful!")

def view_registrations():
    print("\n🧑‍🎓 All Registrations:")
    try:
        with open(REG_FILE, "r") as f:
            regs = f.readlines()
            if not regs:
                print("No registrations found.")
            for line in regs:
                print(line.strip())
    except FileNotFoundError:
        print("No registrations file found.")

def menu():
    while True:
        print("\n📘 College Event Management System")
        print("1. Add Event")
        print("2. View Events")
        print("3. Register Student")
        print("4. View Registrations")
        print("5. Exit")
        choice = input("Choose an option: ")

        if choice == "1":
            add_event()
        elif choice == "2":
            view_events()
        elif choice == "3":
            register_student()
        elif choice == "4":
            view_registrations()
        elif choice == "5":
            print("👋 Exiting system. Goodbye!")
            break
        else:
            print("❌ Invalid choice. Try again.")

if name == "main":
    menu()
