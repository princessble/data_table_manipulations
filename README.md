# Data Table Manipulations (UiPath Studio 2025.0.172 STS)

A beginner-friendly UiPath project that demonstrates how to **join two DataTables** on a shared key (Student ID), **remove a duplicate column**, **sort the result**, and **display it** in a message box.

> Built and tested with **UiPath Studio 2025.0.172 STS** (Stable).

---

## ✨ What this project does

- Creates two in-memory tables:
  - `dt_users` → **Student ID**, **Student Name**
  - `dt_overdueBooks` → **Student ID**, **Book Name**
- Joins them on **Student ID** using **Join Data Tables (Inner Join)**
- Removes the duplicate **Student ID** column that comes from the second table
- Sorts by **Student Name** (A → Z)
- Converts the final table to **text** and shows it in a **Message Box**

Example output (depends on your sample data):

```
Student ID,Student Name,Book Name
S001,Anna Lee,Calculus I
S003,Chinwe Okoro,Organic Chemistry
```

---

## 🧰 Requirements

- UiPath Studio **2025.0.172 STS** (or compatible 2025 build)
- Windows with .NET support (standard UiPath installation)
- No external packages required beyond defaults

---

## 📁 Project Structure (suggested)

```
Data Table Manipulations/
├─ Main.xaml
├─ README.md
└─ (optional) Screenshots/
```

> The workflow is a **single Sequence** in `Main.xaml`.

---

## 🧠 Core Variables

| Name               | Type       | Scope           | Description                                   |
|--------------------|------------|-----------------|-----------------------------------------------|
| `dt_users`         | DataTable  | Main Sequence   | Students table (Student ID, Student Name)     |
| `dt_overdueBooks`  | DataTable  | Main Sequence   | Overdue books table (Student ID, Book Name)   |
| `dt_borrowedBooks` | DataTable  | Main Sequence   | Result after Join                              |
| `dt_OutputDataTable` | DataTable| Main Sequence   | Sorted result                                  |
| `strTableOut`      | String     | Main Sequence   | Final text to display in Message Box           |

> If your course/logbook requires the text variable to be named `DataTable`, you can use that instead of `strTableOut`.

---

## 🛠 Activities Used (in order)

1. **Sequence**  
2. **Build Data Table** → *Users* (`dt_users`)  
   - Columns: `Student ID` (String), `Student Name` (String)  
3. **Build Data Table** → *Overdue Books* (`dt_overdueBooks`)  
   - Columns: `Student ID` (String), `Book Name` (String)  
4. **Join Data Tables** → *Users & Overdue Books* (`dt_borrowedBooks`)  
   - Join Type: **Inner**  
   - Condition: Table1 **ColumnIndex = 0** (= Student ID)  =  Table2 **ColumnIndex = 0**  
5. **Remove Data Column** (from `dt_borrowedBooks`)  
   - **ColumnIndex = 2** to remove the *duplicate* Student ID column from table 2  
6. **Sort Data Table** (`dt_borrowedBooks` → `dt_OutputDataTable`)  
   - **ColumnIndex = 1** (Student Name)  
   - **Order = Ascending**  
7. **Output Data Table** (`dt_OutputDataTable` → `strTableOut`)  
8. **Message Box** (Text = `strTableOut`)  

---

## 🚀 Quick Start (Step‑by‑Step)

1. **Create** a new UiPath **Process**: *Data Table Manipulations*.  
2. Open `Main.xaml`, drop a **Sequence**, rename it appropriately.  
3. Add **Build Data Table** → configure `Student ID`, `Student Name` → output **`dt_users`**.  
   - Add a few rows (e.g., `S001, Anna Lee`; `S003, Chinwe Okoro`).  
4. Add **Build Data Table** → configure `Student ID`, `Book Name` → output **`dt_overdueBooks`**.  
   - Add rows with overlapping IDs (e.g., `S001, Calculus I`; `S003, Organic Chemistry`).  
5. Add **Join Data Tables**:  
   - Table1 = `dt_users`, Table2 = `dt_overdueBooks`  
   - Join Type = **Inner**  
   - Condition: **0 = 0** (joins on Student ID in both tables)  
   - Output = **`dt_borrowedBooks`**  
6. Add **Remove Data Column**:  
   - DataTable = `dt_borrowedBooks`  
   - **ColumnIndex = 2** (removes duplicate Student ID from table 2)  
7. Add **Sort Data Table**:  
   - Input = `dt_borrowedBooks`  
   - Output = **`dt_OutputDataTable`**  
   - **ColumnIndex = 1**, **Order = Ascending**  
8. Add **Output Data Table**:  
   - Input = `dt_OutputDataTable`  
   - Output Text = **`strTableOut`** (String)  
9. Add **Message Box**:  
   - Text = `strTableOut`  
10. **Save** and **Run**.

---

## 🧪 Sample Data (you can paste in *Build Data Table* editors)

### Users (`dt_users`)
| Student ID | Student Name    |
|------------|------------------|
| S001       | Anna Lee         |
| S002       | Ben Cole         |
| S003       | Chinwe Okoro     |

### Overdue Books (`dt_overdueBooks`)
| Student ID | Book Name          |
|------------|--------------------|
| S001       | Calculus I         |
| S003       | Organic Chemistry  |
| S004       | Algorithms         |

> With an **Inner Join**, only `S001` and `S003` will appear in the result because those IDs exist in **both** tables.

---

## 🧯 Troubleshooting

- **No rows after join**  
  Make sure Student IDs **match exactly** in both tables (no extra spaces, same casing).  
- **Wrong column removed**  
  Confirm **ColumnIndex = 2** in **Remove Data Column**. If your duplicate column has a different position/name (e.g., `Student ID_1`), you can remove by **ColumnName** instead.  
- **Sorting didn’t change order**  
  Ensure **ColumnIndex = 1** and **Order = Ascending** in **Sort Data Table**.  
- **Message Box shows `System.Data.DataTable`**  
  You likely passed the DataTable directly. Use **Output Data Table** first and pass the **String** result to Message Box.

---

## 🧭 Extending the Project (Ideas)

- Change **Join Type** to **Left/Right/Full** for different scenarios.  
- Add a second sort (e.g., then by `Book Name`) using LINQ or additional activities.  
- Write the final table to **Excel** with **Write Range**.  
- Validate input data and handle empty tables gracefully.

---

## 🤝 Contributing

1. Fork this repo  
2. Create a feature branch: `git checkout -b feature/my-improvement`  
3. Commit changes: `git commit -m "Describe your improvement"`  
4. Push branch: `git push origin feature/my-improvement`  
5. Open a Pull Request

---

## 📄 License

This project is open-source. Choose a license that fits your needs (e.g., MIT).

---

## 🙋 Support

If you’re stuck, open an **Issue** with:  
- UiPath version (e.g., 2025.0.172 STS)  
- Screenshot of the activity and **Properties** panel  
- Error message (if any) and what you’ve tried
