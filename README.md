# Simple Calculator (Tkinter GUI)

A very small Python project that implements a simple calculator GUI using Tkinter. It provides basic arithmetic functionality (addition, subtraction, multiplication, division, decimal numbers) and a clear (C) button.

This repository contains a single GUI script:
- `Simple_Calculator_GUI.py` — a Tkinter-based calculator.

What I did: I wrote this README to explain what the project is, how to run it, and how to fix the known issues in the included script.

## Features

- Simple, lightweight GUI built with Tkinter
- Basic arithmetic operations: +, -, *, /
- Decimal support
- Clear (C) button, and evaluate (=) button (note: the provided file has a few small bugs — see "Notes & Fixes" below)

## Requirements

- Python 3.6+
- Tkinter (usually included with standard Python distributions)
  - On some Linux systems you may need to install a system package such as `python3-tk`.

## Installation

1. Clone the repository (or download the single file):
   ```
   git clone https://github.com/WallyDevLab/Simple_Calculator_Python.git
   cd Simple_Calculator_Python
   ```

2. Ensure you have Python 3 and Tkinter available:
   - macOS: Tkinter comes with the Python.org installer.
   - Ubuntu/Debian: `sudo apt-get install python3-tk`

## Running

Run the GUI script with Python:
```
python3 Simple_Calculator_GUI.py
```
A window titled "Simple Calculator" should open with buttons for digits and operators.

## Usage

- Click number buttons to enter digits.
- Click `.` to enter a decimal point.
- Use `+`, `-`, `*`, `/` for arithmetic operations.
- Click `C` to clear the input.
- Click `=` to evaluate the expression shown in the entry field.

Example:
- Press `1`, `2`, `+`, `3`, `=` → the entry should display `15`.

## Notes & Fixes

The included `Simple_Calculator_GUI.py` in this repository works conceptually but contains a few small bugs and issues that prevent it from running as-is. Here are the problems and the recommended fixes:

1. Undefined variable `root`:
   - The script creates a Tkinter root window as `window = tk.Tk()` but later uses `root` when creating Button widgets. Replace `root` with `window`.

2. Missing `=` button in the `buttons` list:
   - The code's `buttons` list doesn't include the `"="` entry. Add an `"="` entry in the desired position (commonly as a wide button on the bottom row).

3. Lambdas capturing loop variable incorrectly:
   - Button command lambdas use `lambda: button_click(text)` or an invalid `lambda: symbol=text: button_click(symbol)`. Use a default argument to capture the current button text correctly:
     ```
     command=lambda s=text: button_click(s)
     ```

4. `window.mainloop` is referenced without calling it:
   - The script ends with `window.mainloop` but it should call the function:
     ```
     window.mainloop()
     ```

5. `eval` safety note:
   - The script uses Python's `eval()` to evaluate expressions. That is convenient but can be unsafe if untrusted input is allowed. For a small local calculator this is usually acceptable, but consider replacing `eval` with a safe parser or restricted evaluation for production code.

A minimal corrected snippet for the button-creation loop:

```python
for button in buttons:
    if len(button) == 3:
        text, row, column = button
        rowspan, columnspan = 1, 1
    else:
        text, row, column, rowspan, columnspan = button

    # Capture text in the lambda default argument so the current value is used
    btn = tk.Button(window, text=text, padx=40, pady=20, command=lambda s=text: button_click(s))
    btn.grid(row=row, column=column, rowspan=rowspan, columnspan=columnspan, padx=5, pady=5)
```

## Contributing

Contributions are welcome. If you want to:
- Fix the known issues and open a PR — please include a short explanation of your changes.
- Add tests, more operations, keyboard support, or a more robust expression evaluator — feel free to open an issue or PR.

Guidelines:
- Keep changes focused and small.
- Test that the GUI runs on at least one OS (macOS, Windows, or Linux).
- If you replace `eval` with a parser/evaluator, include tests for correctness and invalid input handling.

## Troubleshooting

- Window does not appear: ensure `tkinter` is installed and call `python3 Simple_Calculator_GUI.py` from a terminal.
- Buttons do not respond or command values are wrong: see the "Lambdas capturing loop variable" fix above.
- Syntax or runtime errors: double-check that the script uses `window` consistently and calls `window.mainloop()`.

## License

This project is provided without a license. If you want to reuse it, please reach out to the repository owner or add a LICENSE file.

---

If you'd like, I can:
- create and push a corrected version of `Simple_Calculator_GUI.py` that applies the fixes above, or
- open a PR with additional improvements (keyboard input, safer expression evaluation, tests).

Tell me which you prefer and I'll make the next change.
