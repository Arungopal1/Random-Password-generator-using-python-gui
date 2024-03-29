# Random-Password-generator-using-python-gui

import tkinter as tk
import string
import random

def generate_password(length, use_uppercase, use_lowercase, use_digits, use_punctuation):
    characters = ''
    if use_uppercase:
        characters += string.ascii_uppercase
    if use_lowercase:
        characters += string.ascii_lowercase
    if use_digits:
        characters += string.digits
    if use_punctuation:
        characters += string.punctuation

    if not characters:
        raise ValueError("At least one character type must be enabled")

    password = ''.join(random.choice(characters) for _ in range(length))
    return password

def generate_passwords_gui():
    length = int(length_entry.get())
    use_uppercase = uppercase_var.get()
    use_lowercase = lowercase_var.get()
    use_digits = digits_var.get()
    use_punctuation = punctuation_var.get()

    try:
        password = generate_password(length, use_uppercase, use_lowercase, use_digits, use_punctuation)
        password_entry.delete(0, tk.END)
        password_entry.insert(0, password)
    except ValueError:
        password_entry.delete(0, tk.END)
        password_entry.insert(0, "Error: at least one character type must be enabled")

root = tk.Tk()
root.title("Random Password Generator")

frame = tk.Frame(root)
frame.pack(padx=10, pady=10)

length_label = tk.Label(frame, text="Length:")
length_label.grid(row=0, column=0)
length_entry = tk.Entry(frame, width=10)
length_entry.grid(row=0, column=1)

uppercase_var = tk.BooleanVar()
uppercase_checkbox = tk.Checkbutton(frame, text="Include uppercase letters", variable=uppercase_var)
uppercase_checkbox.grid(row=1, column=0, columnspan=2)

lowercase_var = tk.BooleanVar()
lowercase_checkbox = tk.Checkbutton(frame, text="Include lowercase letters", variable=lowercase_var)
lowercase_checkbox.grid(row=2, column=0, columnspan=2)

digits_var = tk.BooleanVar()
digits_checkbox = tk.Checkbutton(frame, text="Include digits", variable=digits_var)
digits_checkbox.grid(row=3, column=0, columnspan=2)

punctuation_var = tk.BooleanVar()
punctuation_checkbox = tk.Checkbutton(frame, text="Include punctuation", variable=punctuation_var)
punctuation_checkbox.grid(row=4, column=0, columnspan=2)

generate_button = tk.Button(frame, text="Generate Password", command=generate_passwords_gui)
generate_button.grid(row=5, column=0, columnspan=2, pady=(5, 0))

password_label = tk.Label(frame, text="Password:")
password_label.grid(row=6, column=0)
password_entry = tk.Entry(frame, width=30)
password_entry.grid(row=6, column=1)

root.mainloop()
