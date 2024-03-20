
Mohamed Bouzidi
101265525

Here is the video to below:
https://youtu.be/UR6C9RVqBJc


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




I am writing to inform you about an issue I'm encountering while trying to push my code to my GitHub repository for the assignment. Despite following the instructions provided and ensuring that my Git configurations are correct, I'm experiencing difficulties with the permissions when attempting to push changes to the repository.

Here are the details of the problem:

When I try to push my changes using the git push command, I receive a permission denied error (403) indicating that I do not have access to the repository.
I have checked my repository permissions and verified that my GitHub account ("mohamedbouzidi10") has the necessary permissions to push changes to the repository "MoBouzidi/a3-3005".
Additionally, I have configured my Git settings with the correct email and username, and I have tried reauthenticating Git without success.

Here is my code below and I hope you will be understanding thank you so much.



import psycopg2
from psycopg2 import sql

def create_connection():
    conn = psycopg2.connect(
        host="localhost",
        database="students_db",
        user="postgres",
        password="245883Hi"
    )
    return conn

def create_table():
    conn = create_connection()
    cur = conn.cursor()
    cur.execute("""
        CREATE TABLE IF NOT EXISTS students (
            student_id SERIAL PRIMARY KEY,
            first_name TEXT NOT NULL,
            last_name TEXT NOT NULL,
            email TEXT NOT NULL UNIQUE,
            enrollment_date DATE
        )
    """)
    conn.commit()
    cur.close()
    conn.close()

def insert_initial_data():
    initial_data = [
        ('John', 'Doe', 'john.doe@example.com', '2023-09-01'),
        ('Jane', 'Smith', 'jane.smith@example.com', '2023-09-01'),
        ('Jim', 'Beam', 'jim.beam@example.com', '2023-09-02')
    ]

    conn = create_connection()
    cur = conn.cursor()

    for data in initial_data:
        first_name, last_name, email, enrollment_date = data
        # Check if the email already exists
        cur.execute("SELECT COUNT(*) FROM students WHERE email = %s", (email,))
        if cur.fetchone()[0] == 0:
            # Insert the student data
            cur.execute(
                sql.SQL("INSERT INTO students (first_name, last_name, email, enrollment_date) VALUES (%s, %s, %s, %s)"),
                (first_name, last_name, email, enrollment_date)
            )
            print(f"Inserted data for {email}.")
        else:
            print(f"Data for {email} already exists, skipping insertion.")

    conn.commit()
    cur.close()
    conn.close()

def getAllStudents():
    conn = create_connection()
    cur = conn.cursor()
    cur.execute("SELECT * FROM students")
    rows = cur.fetchall()
    for row in rows:
        print(f"Student ID: {row[0]}, First Name: {row[1]}, Last Name: {row[2]}, Email: {row[3]}, Enrollment Date: {row[4]}")
    cur.close()
    conn.close()

def addStudent(first_name, last_name, email, enrollment_date):
    conn = create_connection()
    cur = conn.cursor()
    
    # Check if the email already exists
    cur.execute("SELECT COUNT(*) FROM students WHERE email = %s", (email,))
    if cur.fetchone()[0] == 0:
        # Insert the student data
        cur.execute(
            sql.SQL("INSERT INTO students (first_name, last_name, email, enrollment_date) VALUES (%s, %s, %s, %s)"),
            (first_name, last_name, email, enrollment_date)
        )
        conn.commit()
        print("Student added successfully.")
    else:
        print(f"Student with email '{email}' already exists.")

    cur.close()
    conn.close()

def updateStudentEmail(student_id, new_email):
    conn = create_connection()
    cur = conn.cursor()
    cur.execute(
        sql.SQL("UPDATE students SET email = %s WHERE student_id = %s"),
        (new_email, student_id)
    )
    conn.commit()
    cur.close()
    conn.close()

def deleteStudent(student_id):
    conn = create_connection()
    cur = conn.cursor()
    cur.execute(
        sql.SQL("DELETE FROM students WHERE student_id = %s"),
        (student_id,)
    )
    conn.commit()
    cur.close()
    conn.close()

# Create the students table and insert initial data
create_table()
insert_initial_data()

# Test the functions
getAllStudents()
addStudent('Test', 'User', 'test.user@example.com', '2023-09-03')
getAllStudents()
updateStudentEmail(1, 'john.doe_new@example.com')
getAllStudents()
deleteStudent(2)
getAllStudents()









