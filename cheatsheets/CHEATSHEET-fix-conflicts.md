Când faci `git pull` și apare mesajul **“divergent branches”**, Git îți spune că branch-ul local și cel remote au commit-uri diferite. Dacă faci merge/rebase și apar **conflicts**, le vezi și le rezolvi astfel:

---

## 1️⃣ Vezi fișierele cu conflicte

```bash
git status
```

Exemplu output:

```
both modified:   file1.js
both modified:   app.py
```

---

## 2️⃣ Deschide fișierul și editează conflictul

În fișier vei vedea ceva de genul:

```
<<<<<<< HEAD
codul tău local
=======
codul din remote
>>>>>>> origin/main
```

Rezolvi manual alegând sau combinând codul, apoi ștergi marker-ele:

```
codul final ales
```

---

## 3️⃣ Marchează conflictul ca rezolvat

```bash
git add nume_fisier
```

sau pentru toate:

```bash
git add .
```

---

## 4️⃣ Finalizează merge-ul

Dacă ai făcut **merge**:

```bash
git commit
```

Dacă ai făcut **rebase**:

```bash
git rebase --continue
```

---

💡 **Comandă utilă să vezi exact conflictele:**

```bash
git diff
```

---

✅ **Flow rapid:**

```
git pull
git status
(edit files)
git add .
git commit   (sau git rebase --continue)
```

---

Dacă vrei, îți pot arăta și **cea mai rapidă metodă de a rezolva conflicte în VS Code (mult mai ușor decât manual)**.
