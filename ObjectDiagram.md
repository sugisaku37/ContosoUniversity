@startuml
entity "Student" {
    + ID [PK]:int
    LastName:string
    FirstMidName:string
    EnrollmentDate:DateTime
    ==
    Enrollments:ICollection<Enrollment>
}

entity "Enrollment" {
    + EnrollmentID [PK]:int
    # CourseID [FK(Course,CourseID)]
    # StudentID [FK(Student,Id)]
    Grade:Grade?
    ==
    Course:Course
    Student:Student
}

entity "Course" {
    + CourseID [PK]:int
    Title:string
    Credits:string
    # DepartmentID [FK(Department,DepartmentID)]
    ==
    Department:Department
    Enrollments:ICollection<Enrollment>
    CourseAssignments:ICollection<CourseAssignment>
}

entity "Department" {
    + DepartmentID [PK]:int
    Name:string
    Budget:decimal
    StartDate:DateTime
    InstructorID:int?
    ==
    Administrator:Instructor
    Courses:ICollection<Course>
}

entity "CourseAssignment" {
    + InstructorID [PK]:int
    # CourseID [FK(Course,CourseID)]
    ==
    Instructor:Instructor
    Course:Course
}

entity "Instructor" {
    + ID [PK]:int
    LastName:string
    FirstMidName:string
    HireDate:DateTime
    ==
    CourseAssignments:ICollection<CourseAssignment>
    OfficeAssignment:OfficeAssignment
}

entity "OfficeAssignment" {
    + InstructorID [PK]:int
    Location:string
    ==
    Instructor:Instructor
}


Student --o{ Enrollment
Course --o{ Enrollment
Department --o{ Course
Department --|{ Instructor
Course --o{ CourseAssignment
Instructor --o{ CourseAssignment
Instructor||--||OfficeAssignment


@enduml