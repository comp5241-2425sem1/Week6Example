Imagine a system with users and courses.
Let's define the user and course classes.
```python
class User:
    def __init__(self, name, login_name, password):
        self.name = name
        self.courses = []
        self.login_name = login_name
        self.password = password
    
    def set_password(self, password):
        self.password = password

    def enroll(self, course):
        self.courses.append(course)

class Course:
    def __init__(self, name,id):
        self.id = id # COMP5241
        self.name = name # Software Engineering and Development
        self.students = []

    def add_student(self, student):
        self.students.append(student)


# Create a user
user1 = User("Alice") # instantiate an object of User class
user2 = User("Bob")

print(user1.name) # Alice

comp5241_course = Course("Software Engineering and Development", "COMP5241")

# enrol user1 to comp5241
user1.enroll(comp5241_course)
comp5241_course.add_student(user1)


```

In the system, there are three types of user:
- Admin
- Instructor
- Student

```python
class Admin(User):
    def __init__(self, name):
        super().__init__(name)
        self.role = "Admin"

    def add_course(self, course):
        print("add a new course") 

    def remove_course(self, course):
        print("remove a course")

class Instructor(User):
    def __init__(self, name):
        super().__init__(name)
        self.role = "Instructor"

    # add students into a course
    def add_student(self, course, student):
        course.add_student(student)
    
    # remove students from a course
    def remove_student(self, course, student):
        course.students.remove(student)

class Student(User):
    def __init__(self, name):
        super().__init__(name)
        self.role = "Student"

    def enroll(self, course):
        super().enroll(course)
        course.add_student(self)
```




```python
from abc import ABC, abstractmethod
class SocialLogin(ABC): # interface
    @abstractmethod
    def authenticate(self):
        pass
class FacebookLogin(SocialLogin): # concrete class that implements SocialLogin interface
    def authenticate(self):
        print("Authenticating with Facebook.")
class GoogleLogin(SocialLogin):  # concrete class that implements SocialLogin interface
    def authenticate(self):
        print("Authenticating with Google.")

class MyApp:
    def login(self, social_login SocialLo:gin):
        social_login.authenticate()

app = MyApp()
social_login = FacebookLogin()
app.login(social_login)


# Output: Authenticating with Facebook.

app.login(GoogleLogin())
# Output: Authenticating with Google.


# Allow Github Login
class GithubLogin(SocialLogin):
        def authenticate(self):
            print("Authenticating with Github.")

app.login(GithubLogin())
# Output: Authenticating with Github.
```
```

```

```python
class MyApp:
    def __init__(self, data: dict):
        self.data = data
   def save_to_db(self, db: Database):
        db.connect()
        db.save(self.data)
        db.close()
data = {"name": "John Doe", "age": 30}
app = MyApp(data)
app.save_to_db(MySQLDatabase())
app.save_to_db(MongoDB())


# An interface for database operations
class Database(ABC):
    @abstractmethod
    def connect(self):
        pass
    @abstractmethod
    def save(self, data):
        pass
    @abstractmethod
    def close(self):
        pass

# Concrete implementation for MySQL
class MySQLDatabase(Database):
    def connect(self):
        print("Connecting to MySQL database")
    def save(self, data):
        print(f"Saving data to MySQL: {data}")
    def close(self):
        print("Closing MySQL connection")

# A new class that can log the database operations for MySQLDatabase
class LoggingMySQLDatabase(MySQLDatabase):
        def connect(self):
            print("Connecting to MySQL database")   
            print("Logging the connection")

        def save(self, data):
            print(f"Saving data to MySQL: {data}")
            print("Logging the save operation")
        
        def close(self):
            print("Closing MySQL connection")
            print("Logging the close operation")

app.save_to_db(LoggingMySQLDatabase())
