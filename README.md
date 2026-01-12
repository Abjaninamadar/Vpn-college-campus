# Vpn-college-campus
import json
import os

class CampusManagementSystem:
    def __init__(self):
        self.data_file = "campus_data.json"
        self.load_data()

    def load_data(self):
        if os.path.exists(self.data_file):
            with open(self.data_file, 'r') as f:
                self.data = json.load(f)
        else:
            self.data = {
                "staff": {},
                "students": {},
                "placements": {},
                "trainings": {}
            }

    def save_data(self):
        with open(self.data_file, 'w') as f:
            json.dump(self.data, f, indent=4)

    def generate_id(self, category):
        ids = list(self.data[category].keys())
        if ids:
            return max(int(id) for id in ids) + 1
        return 1

class AdministrationModule(CampusManagementSystem):
    def create_staff(self, name, role, department):
        staff_id = str(self.generate_id("staff"))
        self.data["staff"][staff_id] = {
            "name": name,
            "role": role,
            "department": department
        }
        self.save_data()
        print(f"Staff member {name} created with ID {staff_id}.")

    def read_staff(self, staff_id=None):
        if staff_id:
            if staff_id in self.data["staff"]:
                print(self.data["staff"][staff_id])
            else:
                print("Staff not found.")
        else:
            for sid, details in self.data["staff"].items():
                print(f"ID: {sid}, {details}")

    def update_staff(self, staff_id, name=None, role=None, department=None):
        if staff_id in self.data["staff"]:
            if name:
                self.data["staff"][staff_id]["name"] = name
            if role:
                self.data["staff"][staff_id]["role"] = role
            if department:
                self.data["staff"][staff_id]["department"] = department
            self.save_data()
            print(f"Staff {staff_id} updated.")
        else:
            print("Staff not found.")

    def delete_staff(self, staff_id):
        if staff_id in self.data["staff"]:
            del self.data["staff"][staff_id]
            self.save_data()
            print(f"Staff {staff_id} deleted.")
        else:
            print("Staff not found.")

class AdmissionModule(CampusManagementSystem):
    def create_student(self, name, course, year):
        student_id = str(self.generate_id("students"))
        self.data["students"][student_id] = {
            "name": name,
            "course": course,
            "year": year
        }
        self.save_data()
        print(f"Student {name} admitted with ID {student_id}.")

    def read_student(self, student_id=None):
        if student_id:
            if student_id in self.data["students"]:
                print(self.data["students"][student_id])
            else:
                print("Student not found.")
        else:
            for sid, details in self.data["students"].items():
                print(f"ID: {sid}, {details}")

    def update_student(self, student_id, name=None, course=None, year=None):
        if student_id in self.data["students"]:
            if name:
                self.data["students"][student_id]["name"] = name
            if course:
                self.data["students"][student_id]["course"] = course
            if year:
                self.data["students"][student_id]["year"] = year
            self.save_data()
            print(f"Student {student_id} updated.")
        else:
            print("Student not found.")

    def delete_student(self, student_id):
        if student_id in self.data["students"]:
            del self.data["students"][student_id]
            self.save_data()
            print(f"Student {student_id} deleted.")
        else:
            print("Student not found.")

class TrainingPlacementModule(CampusManagementSystem):
    def create_placement(self, student_id, company, role, status):
        placement_id = str(self.generate_id("placements"))
        self.data["placements"][placement_id] = {
            "student_id": student_id,
            "company": company,
            "role": role,
            "status": status
        }
        self.save_data()
        print(f"Placement created with ID {placement_id}.")

    def read_placement(self, placement_id=None):
        if placement_id:
            if placement_id in self.data["placements"]:
                print(self.data["placements"][placement_id])
            else:
                print("Placement not found.")
        else:
            for pid, details in self.data["placements"].items():
                print(f"ID: {pid}, {details}")

    def update_placement(self, placement_id, student_id=None, company=None, role=None, status=None):
        if placement_id in self.data["placements"]:
            if student_id:
                self.data["placements"][placement_id]["student_id"] = student_id
            if company:
                self.data["placements"][placement_id]["company"] = company
            if role:
                self.data["placements"][placement_id]["role"] = role
            if status:
                self.data["placements"][placement_id]["status"] = status
            self.save_data()
            print(f"Placement {placement_id} updated.")
        else:
            print("Placement not found.")

    def delete_placement(self, placement_id):
        if placement_id in self.data["placements"]:
            del self.data["placements"][placement_id]
            self.save_data()
            print(f"Placement {placement_id} deleted.")
        else:
            print("Placement not found.")

    def create_training(self, title, description, duration):
        training_id = str(self.generate_id("trainings"))
        self.data["trainings"][training_id] = {
            "title": title,
            "description": description,
            "duration": duration
        }
        self.save_data()
        print(f"Training {title} created with ID {training_id}.")

    def read_training(self, training_id=None):
        if training_id:
            if training_id in self.data["trainings"]:
                print(self.data["trainings"][training_id])
            else:
                print("Training not found.")
        else:
            for tid, details in self.data["trainings"].items():
                print(f"ID: {tid}, {details}")

    def update_training(self, training_id, title=None, description=None, duration=None):
        if training_id in self.data["trainings"]:
            if title:
                self.data["trainings"][training_id]["title"] = title
            if description:
                self.data["trainings"][training_id]["description"] = description
            if duration:
                self.data["trainings"][training_id]["duration"] = duration
            self.save_data()
            print(f"Training {training_id} updated.")
        else:
            print("Training not found.")

    def delete_training(self, training_id):
        if training_id in self.data["trainings"]:
            del self.data["trainings"][training_id]
            self.save_data()
            print(f"Training {training_id} deleted.")
        else:
            print("Training not found.")

