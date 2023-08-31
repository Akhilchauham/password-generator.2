# password-generator.2
import tkinter as tk
import random
import string

def generate_password():
    password_length = int(length_entry.get())
    if password_length < 4:
        password_label.config(text="Password length must be at least 4 characters.")
        return

    special_chars = "!@#$%^&*()_+-=[]{}|;:,.<>?"
    all_chars = string.ascii_letters + string.digits + special_chars
    password = ''.join(random.choice(all_chars) for _ in range(password_length))
    
    username = username_entry.get()
    if not username:
        password_label.config(text="Please enter a username.")
        return
    
    password_label.config(text=f"Username: {username}\nGenerated Password: {password}")
    accept_button.config(state=tk.NORMAL)

def reset_fields():
    username_entry.delete(0, tk.END)
    length_entry.delete(0, tk.END)
    password_label.config(text="")
    accept_button.config(state=tk.DISABLED)

root = tk.Tk()
root.title("Password Generator")

username_label = tk.Label(root, text="Enter Username:")
username_label.pack()

username_entry = tk.Entry(root)
username_entry.pack()

length_label = tk.Label(root, text="Enter Password Length:")
length_label.pack()

length_entry = tk.Entry(root)
length_entry.pack()

generate_button = tk.Button(root, text="Generate Password", command=generate_password)
generate_button.pack()

password_label = tk.Label(root, text="", wraplength=300)
password_label.pack()

button_frame = tk.Frame(root)
button_frame.pack()

accept_button = tk.Button(button_frame, text="Accept", state=tk.DISABLED, command=reset_fields)
accept_button.pack(side=tk.LEFT, padx=10)

reset_button = tk.Button(button_frame, text="Reset", command=reset_fields)
reset_button.pack(side=tk.LEFT, padx=10)

root.mainloop()
