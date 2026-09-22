class AssignmentSubmission:
    def __init__(self, student_name: str, student_id: str, assignment_title: str, due_date: str, is_submitted: bool, grade: float, submitted_files: list):
        self.student_name = student_name
        self.student_id = student_id
        self.assignment_title = assignment_title
        self.due_date = due_date
        self.is_submitted = is_submitted
        self.submitted_files = submitted_files
        
        if self.validate_grade_status(grade):
            self.grade = grade
        else:
            self.grade = 0.0

    def validate_grade_status(self, grade_value: float) -> bool:
        if 0.0 <= grade_value <= 100.0:
            return True
        return False

    def check_submission_status(self) -> bool:
        if len(self.submitted_files) > 0:
            self.is_submitted = True
        else:
            self.is_submitted = False
        return self.is_submitted

    def is_duplicate(self, filename: str) -> bool:
        if filename in self.submitted_files:
            return True
        return False

    def add_file(self, filename: str) -> None:
        if self.is_duplicate(filename):
            print(f"Notice: '{filename}' has already been uploaded by {self.student_name}.")
        else:
            self.submitted_files.append(filename)
            self.check_submission_status()

    def remove_file(self, filename: str) -> None:
        if filename in self.submitted_files:
            self.submitted_files.remove(filename)
        self.check_submission_status()

    def assign_grade(self, grade_value: float) -> None:
        if self.validate_grade_status(grade_value):
            self.grade = grade_value
        else:
            print(f"Error: {grade_value} is an invalid grade record for {self.student_name}.")

    def get_grade(self) -> str:
        return f"Grade: {self.grade:.1f}"

    def view_files(self) -> str:
        if not self.submitted_files:
            return "No files uploaded."
        return ", ".join(self.submitted_files)

    def get_status_report(self) -> str:
        status = "Submitted" if self.is_submitted else "Missing"
        return f"{self.student_name} ({self.student_id}) - {self.get_grade()} - Status: {status}"

if __name__ == "__main__":
    student1 = AssignmentSubmission("Pia Noe", "pshs-1090-x", "CS-101", "2026-10-01", False, 0.0, [])
    student2 = AssignmentSubmission("Glittersparkles", "pshs-1920-x", "CS-103", "2026-10-01", False, 0.0, [])

    print("---Student 1 ---")
    student1.add_file("main.py")
    student1.add_file("main.py")  
    student1.add_file("report.pdf")
    student1.assign_grade(95.5)
    print(f"Pia Noe's Files: {student1.view_files()}")
    
    print("\n---Student 2 ---")
    student2.add_file("wrong_homework.docx")
    student2.remove_file("wrong_homework.docx")
    student2.add_file("correct_project.py")
    student2.assign_grade(88.0)
    print(f"Glittersparkles's Files: {student2.view_files()}")

    print("\n---- Final System Report ----")
    print(student1.get_status_report())
    print(student2.get_status_report())
