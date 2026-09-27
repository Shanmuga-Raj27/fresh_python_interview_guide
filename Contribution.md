# Contribution Guidelines

Thank you for contributing to this Python interview preparation guide. Follow the guidelines below to keep the content accurate, consistent, and easy to read.

---

## 📋 General Rules

- Keep content **interview-focused** — avoid unnecessary theory.
- Write in **simple, natural language** — no long paragraphs.
- Follow the existing folder structure and naming conventions.
- Do not modify or remove existing content unless correcting an error.
- All contributions must be relevant to Python technical interviews.

---

## 🤖 Using AI Tools

AI tools may be used, but you are responsible for the final content.

- **Verify** every code snippet, output, and explanation.
- Keep answers **concise, natural, and readable** — avoid verbose technical essays.
- Remove any AI-style filler or disclaimers from the final submission.
- If an answer is wrong, fix it before submitting.

---

## 📝 Markdown File Format

Use this structure for every topic:

### Interview Answer

A short, clear answer suitable for an interview.

### Code

```python
# code here
```

### Output

```
# expected output here
```

### Execution Flow

```
step 1
  ↓
step 2
  ↓
result
```

Use **text or ASCII diagrams only** — no Mermaid, Graphviz, or complex diagrams.

---

## 🐍 Python Code File Format

For every `.py` file, include:

1. **Command-line explanation** at the top as comments
2. **Interview-style answer** in comments where relevant
3. **Execution flow** as a text diagram at the end

### Example

```python
# Command-line:
# python 01_Sum-of-digits.py

# Sum of Digits

a = 12345

# 1. Pythonic approach — sum() + map()
print(sum(map(int,str(a))))


"""
How it works: str(a) converts the number into a string, map(int, ...) converts each digit back to an integer, 
and sum() adds all the digits. This is the shortest and most Pythonic solution.

Execution Flow:
                  a = 12345
                     ↓
                  str(a)
                     ↓
                  "12345"
                     ↓
                  map(int, ...)
                     ↓
                  1 → 2 → 3 → 4 → 5
                     ↓
                  sum(...)
                     ↓
                  1 + 2 + 3 + 4 + 5
                     ↓
                  15

"""
```

---

## ✅ Before Submitting

- [ ] Code runs and produces the shown output.
- [ ] Explanation is accurate and concise.
- [ ] No long paragraphs or AI Slop.
- [ ] Formatting matches the examples above.

---

## 🧩 Problem Solving Files

For coding problems in `Problem Solvings/`:

- Multiple solutions for the **same problem** are encouraged using different common methods.
- Use numbered filenames to keep solutions organized.
- Follow this naming format:

```
01_Problem-name.py
02_Problem-name.py
```

**Example:**

```
01_Sum-of-digits.py
02_Sum-of-digits.py
```

Each file should show a different approach to the same problem.

---

## 📂 Where to Contribute

| Type | Location |
|------|----------|
| Topic explanation | `Fundamentals/`, `Intermediate/`, `OOPs/`, `Data Structures/`, `Advanced/` |
| Coding problem | `Problem Solvings/Easy/` or `Problem Solvings/Medium/` |
| Multiple solutions for same problem | Same folder, numbered filenames |
| Interview Q&A | Relevant topic folder as `.md` |

---

## 💬 Questions?

Open an issue if you need clarification before contributing.
