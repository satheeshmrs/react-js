# 📘 Diffing & Reconciliation in Runtime (with Flow Diagrams)

When a UI framework like **React** updates state or props, it doesn’t replace the entire DOM. Instead, it uses **Diffing** and **Reconciliation** to efficiently update only what’s changed.

---

## 🔹 1) What is Diffing?
- **Definition**: Compare the **old virtual tree** with the **new virtual tree**.
- **Goal**: Find the minimal set of changes (insertions, updates, deletions).

---

## 🔹 2) What is Reconciliation?
- **Definition**: Apply those detected changes to the **real DOM** (or platform-specific UI).
- **Goal**: Keep the UI in sync with the latest state/props with **minimal cost**.

---

## 🔹 3) Runtime Workflow

### Flow Overview
```text
 ┌─────────────────────┐
 │  State/Props Change │
 └──────────┬──────────┘
            │
            ▼
 ┌─────────────────────┐
 │ Render New Virtual  │
 │ DOM Tree            │
 └──────────┬──────────┘
            │
            ▼
 ┌─────────────────────┐
 │   Diffing Process   │
 │ (Old VTree vs New)  │
 └──────────┬──────────┘
            │
            ▼
 ┌─────────────────────┐
 │ Reconciliation      │
 │ (Apply changes to   │
 │ Real DOM/Native UI) │
 └──────────┬──────────┘
            │
            ▼
 ┌─────────────────────┐
 │ Updated User View   │
 └─────────────────────┘
```

---

## 🔹 4) Diffing Rules (Heuristics in React)

1. **Same type element**  
   → Update attributes/props only.  
   Example: `<div class="a">` → `<div class="b">`

2. **Different type element**  
   → Destroy old subtree, mount new subtree.  
   Example: `<div>` → `<span>`

3. **Lists (with keys)**  
   - Use `key` to identify stable elements.
   - Moves items instead of re-creating them.
   - Without stable keys, React assumes reorder = content changes.

---

## 🔹 5) Reconciliation Commit Phase

Once diffs are found, reconciliation runs in 3 steps:

```text
1. Before Mutation → capture snapshots if needed.
2. Mutation Phase → Apply DOM changes (insert/update/delete).
3. Layout Effects → Run lifecycle hooks (componentDidMount, useLayoutEffect).
```

---

## 🔹 6) Example Walkthrough

### Code Change
```jsx
// Old Virtual DOM
<ul>
  <li key="1">A</li>
  <li key="2">B</li>
</ul>

// New Virtual DOM
<ul>
  <li key="2">B</li>
  <li key="1">A</li>
</ul>
```

### Runtime Steps
1. **Render**: new VDOM generated.  
2. **Diffing**: Compare old vs new. Keys help detect nodes are same items but reordered.  
3. **Effect List**: Move `<li key="2">` above `<li key="1">`.  
4. **Reconciliation**: Apply DOM change → reorder elements.  
5. **Result**: DOM updated minimally without destroying `<li>` nodes.

---

## 🔹 7) Another Flow Diagram (with Phases)

```text
[ Trigger: setState() ]
          │
          ▼
 ┌───────────────────┐
 │ Render Phase      │
 │ - Create new VDOM │
 │ - Diff old vs new │
 └─────────┬─────────┘
           │
   Effect list built
           │
           ▼
 ┌───────────────────┐
 │ Commit Phase      │
 │ - Before mutation │
 │ - DOM mutations   │
 │ - Run effects     │
 └─────────┬─────────┘
           │
           ▼
   ✅ UI Updated
```

---

## 🔑 Key Takeaways
- **Diffing** = *what changed?*  
- **Reconciliation** = *apply those changes*.  
- Runtime ensures only the **minimum required operations** are done.  
- Stable keys & immutability = predictable, efficient updates.  
