Când faci `git pull`, Git face de fapt **două operații**:

```
git fetch  (aduce schimbările din remote)
git merge / git rebase (le aplică peste branch-ul local)
```

Mesajul apare pentru că Git nu știe **cum vrei să combine istoricul** când branch-urile au divergat.

---

# 1️⃣ `pull.rebase false` → **merge (default clasic)**

```bash
git config pull.rebase false
```

`git pull` va face:

```
git fetch
git merge
```

Dacă există commit-uri locale și remote, Git creează **un merge commit**.

Diagramă:

```
main:    A---B---C
               \
local:          D---E

după pull:

A---B---C-------M
     \         /
      D-------E
```

`M` = merge commit

✅ Avantaj: nu rescrie istoricul
❌ Dezavantaj: istoricul devine mai ramificat

---

# 2️⃣ `pull.rebase true` → **rebase**

```bash
git config pull.rebase true
```

`git pull` va face:

```
git fetch
git rebase origin/main
```

Commit-urile tale locale sunt **mutate peste cele din remote**.

Diagramă:

```
înainte:

main:    A---B---C
               \
local:          D---E

după rebase:

A---B---C---D'---E'
```

`D' E'` = aceleași commit-uri, dar rescrise

✅ Avantaj: istoric **liniar și curat**
❌ Dezavantaj: rescrie commit-urile (hash nou)

---

# 3️⃣ `pull.ff only` → **fast-forward only**

```bash
git config pull.ff only
```

Git va face update **doar dacă poate avansa branch-ul fără merge sau rebase**.

Diagramă permisă:

```
main(remote): A---B---C
local:        A---B

după pull:

A---B---C
```

Diagramă interzisă:

```
main(remote): A---B---C
local:        A---B---D
```

Aici Git va da **eroare**.

✅ Avantaj: istoric perfect liniar
❌ Dezavantaj: trebuie să rezolvi manual divergența

---

# 🧠 Pe scurt

| Config              | Ce face           | Istoric       |
| ------------------- | ----------------- | ------------- |
| `pull.rebase false` | merge             | ramificat     |
| `pull.rebase true`  | rebase            | liniar        |
| `pull.ff only`      | doar fast-forward | foarte strict |

---

💡 **În multe echipe moderne se folosește:**

```bash
git config --global pull.rebase true
```

pentru că păstrează istoricul **mai curat**.

---

Dacă vrei, îți pot arăta și **care este workflow-ul Git folosit în majoritatea companiilor (GitHub/GitLab)** și de ce aproape toți folosesc `rebase`.
