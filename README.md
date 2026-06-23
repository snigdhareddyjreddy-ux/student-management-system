student_management_system.py
import csv
import os

FILE_NAME = "students.csv"

# Create file if it doesn't exist
if not os.path.exists(FILE_NAME):
    with open(FILE_NAME, "w", newline="") as file:
        writer = csv.writer(file)
        writer.writerow(["Roll No", "Name", "Marks"])

# Add student
def add_student():
    roll = input("Enter Roll Number: ")
    name = input("Enter Name: ")
    marks = input("Enter Marks: ")

    with open(FILE_NAME, "a", newline="") as file:
        writer = csv.writer(file)
        writer.writerow([roll, name, marks])

    print("Student Added Successfully!")

# View all students
def view_students():
    try:
        with open(FILE_NAME, "r") as file:
            reader = csv.reader(file)
            for row in reader:
                print(row)
    except FileNotFoundError:
        print("No student records found.")

# Search student
def search_student():
    roll = input("Enter Roll Number to Search: ")

    found = False

    with open(FILE_NAME, "r") as file:
        reader = csv.reader(file)

        for row in reader:
            if len(row) > 0 and row[0] == roll:
                print("Student Found:")
                print("Roll No:", row[0])
                print("Name:", row[1])
                print("Marks:", row[2])
                found = True
                break

    if not found:
        print("Student Not Found!")

# Delete student
def delete_student():
    roll = input("Enter Roll Number to Delete: ")

    rows = []
    found = False

    with open(FILE_NAME, "r") as file:
        reader = csv.reader(file)

        for row in reader:
            if len(row) > 0 and row[0] != roll:
                rows.append(row)
            else:
                found = True

    with open(FILE_NAME, "w", newline="") as file:
        writer = csv.writer(file)
        writer.writerows(rows)

    if found:
        print("Student Deleted Successfully!")
    else:
        print("Student Not Found!")

# Main Menu
while True:
    print("\n----- Student Management System -----")
    print("1. Add Student")
    print("2. View Students")
    print("3. Search Student")
    print("4. Delete Student")
    print("5. Exit")

    choice = input("Enter Choice: ")

    if choice == "1":
        add_student()
    elif choice == "2":
        view_students()
    elif choice == "3":
        search_student()
    elif choice == "4":
        delete_student()
    elif choice == "5":
        print("Thank You!")
        break
    else:
        print("Invalid Choice!")