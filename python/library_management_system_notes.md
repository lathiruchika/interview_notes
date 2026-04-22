# 📚 Library Management System (OOP Project)

## 📌 Overview
The **Library Management System** is a beginner-friendly project designed to implement core **Object-Oriented Programming (OOP)** concepts such as:
- Encapsulation
- Inheritance
- Polymorphism

This system manages books, users, and borrowing transactions.

---

## 🎯 Problem Statement
Design a system that:
- Stores and manages books
- Registers users (students & faculty)
- Allows borrowing and returning of books
- Tracks all transactions

---

## 🧱 Classes Design

### 1. `Book` Class
Represents a book in the library.

**Attributes:**
- `book_id`
- `title`
- `author`
- `is_available`

**Methods:**
- `borrow_book()`
- `return_book()`

---

### 2. `User` Class (Base Class)
Represents a generic user.

**Attributes:**
- `user_id`
- `name`

**Methods:**
- `borrow_book()`
- `return_book()`

---

### 3. `Student` Class (Derived)
Inherits from `User`.

**Features:**
- Max books limit = 3

---

### 4. `Faculty` Class (Derived)
Inherits from `User`.

**Features:**
- Max books limit = 5

---

### 5. `Library` Class
Main controller class.

**Attributes:**
- `books` (list)
- `users` (list)
- `transactions` (list)

**Methods:**
- `add_book()`
- `register_user()`
- `issue_book()`
- `return_book()`

---

### 6. `Transaction` Class
Stores borrowing details.

**Attributes:**
- `transaction_id`
- `user`
- `book`
- `issue_date`
- `return_date`

---

## 🔑 OOP Concepts Used

### ✅ Encapsulation
- Data is hidden using private variables
- Access through methods

```python
class Book:
    def __init__(self, title):
        self._title = title
```

---

### ✅ Inheritance
- `Student` and `Faculty` inherit from `User`

```python
class Student(User):
    pass
```

---

### ✅ Polymorphism
- Same method behaves differently

```python
def borrow_book(self):
    if isinstance(self, Student):
        limit = 3
    else:
        limit = 5
```

---

## ⚙️ Functional Requirements

- Add books
- Register users
- Borrow books
- Return books
- Check availability
- Track transactions

---

## 🔄 Workflow

1. Add books to library  
2. Register users  
3. Issue book if available  
4. Update availability  
5. Return book  
6. Record transaction  

---

## 💡 Optional Features

- Search books
- Due dates & late fees
- File storage (JSON/CSV)
- User history tracking

---

## 🧠 Learning Outcomes

- Understand real-world use of OOP
- Practice class design
- Improve problem-solving skills
- Learn modular programming

---

## 🚀 Future Improvements

- Add GUI (Tkinter / Web)
- Database integration (MySQL)
- Admin panel
