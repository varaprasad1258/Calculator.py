import tkinter as tk

def click(event):
    global expression
    text = event.widget.cget("text")
    
    if text == "=":
        try:
            result = str(eval(expression))
            display_var.set(result)
            expression = result
        except Exception as e:
            display_var.set("Error")
            expression = ""
    elif text == "C":
        expression = ""
        display_var.set("")
    else:
        expression += text
        display_var.set(expression)

# Initialize main window
root = tk.Tk()
root.title("Simple Calculator")
root.geometry("300x400")
root.resizable(0, 0)

# Global expression variable
expression = ""

# Display field
display_var = tk.StringVar()
entry = tk.Entry(root, textvar=display_var, font="Arial 20", bd=10, relief=tk.RIDGE, justify='right')
entry.pack(fill="both", ipadx=8, pady=10, padx=10)

# Button layout
button_texts = [
    ["7", "8", "9", "/"],
    ["4", "5", "6", "*"],
    ["1", "2", "3", "-"],
    ["C", "0", "=", "+"]
]

for row_values in button_texts:
    row = tk.Frame(root)
    row.pack(expand=True, fill="both")
    for text in row_values:
        button = tk.Button(row, text=text, font="Arial 18", relief=tk.GROOVE)
        button.pack(side="left", expand=True, fill="both")
        button.bind("<Button-1>", click)

root.mainloop()
