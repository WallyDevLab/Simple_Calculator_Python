import tkinter as tk

def button_click(symbol):
    """
    Handles button clicks for the calculator.

    Parameters:
    symbol (str): The symbol of the button that was clicked. Can be a digit, operator, 
                  'C' for clear, or '=' for evaluate.

    Returns:
    None
    """
    current = entry.get()
    if symbol == "C":
        entry.delete(0, tk.END)
    elif symbol == "=":
        try:
            result = eval(current)
            entry.delete(0, tk.END)
            entry.insert(tk.END, str(result))
        except:
            entry.delete(0, tk.END)
            entry.insert(tk.END, "Error")
    else:
        entry.insert(tk.END, symbol)

# This is the section for creating the main window

window = tk.Tk()
window.title("Simple Calculator")

# This is the buttons section

buttons = [
    ("7", 1, 0), ("8", 1, 1), ("9", 1, 2), ("/", 1, 3),
    ("4", 2, 0), ("5", 2, 1), ("6", 2, 2), ("*", 2, 3), 
    ("1", 3, 0), ("2", 3, 1), ("3", 3, 2), ("-", 3, 3), 
    ("0", 4, 0), (".", 4, 1), ("C", 4, 2), ("+", 4, 3), 
    ("", 5, 0, 1, 4) 
]

# This section is for the creation of the buttons

for button in buttons:
    if len(button) == 3:
        text, row, column = button
        rowspan, columnspan = 1, 1
    else:
        text, row, column, rowspan, columnspan = button

    if text == "=":
        btn = tk.Button(root, text=text, padx = 80, pady = 20, command = lambda: button_click(text))
    else:
        btn = tk.Button(root, text=text, padx = 40, pady = 20, command = lambda: symbol=text: button_click(symbol))
    btn.grid(row=row, column=column, rowspan=rowspan, columnspan=columnspan, padx=5, pady=5)

# Start the main event loop

window.mainloop
