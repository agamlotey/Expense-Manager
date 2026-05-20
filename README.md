# Expense Manager

> A desktop expense and budget tracking application built in Python, designed as an object-oriented programming project. It uses a Tkinter GUI and is organized into clean model, controller, view, and utility layers.

Track your spending, group expenses into categories, set budget limits, and see at a glance when a category goes over budget — all from a simple desktop window.

---

## Features

- **Add expenses** with a description, amount, date, category, and payment method.
- **Manage categories** — create your own spending categories, each with its own budget limit.
- **Budget tracking** — every expense is deducted from its category's budget, and the app flags categories that go over their limit.
- **Edit and delete** existing expenses, with the budget automatically adjusted.
- **Export to CSV** — save all expenses to a spreadsheet-friendly file.
- **Interactive GUI** — a dark-themed Tkinter interface with a live expense table and status bar.
- **Sensible defaults** — the app starts seeded with sample categories (Food, Transport) and payment methods (card, cash) so you can try it immediately.

---

## Object-oriented design

This project is built to demonstrate the four core pillars of object-oriented programming:

| Concept | Where it's used |
|---------|-----------------|
| **Abstraction** | `Entity` is an abstract base class with an abstract `display()` method; `Reportable` is an abstract interface for reports. |
| **Inheritance** | `User`, `Expense`, `Category`, `Budget`, `Transaction`, and `PaymentMethod` all inherit from `Entity`, sharing a common `id` and `created_at`. |
| **Encapsulation** | `Budget` keeps its `__balance` private and exposes it only through `get_balance()`, `add_expense()`, and `is_over_budget()`. |
| **Polymorphism** | Every model overrides `display()` with its own formatted string. |

---

## Project structure

```
oopsproject/
├── main.py                     Application entry point
├── models/                     Data classes (the OOP core)
│   ├── entity.py               Abstract base class for all models
│   ├── user.py
│   ├── expense.py
│   ├── category.py
│   ├── budget.py               Encapsulated budget balance
│   ├── transaction.py
│   └── payment_method.py
├── controllers/                Business logic
│   ├── expense_controller.py
│   ├── budget_controller.py
│   └── report_controller.py    Implements the Reportable interface
├── views/                      Text-based renderers
│   ├── dashboard_view.py
│   ├── expense_view.py
│   └── budget_view.py
├── ui/                         Tkinter graphical interface
│   ├── main_window.py          The main application window
│   ├── expense_form.py         Pop-up form for adding an expense
│   └── chart_canvas.py
└── utils/                      Helper functions
    ├── date_utils.py           Date parsing and month ranges
    ├── file_handler.py         JSON save/load
    └── validator.py            Amount and email validation
```

---

## Requirements

- **Python 3.8+**
- **Tkinter** — included with most Python installations. On some Linux systems you may need to install it separately:

  ```bash
  sudo apt install python3-tk
  ```

The project uses only the Python standard library — there are no third-party packages to install.

---

## How to run

```bash
# Clone the repository
git clone https://github.com/<your-username>/<repo-name>.git
cd <repo-name>

# Move into the project folder and launch
cd oopsproject
python main.py
```

The application window opens with sample categories already loaded. Fill in the form on the left to add an expense, and it appears in the table on the right.

---

## Using the app

1. **Add an expense** — enter a description, amount, and date, pick a category and payment method, then click **Add Expense**.
2. **Add a category** — type a name and a budget limit in the "Categories & Budgets" section and click **Add Category**.
3. **Edit an expense** — select a row in the table and click **Edit Selected**; its details load back into the form.
4. **Delete an expense** — select a row and click **Delete Selected**.
5. **Export** — click **Export CSV** to save all expenses to `expenses_export.csv`.

---

## Notes

A couple of housekeeping items if you continue developing this project:

- `ui/chart_canvas.py` currently contains a duplicate copy of `main_window.py` — it looks like a copy-paste leftover and can be replaced with the real chart code or removed.
- Import paths are inconsistent across the codebase: `main.py` and `ui/main_window.py` use plain imports (`from models.user import User`), while the controllers use package-prefixed imports (`from oopsproject.models...`). Running from inside the `oopsproject/` folder, as shown above, makes the GUI work. Standardizing all imports to one style would make the project easier to run from anywhere.
- The Tkinter GUI in `main_window.py` manages its own in-memory data; the `controllers/` and `views/` modules are a parallel layer that isn't wired into the running app yet.
