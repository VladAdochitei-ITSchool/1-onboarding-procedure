Mai jos ai explicația pe scurt + câte o diagramă simplă pentru fiecare opțiune din GitHub.

---

## 1. **Create a merge commit**

Combină cele două branch-uri și creează **un commit nou de tip merge**. Istoricul păstrează clar faptul că a existat un branch separat.

**Ideea:** istoricul rămâne complet, dar apare un commit în plus.

**Diagramă:**

```
main:    A---B---C
               \
feature:        D---E

după merge:

main:    A---B---C-------M
               \       /
feature:        D-----E
```

`M` = merge commit

---

## 2. **Squash and merge**

Toate commit-urile din branch sunt **comasate într-un singur commit** înainte de a fi adăugate în `main`.

**Ideea:** istoricul devine mai curat, dar se pierd commit-urile individuale din branch.

**Diagramă:**

```
înainte:

main:    A---B---C
               \
feature:        D---E---F

după squash:

main:    A---B---C---S
```

`S` = un singur commit care conține tot (D+E+F)

---

## 3. **Rebase and merge**

Commit-urile din branch sunt **mutate (rebased) peste ultimul commit din main**, fără merge commit.

**Ideea:** istoric liniar, dar commit-urile sunt rescrise.

**Diagramă:**

```
înainte:

main:    A---B---C
               \
feature:        D---E

după rebase:

main:    A---B---C---D'---E'
```

`D' E'` = aceleași schimbări, dar cu hash nou (rescrise)

---

✅ **Pe scurt:**

| Metodă       | Ce face                      | Istoric      |
| ------------ | ---------------------------- | ------------ |
| Merge commit | adaugă commit de merge       | ramificat    |
| Squash       | combină toate commit-urile   | foarte curat |
| Rebase       | mută commit-urile peste main | liniar       |

---

Dacă vrei, îți pot arăta și **când se folosește fiecare în echipe reale (GitHub workflow)** — e mult mai ușor de înțeles.
