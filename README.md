

## 📓 **Jupyter Notebook Version**

This repository includes an interactive **Jupyter Notebook (`.ipynb`)** that demonstrates the full workflow for handling large **SQL `IN` clause** queries using chunking.

The notebook version is ideal for **ad hoc analysis**, **step-by-step debugging**, and understanding how the batching logic works.

---

## 🚀 **What the Notebook Does**

The notebook walks through the process in clear stages:

* 📥 Load a list of IDs from an Excel file
* 🧹 Clean and prepare the ID list
* ✂️ Split IDs into smaller chunks
* 🧩 Dynamically build SQL `IN` clauses
* 🗄️ Execute the query for each chunk
* 🔗 Combine all results into one dataset
* 📤 Export the final output to Excel

---

## ▶️ **How to Run the Notebook**

### 1️⃣ Install Required Libraries

```bash
pip install pandas openpyxl
```

### 2️⃣ Start Jupyter Notebook

```bash
jupyter notebook
```

### 3️⃣ Open the Notebook File

Open the uploaded `.ipynb` file from the Jupyter interface.

### 4️⃣ Update Configuration Cells

Before running all cells, update:

* 📁 Input Excel file path
* 🏷️ Column name containing IDs
* 🧠 SQL query
* 🔐 Database connection/query execution logic

### 5️⃣ Run All Cells

Run cells from **top to bottom** to execute the full workflow.

---

## 🔐 **Security Best Practices**

For safety, this notebook does **not** include:

* ❌ Database credentials
* ❌ Internal connection libraries
* ❌ Confidential table or schema names

**Always use:**

✔ Environment variables
✔ Secure credential storage
✔ Sanitized queries before sharing publicly

---

## 🛠 **Where Customization Is Required**

You must modify:

| Section           | What to Update                         |
| ----------------- | -------------------------------------- |
| Database Function | Add your own query execution logic     |
| SQL Query         | Replace with your required query       |
| File Paths        | Set correct input and output locations |

The chunking and merging logic will work as-is.

---

## 💡 **Performance Tips**

* If queries fail → **reduce `CHUNK_SIZE`**
* If queries are stable → **increase `CHUNK_SIZE`** to reduce total runs
* For very large pulls → consider adding **parallel execution**

---
