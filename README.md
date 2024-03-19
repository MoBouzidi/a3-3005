How to Compile and Run the Application
Prerequisites:

Ensure that you have Python installed on your system. You can download it from the official Python website.
Install the psycopg2 library, which is required for PostgreSQL database interaction. You can install it using pip:
pip install psycopg2

Setting up the PostgreSQL Database:
Install PostgreSQL on your system if you haven't already. You can download it from the official PostgreSQL website.
Create a new PostgreSQL database named students_db.
Use the provided schema to create the students table within the students_db database. You can execute the provided SQL script using a PostgreSQL database management tool like pgAdmin or by running it via the command line.
Running the Application:

Clone or download this repository to your local machine.
Open a terminal or command prompt and navigate to the directory where you have saved the repository.
Run the Python script a3.py using the following command:
python a3.py

Executing Each Function
getAllStudents():

This function retrieves and displays all records from the students table in the PostgreSQL database.
addStudent(first_name, last_name, email, enrollment_date):

To add a new student record, call the addStudent function and provide the required parameters: first name, last name, email, and enrollment date.
updateStudentEmail(student_id, new_email):

To update the email address for a student, call the updateStudentEmail function and provide the student ID and the new email address.
deleteStudent(student_id):

To delete a student record, call the deleteStudent function and provide the student ID of the record to be deleted.
