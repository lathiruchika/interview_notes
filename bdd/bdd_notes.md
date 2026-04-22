# BDD vs TDD - Complete Notes

## 🧠 Layman Explanation

### What is BDD?

BDD (Behavior Driven Development) means: "Let's first agree what the
software should do, in simple English, before writing code."

People involved: - Developer - Tester - Business

Example: If user enters correct username and password → user should
login

------------------------------------------------------------------------

### What is TDD?

TDD (Test Driven Development) means: First write a test → then write
code to pass the test.

------------------------------------------------------------------------

## 🔥 Simple Difference

  BDD                     TDD
  ----------------------- ------------------------
  English language        Code
  User behavior           Code correctness
  Everyone understands    Developers
  Example: User logs in   assert login() == True

------------------------------------------------------------------------

## 🤝 Collaboration (Layman)

BDD ensures everyone discusses before coding.

Example: Given user has placed an order\
When user opens tracking screen\
Then user should see live location

Benefits: - No confusion - Less bugs - Clear understanding

------------------------------------------------------------------------

## 🧠 Interview Explanation

### What is BDD?

BDD is a development approach that: - Focuses on behavior - Uses Gherkin
language - Encourages collaboration

------------------------------------------------------------------------

### What is TDD?

Steps: 1. Write test 2. Fail 3. Write code 4. Pass 5. Refactor

------------------------------------------------------------------------

## 📌 Differences

  Aspect     BDD        TDD
  ---------- ---------- -------------
  Focus      Behavior   Logic
  Language   Gherkin    Programming
  Audience   All        Developers
  Level      High       Unit

------------------------------------------------------------------------

## 📚 Terminology

### Feature

High-level functionality

### Scenario

Specific use case

### Gherkin Keywords

-   Given
-   When
-   Then
-   And
-   But

------------------------------------------------------------------------

### Given / When / Then

Given → initial condition\
When → action\
Then → result

------------------------------------------------------------------------

### Step Definition

Code behind steps

------------------------------------------------------------------------

### Feature File

File with .feature extension

------------------------------------------------------------------------

### Scenario Outline

Used for multiple datasets

------------------------------------------------------------------------

### Tags

@smoke\
@regression

------------------------------------------------------------------------

## 🤝 Collaboration (Interview)

-   Common language
-   Three Amigos (Dev + QA + Business)
-   Shared understanding
-   Executable documentation
-   Less miscommunication

------------------------------------------------------------------------

## 🎯 Interview Answer

BDD is an approach where we define application behavior in a
human-readable format using Gherkin, enabling collaboration between
developers, testers, and business stakeholders, and converting those
scenarios into automated tests.
