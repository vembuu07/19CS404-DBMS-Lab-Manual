# Experiment 7: PL/SQL – Variables, Control Structures and Loops

## AIM
To write and execute simple PL/SQL programs using variables, loops, and conditional statements.


## THEORY

PL/SQL, which stands for Procedural Language extensions to the Structured Query Language (SQL). It is a combination of SQL along with the procedural features of programming languages.

**Syntax:**
```sql
DECLARE 
   <declarations section> 
BEGIN 
   <executable command(s)>
EXCEPTION 
   <exception handling> 
END;
```

### Basic Components of PL/SQL Block:
- DECLARE: Section to declare variables and constants.
- BEGIN: The execution section that contains PL/SQL statements.
- EXCEPTION: Handles errors or exceptions that occur in the program.
- END: Marks the end of the PL/SQL block.

# PL/SQL Programs – Steps and Expected Output

## 1. Write a PL/SQL program to find the Greatest of Two Numbers

### Steps:
- Declare two numeric variables and initialize them.
- Use an `IF` statement to compare the values.
- Display the greater number using `DBMS_OUTPUT.PUT_LINE`.

#### Program:

```
DECLARE
    a NUMBER := 50;
    b NUMBER := 80;
BEGIN
    IF a > b THEN
        DBMS_OUTPUT.PUT_LINE('Greater number is: ' || a);
    ELSE
        DBMS_OUTPUT.PUT_LINE('Greater number is: ' || b);
    END IF;
END;
```


**Expected Output:**  
Greater number is: 80

![op1](https://github.com/user-attachments/assets/bf3a9d16-c93f-44c4-a3d3-7c86035b72a0)

![op1](https://github.com/user-attachments/assets/037f5706-b092-4ec2-b8be-100a0f9be16f)


---

## 2. Write a PL/SQL program to Calculate Sum of First N Natural Numbers

### Steps:
- Declare a variable `n` and assign a value (e.g., 10).
- Initialize a `sum` variable to 0.
- Use a `WHILE` loop to iterate from 1 to `n`, adding each number to the sum.
- Display the result using `DBMS_OUTPUT.PUT_LINE`.


#### Program:
```
DECLARE
    n NUMBER := 10;
    i NUMBER := 1;
    sum NUMBER := 0;
BEGIN
    WHILE i <= n LOOP
        sum := sum + i;
        i := i + 1;
    END LOOP;
    DBMS_OUTPUT.PUT_LINE('Sum of first ' || n || ' natural numbers is: ' || sum);
END;
```


**Expected Output:**  
Sum of first 10 natural numbers is: 55
![op2](https://github.com/user-attachments/assets/5c8fc36e-ff88-46bc-b7a4-caeb0043508f)

![op2](https://github.com/user-attachments/assets/77897a77-73c1-4b58-87c9-69b415e18b4d)

---

## 3. Write a PL/SQL program to generate Fibonacci series

### Steps:
- Declare the variable `n` to indicate how many terms to generate.
- Initialize the first two Fibonacci numbers (0 and 1).
- Use a loop to generate the next terms using the formula `c = a + b`.
- Print each term in the series.

#### Program:
```
DECLARE
    n NUMBER := 7;
    a NUMBER := 0;
    b NUMBER := 1;
    c NUMBER;
    i NUMBER := 3;
BEGIN
    DBMS_OUTPUT.PUT_LINE('Fibonacci sequence:');
    DBMS_OUTPUT.PUT_LINE(a);
    DBMS_OUTPUT.PUT_LINE(b);
    WHILE i <= n LOOP
        c := a + b;
        DBMS_OUTPUT.PUT_LINE(c);
        a := b;
        b := c;
        i := i + 1;
    END LOOP;
END;
```

**Expected Output:**  
n = 7  
Fibonacci sequence: 0, 1, 1, 2, 3, 5, 8
![op3](https://github.com/user-attachments/assets/0c7d6b8b-7c84-48ca-84ed-b9a3d1fa704b)
![op3](https://github.com/user-attachments/assets/98573579-a3d8-4754-a7e7-6bdf8c1ca843)

---

## 4. Write a PL/SQL Program to display the number in Reverse Order

### Steps:
- Declare a variable `n` and assign a value (e.g., 1535).
- Use a loop to extract each digit using modulo and reverse the number.
- Display the reversed number.

#### Program:
```
DECLARE
    n NUMBER := 1535;
    rev NUMBER := 0;
    r NUMBER;
    temp NUMBER := n;
BEGIN
    WHILE temp > 0 LOOP
        r := MOD(temp, 10);
        rev := rev * 10 + r;
        temp := FLOOR(temp / 10);
    END LOOP;
    DBMS_OUTPUT.PUT_LINE('Reversed number is: ' || rev);
END;
```

**Expected Output:**  
n = 1535  
Reversed number is 5351
![op4](https://github.com/user-attachments/assets/9eda37b7-4b0f-4f8d-92bd-d5c3e0521dde)
![op4](https://github.com/user-attachments/assets/ef170dab-e411-4b55-b4ce-2984881e139f)

---

## 5. Write a PL/SQL program to find the largest of three numbers

### Steps:
- Declare three numeric variables `a`, `b`, and `c`.
- Use nested `IF-ELSIF-ELSE` conditions to find the largest among the three.
- Display the largest number.

#### Program:
```
DECLARE
    a NUMBER := 10;
    b NUMBER := 9;
    c NUMBER := 15;
    max NUMBER;
BEGIN
    IF a >= b AND a >= c THEN
        max := a;
    ELSIF b >= a AND b >= c THEN
        max := b;
    ELSE
        max := c;
    END IF;
    DBMS_OUTPUT.PUT_LINE('Largest of three number is ' || max);
END;
```



**Expected Output:**  
a = 10, b = 9, c = 15  
Largest of three number is 15
![op5](https://github.com/user-attachments/assets/9db2e363-56cc-4657-aab9-9ac371a72d14)
![op5](https://github.com/user-attachments/assets/f9194e7d-cad7-49fb-8e3d-6f7dbb052e52)

---
## RESULT
Thus, the PL/SQL programs using variables, conditionals, and loops were executed successfully.
