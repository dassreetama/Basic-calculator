# Basic-calculator


## Aim

Develop a simple calculator that can perform basic arithmetic operations.

## Description

Build a calculator with a graphical user interface (GUI) that allows users to perform addition, subtraction, multiplication, and division.

## Technologies

Python, Tkinter

## What You Learn

Handling user input for calculations, Basic arithmetic operations

## Code

```python
import tkinter as tk
from tkinter import messagebox

# Create the main application window
root = tk.Tk()
root.title("Simple Calculator")
root.geometry("300x400")

# Create a StringVar to hold the display content
display_text = tk.StringVar()

# Create the display entry widget
display = tk.Entry(root, textvariable=display_text, font=('Arial', 20), bd=10, insertwidth=2, width=14, borderwidth=4)
display.grid(row=0, column=0, columnspan=4)

# Function to update the display when a button is pressed
def button_click(item):
    current = display_text.get()
    display_text.set(current + str(item))

# Function to clear the display
def clear_display():
    display_text.set("")

# Function to evaluate the expression in the display
def evaluate_expression():
    try:
        result = str(eval(display_text.get()))
        display_text.set(result)
    except Exception as e:
        messagebox.showerror("Error", "Invalid Input")

# Create buttons for digits and operators
button_numbers = [
    ('7', 1, 0), ('8', 1, 1), ('9', 1, 2),
    ('4', 2, 0), ('5', 2, 1), ('6', 2, 2),
    ('1', 3, 0), ('2', 3, 1), ('3', 3, 2), ('0', 4, 1)
]

button_operators = [
    ('+', 1, 3), ('-', 2, 3),
    ('*', 3, 3), ('/', 4, 3),
    ('C', 4, 0), ('=', 4, 2)
]

# Add number buttons to the window
for (text, row, col) in button_numbers:
    button = tk.Button(root, text=text, padx=20, pady=20, font=('Arial', 18),
                       command=lambda txt=text: button_click(txt))
    button.grid(row=row, column=col)

# Add operator buttons to the window
for (text, row, col) in button_operators:
    if text == 'C':
        button = tk.Button(root, text=text, padx=20, pady=20, font=('Arial', 18),
                           command=clear_display)
    elif text == '=':
        button = tk.Button(root, text=text, padx=20, pady=20, font=('Arial', 18),
                           command=evaluate_expression)
    else:
        button = tk.Button(root, text=text, padx=20, pady=20, font=('Arial', 18),
                           command=lambda txt=text: button_click(txt))
    button.grid(row=row, column=col)

# Run the main loop
root.mainloop()