def main():
    admin = AdministrationModule()
    admission = AdmissionModule()
    tp = TrainingPlacementModule()

    while True:
        print("\n=== College Campus Management System (VPN-Enabled for Secure Access) ===")
        print("1. Administration Operations")
        print("2. Admission Operations")
        print("3. Training & Placement Operations")
        print("4. Exit")
        choice = input("Choose a module: ")

        if choice == "1":
            while True:
                print("\n--- Administration ---")
                print("1. Create Staff")
                print("2. View Staff")
                print("3. Update Staff")
                print("4. Delete Staff")
                print("5. Back")
                sub_choice = input("Choose operation: ")
                if sub_choice == "1":
                    name = input("Name: ")
                    role = input("Role: ")
                    department = input("Department: ")
                    admin.create_staff(name, role, department)
                elif sub_choice == "2":
                    sid = input("Staff ID (leave blank for all): ")
                    admin.read_staff(sid if sid else None)
                elif sub_choice == "3":
                    sid = input("Staff ID: ")
                    name = input("New Name (leave blank to skip): ")
                    role = input("New Role: ")
                    department = input("New Department: ")
                    admin.update_staff(sid, name or None, role or None, department or None)
                elif sub_choice == "4":
                    sid = input("Staff ID: ")
                    admin.delete_staff(sid)
                elif sub_choice == "5":
                    break
                else:
                    print("Invalid choice.")

        elif choice == "2":
            while True:
                print("\n--- Admission ---")
                print("1. Admit Student")
                print("2. View Students")
                print("3. Update Student")
                print("4. Delete Student")
                print("5. Back")
                sub_choice = input("Choose operation: ")
                if sub_choice == "1":
                    name = input("Name: ")
                    course = input("Course: ")
                    year = input("Year: ")
                    admission.create_student(name, course, year)
                elif sub_choice == "2":
                    sid = input("Student ID (leave blank for all): ")
                    admission.read_student(sid if sid else None)
                elif sub_choice == "3":
                    sid = input("Student ID: ")
                    name = input("New Name: ")
                    course = input("New Course: ")
                    year = input("New Year: ")
                    admission.update_student(sid, name or None, course or None, year or None)
                elif sub_choice == "4":
                    sid = input("Student ID: ")
                    admission.delete_student(sid)
                elif sub_choice == "5":
                    break
                else:
                    print("Invalid choice.")

        elif choice == "3":
            while True:
                print("\n--- Training & Placement ---")
                print("1. Create Placement")
                print("2. View Placements")
                print("3. Update Placement")
                print("4. Delete Placement")
                print("5. Create Training")
                print("6. View Trainings")
                print("7. Update Training")
                print("8. Delete Training")
                print("9. Back")
                sub_choice = input("Choose operation: ")
                if sub_choice == "1":
                    student_id = input("Student ID: ")
                    company = input("Company: ")
                    role = input("Role: ")
                    status = input("Status: ")
                    tp.create_placement(student_id, company, role, status)
                elif sub_choice == "2":
                    pid = input("Placement ID (leave blank for all): ")
                    tp.read_placement(pid if pid else None)
                elif sub_choice == "3":
                    pid = input("Placement ID: ")
                    student_id = input("New Student ID: ")
                    company = input("New Company: ")
                    role = input("New Role: ")
                    status = input("New Status: ")
                    tp.update_placement(pid, student_id or None, company or None, role or None, status or None)
                elif sub_choice == "4":
                    pid = input("Placement ID: ")
                    tp.delete_placement(pid)
                elif sub_choice == "5":
                    title = input("Title: ")
                    description = input("Description: ")
                    duration = input("Duration: ")
                    tp.create_training(title, description, duration)
                elif sub_choice == "6":
                    tid = input("Training ID (leave blank for all): ")
                    tp.read_training(tid if tid else None)
                elif sub_choice == "7":
                    tid = input("Training ID: ")
                    title = input("New Title: ")
                    description = input("New Description: ")
                    duration = input("New Duration: ")
                    tp.update_training(tid, title or None, description or None, duration or None)
                elif sub_choice == "8":
                    tid = input("Training ID: ")
                    tp.delete_training(tid)
                elif sub_choice == "9":
                    break
                else:
                    print("Invalid choice.")

        elif choice == "4":
            print("Exiting system.")
            break
        else:
            print("Invalid choice.")

if __name__ == "__main__":
    main()
