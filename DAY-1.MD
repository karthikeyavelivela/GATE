# GATE 2027 CS — Week 1, Day 1
# Propositional Logic: Truth Tables, Tautologies, Equivalences

**Date:** Monday, July 27, 2026
**Time budget:** 4–5 hours (3 hrs theory + 1.5 hrs problems)
**Starting point assumed:** Absolute zero. Nothing here assumes prior discrete math.

---

# PART 1 — THEORY (from scratch)

## 1.1 What is a proposition?

A **proposition** is a statement that is either **definitely true** or **definitely false** — never both, never neither.

| Statement | Proposition? | Why |
|---|---|---|
| "Delhi is the capital of India." | ✅ Yes | Definitely true |
| "2 + 2 = 5" | ✅ Yes | Definitely false (still a proposition!) |
| "What time is it?" | ❌ No | A question has no truth value |
| "Close the door." | ❌ No | A command has no truth value |
| "x + 1 = 5" | ❌ No | Truth depends on x — this is a *predicate*, covered on Day 2 |
| "This sentence is false." | ❌ No | Paradox — can't be assigned T or F consistently |

**Key idea:** Being false does not disqualify a statement. Being *undetermined* does.

We name propositions with letters: p, q, r, s. Each can hold value **T** (true, sometimes written 1) or **F** (false, written 0).

---

## 1.2 The five logical connectives

Connectives combine simple propositions into **compound propositions**. There are exactly five you need.

### (a) NEGATION — "NOT p"
**Symbols:** ¬p, ~p, p′, p̄

| p | ¬p |
|---|---|
| T | F |
| F | T |

Flips the value. That's all.

---

### (b) CONJUNCTION — "p AND q"
**Symbols:** p ∧ q, p · q, p AND q

| p | q | p ∧ q |
|---|---|---|
| T | T | **T** |
| T | F | F |
| F | T | F |
| F | F | F |

**True only when BOTH are true.** One false ruins it.

*Memory hook:* AND is greedy — it demands everything.

---

### (c) DISJUNCTION — "p OR q"
**Symbols:** p ∨ q, p + q

| p | q | p ∨ q |
|---|---|---|
| T | T | **T** |
| T | F | **T** |
| F | T | **T** |
| F | F | F |

**False only when BOTH are false.** One true saves it.

⚠️ **Critical beginner trap:** This is **inclusive** OR. In English, "tea or coffee" usually means *one, not both*. In logic, p ∨ q is **true when both are true**. Exclusive OR is a separate connective (below).

---

### (d) EXCLUSIVE OR — "p XOR q"
**Symbols:** p ⊕ q, p ⊻ q

| p | q | p ⊕ q |
|---|---|---|
| T | T | F |
| T | F | **T** |
| F | T | **T** |
| F | F | F |

**True when the two values DIFFER.** False when they match.

Useful facts (memorize — GATE tests these):
- p ⊕ q ≡ (p ∧ ¬q) ∨ (¬p ∧ q)
- p ⊕ q ≡ ¬(p ↔ q)  ← XOR is the negation of biconditional
- p ⊕ p ≡ F
- p ⊕ F ≡ p
- p ⊕ T ≡ ¬p
- XOR is both **commutative** and **associative**

---

### (e) IMPLICATION — "if p then q"
**Symbols:** p → q, p ⊃ q, p ⇒ q

| p | q | p → q |
|---|---|---|
| T | T | **T** |
| T | F | **F** ← the ONLY false row |
| F | T | **T** |
| F | F | **T** |

**This is the single most important and most misunderstood row set in all of discrete math.** Learn it properly now or it will cost you marks for the next six months.

**Terminology:**
- p is the **antecedent** / hypothesis / premise
- q is the **consequent** / conclusion

**Why is p → q true when p is false?**

Think of implication as a **promise**. Suppose I say: *"If it rains, I will carry an umbrella."*

- It rains, I carry umbrella → promise kept → **T**
- It rains, I don't carry umbrella → promise **broken** → **F**
- It doesn't rain, I carry umbrella → promise not violated (I said nothing about dry days) → **T**
- It doesn't rain, I don't carry umbrella → promise not violated → **T**

A promise is only *broken* when the condition triggers and you fail to deliver. When the condition never triggers, the promise is trivially kept. Those last two rows are called **vacuously true**.

**The most important identity in this entire topic:**

> **p → q ≡ ¬p ∨ q**

Verify it yourself against the table above — every row matches. You will use this rewrite constantly to simplify expressions. Burn it in.

Also: **¬(p → q) ≡ p ∧ ¬q**
(To break a promise, the condition must hold AND the result must fail.)

---

### (f) BICONDITIONAL — "p if and only if q"
**Symbols:** p ↔ q, p ≡ q, p ⇔ q, "p iff q"

| p | q | p ↔ q |
|---|---|---|
| T | T | **T** |
| T | F | F |
| F | T | F |
| F | F | **T** |

**True when both values MATCH.** (Exact opposite of XOR.)

Useful identities:
- p ↔ q ≡ (p → q) ∧ (q → p)
- p ↔ q ≡ (p ∧ q) ∨ (¬p ∧ ¬q)
- p ↔ q ≡ ¬(p ⊕ q)

---

## 1.3 Precedence (order of operations)

When brackets are missing, evaluate in this order:

| Priority | Connective |
|---|---|
| 1 (highest) | ¬ (NOT) |
| 2 | ∧ (AND) |
| 3 | ∨ (OR) |
| 4 | → (implication) |
| 5 (lowest) | ↔ (biconditional) |

So `¬p ∨ q ∧ r → s` means `((¬p) ∨ (q ∧ r)) → s`.

**Associativity warning:** → is **right-associative**.
`p → q → r` means `p → (q → r)`, **not** `(p → q) → r`.

These two are **not equivalent** — proven in Q6 of the practice set below. GATE has exploited this repeatedly.

---

## 1.4 How to build a truth table (mechanical method)

For a formula with **n** distinct propositional variables, the table has **2ⁿ rows**.

| Variables | Rows |
|---|---|
| 1 | 2 |
| 2 | 4 |
| 3 | 8 |
| 4 | 16 |
| n | 2ⁿ |

**Standard procedure:**

1. Count distinct variables → gives you row count
2. Fill the variable columns in a fixed pattern. Convention: leftmost variable changes slowest.
   - For 3 variables: p = TTTTFFFF, q = TTFFTTFF, r = TFTFTFTF
   - (This is just counting down in binary with T=1, F=0)
3. Add one column per **sub-expression**, innermost brackets first
4. Combine sub-expressions to reach the final column

**Worked example:** Build the table for `(p ∨ q) → ¬r`

| p | q | r | p ∨ q | ¬r | (p ∨ q) → ¬r |
|---|---|---|---|---|---|
| T | T | T | T | F | **F** |
| T | T | F | T | T | **T** |
| T | F | T | T | F | **F** |
| T | F | F | T | T | **T** |
| F | T | T | T | F | **F** |
| F | T | F | T | T | **T** |
| F | F | T | F | F | **T** ← vacuously true |
| F | F | F | F | T | **T** |

Notice the last two rows: `p ∨ q` is false, so the implication is automatically true regardless of `¬r`.

---

## 1.5 Tautology, Contradiction, Contingency

These three words describe the **final column** of a truth table.

| Type | Definition | Final column |
|---|---|---|
| **Tautology** | True for *every* assignment | All T |
| **Contradiction** (unsatisfiable) | False for *every* assignment | All F |
| **Contingency** (satisfiable, not tautology) | True for some, false for others | Mixed |

**Canonical examples:**
- Tautology: `p ∨ ¬p` (law of excluded middle)
- Contradiction: `p ∧ ¬p`
- Contingency: `p ∧ q`

**Related vocabulary GATE uses:**

| Term | Meaning |
|---|---|
| **Satisfiable** | True for **at least one** assignment |
| **Valid** | True for **all** assignments (= tautology) |
| **Unsatisfiable** | True for **no** assignment (= contradiction) |
| **Falsifiable** | False for at least one assignment |

**Critical relationships to memorize:**
- Every tautology is satisfiable. Not every satisfiable formula is a tautology.
- **F is a tautology ⟺ ¬F is a contradiction**
- **F is a tautology ⟺ ¬F is unsatisfiable** ← this is the basis of proof by contradiction and of resolution
- A **model** of a formula = an assignment that makes it true. Counting models is a common GATE question type.

---

## 1.6 Logical Equivalence

Two formulas F and G are **logically equivalent** (written F ≡ G) if they have **identical final columns** in the truth table — same value for every possible assignment.

**Formal test:** F ≡ G if and only if `F ↔ G` is a **tautology**.

Two ways to prove equivalence:
1. **Truth table** — always works, but slow (2ⁿ rows)
2. **Algebraic simplification** using the laws below — faster, and what toppers use

### THE LAWS (memorize all of them)

Let T = tautology (true), F = contradiction (false).

**Identity Laws**
- p ∧ T ≡ p
- p ∨ F ≡ p

**Domination / Annihilation Laws**
- p ∨ T ≡ T
- p ∧ F ≡ F

**Idempotent Laws**
- p ∨ p ≡ p
- p ∧ p ≡ p

**Double Negation**
- ¬(¬p) ≡ p

**Commutative Laws**
- p ∨ q ≡ q ∨ p
- p ∧ q ≡ q ∧ p
- (Note: → is **NOT** commutative. p → q ≢ q → p)

**Associative Laws**
- (p ∨ q) ∨ r ≡ p ∨ (q ∨ r)
- (p ∧ q) ∧ r ≡ p ∧ (q ∧ r)
- (→ is **NOT** associative)

**Distributive Laws**
- p ∨ (q ∧ r) ≡ (p ∨ q) ∧ (p ∨ r)
- p ∧ (q ∨ r) ≡ (p ∧ q) ∨ (p ∧ r)

**De Morgan's Laws** ← the most heavily used pair
- ¬(p ∧ q) ≡ ¬p ∨ ¬q
- ¬(p ∨ q) ≡ ¬p ∧ ¬q

*Rule of thumb: push the negation inward and flip the connective.*

**Absorption Laws**
- p ∨ (p ∧ q) ≡ p
- p ∧ (p ∨ q) ≡ p

**Negation / Complement Laws**
- p ∨ ¬p ≡ T
- p ∧ ¬p ≡ F

**Implication-related Laws** (these are where marks are won)
- **p → q ≡ ¬p ∨ q** ← use this to eliminate → entirely
- ¬(p → q) ≡ p ∧ ¬q
- **Contrapositive:** p → q ≡ ¬q → ¬p
- **Exportation:** (p ∧ q) → r ≡ p → (q → r)
- p → (q ∧ r) ≡ (p → q) ∧ (p → r)
- p → (q ∨ r) ≡ (p → q) ∨ (p → r)
- (p ∨ q) → r ≡ (p → r) ∧ (q → r)
- (p ∧ q) → r ≡ (p → r) ∨ (q → r)
- p → q ≡ ¬(p ∧ ¬q)

**Biconditional Laws**
- p ↔ q ≡ (p → q) ∧ (q → p)
- p ↔ q ≡ ¬p ↔ ¬q
- ¬(p ↔ q) ≡ p ↔ ¬q ≡ p ⊕ q

---

## 1.7 Converse, Inverse, Contrapositive

Given the conditional **p → q**:

| Name | Form | Equivalent to original? |
|---|---|---|
| **Original** | p → q | — |
| **Converse** | q → p | ❌ **NO** |
| **Inverse** | ¬p → ¬q | ❌ **NO** |
| **Contrapositive** | ¬q → ¬p | ✅ **YES** |

**Two facts GATE loves:**
1. Original ≡ Contrapositive
2. Converse ≡ Inverse (they're contrapositives of each other!)

**Example:** "If it is a square, then it is a rectangle." (True)
- Converse: "If it is a rectangle, then it is a square." (**False** — proves converse isn't equivalent)
- Inverse: "If it is not a square, then it is not a rectangle." (**False**)
- Contrapositive: "If it is not a rectangle, then it is not a square." (**True** ✓)

---

## 1.8 Translating English into logic (high-frequency GATE skill)

This table is worth memorizing cold. Getting these backwards is the #1 avoidable error.

| English phrase | Logical form |
|---|---|
| "if p then q" | p → q |
| "p implies q" | p → q |
| "q if p" | p → q |
| "**p only if q**" | **p → q** |
| "p is sufficient for q" | p → q |
| "**q is necessary for p**" | **p → q** |
| "q whenever p" | p → q |
| "q follows from p" | p → q |
| "p is necessary for q" | q → p |
| "p is sufficient and necessary for q" | p ↔ q |
| "**p unless q**" | **¬q → p** (equivalently ¬p → q, or p ∨ q) |
| "neither p nor q" | ¬p ∧ ¬q |
| "not both p and q" | ¬(p ∧ q) |

⚠️ **"only if" vs "if"** is the classic trap:
- "I will go **if** it rains" → rain → go
- "I will go **only if** it rains" → go → rain (rain is *required*)

⚠️ **"necessary" vs "sufficient"**:
- **Sufficient** condition sits on the **left** of the arrow (it's enough to guarantee)
- **Necessary** condition sits on the **right** of the arrow (it must hold for the other to hold)

---

## 1.9 Rules of Inference (valid argument forms)

An **argument** is valid if whenever all premises are true, the conclusion is true. Each of these corresponds to a tautology.

| Rule | Premises | Conclusion | Tautology form |
|---|---|---|---|
| **Modus Ponens** | p → q, p | ∴ q | ((p → q) ∧ p) → q |
| **Modus Tollens** | p → q, ¬q | ∴ ¬p | ((p → q) ∧ ¬q) → ¬p |
| **Hypothetical Syllogism** | p → q, q → r | ∴ p → r | transitivity of → |
| **Disjunctive Syllogism** | p ∨ q, ¬p | ∴ q | ((p ∨ q) ∧ ¬p) → q |
| **Addition** | p | ∴ p ∨ q | p → (p ∨ q) |
| **Simplification** | p ∧ q | ∴ p | (p ∧ q) → p |
| **Conjunction** | p, q | ∴ p ∧ q | — |
| **Resolution** | p ∨ q, ¬p ∨ r | ∴ q ∨ r | — |
| **Constructive Dilemma** | p → q, r → s, p ∨ r | ∴ q ∨ s | — |

**Two famous FALLACIES (invalid — GATE asks these as traps):**

| Fallacy | Premises | Wrong conclusion | Why invalid |
|---|---|---|---|
| **Affirming the consequent** | p → q, q | ∴ p ❌ | This is using the converse |
| **Denying the antecedent** | p → q, ¬p | ∴ ¬q ❌ | This is using the inverse |

*Resolution is worth extra attention — it's the engine behind automated theorem proving and SAT solvers, and it reappears in your Compiler Design and AI topics later.*

---

## 1.10 Normal Forms (CNF and DNF)

Every propositional formula can be rewritten in these standard shapes.

**Literal:** a variable or its negation (p, ¬p)

**DNF — Disjunctive Normal Form:** an OR of ANDs
- Shape: `(p ∧ ¬q) ∨ (¬p ∧ r) ∨ (q ∧ r)`
- "Sum of products"
- Read directly off the truth table rows where the formula is **TRUE**

**CNF — Conjunctive Normal Form:** an AND of ORs
- Shape: `(p ∨ ¬q) ∧ (¬p ∨ r) ∧ (q ∨ r)`
- "Product of sums"
- Read off the rows where the formula is **FALSE** (negate each literal)

**How to convert to CNF (standard algorithm):**
1. Eliminate ↔ using `p ↔ q ≡ (p → q) ∧ (q → p)`
2. Eliminate → using `p → q ≡ ¬p ∨ q`
3. Push negations inward with De Morgan until they touch variables only
4. Distribute ∨ over ∧ to reach the AND-of-ORs shape

This exact pipeline reappears in Digital Logic (Week 5, K-maps) as sum-of-products/product-of-sums — you're learning it once and using it twice.

---

## 1.11 Functional Completeness

A set of connectives is **functionally complete** if every possible truth function can be built using only those connectives.

**Functionally complete sets:**
- {¬, ∧}
- {¬, ∨}
- {¬, →}
- **{NAND}** alone ✅ (single connective!)
- **{NOR}** alone ✅ (single connective!)

**NOT functionally complete:**
- {∧, ∨} — no way to produce negation
- {→} alone
- {↔}
- {⊕}

**Counting fact GATE asks:** The number of distinct truth functions (Boolean functions) of **n** variables is **2^(2ⁿ)**.
- n = 1 → 2² = 4 functions
- n = 2 → 2⁴ = **16** functions
- n = 3 → 2⁸ = 256 functions

*Reasoning: the truth table has 2ⁿ rows, and each row's output can independently be T or F.*

---

# PART 2 — PRACTICE QUESTIONS WITH FULL SOLUTIONS

These are written in authentic GATE style. Attempt each one on paper **before** reading the solution. Solving-then-checking builds the skill; reading solutions does not.

---

### Q1. Truth table basics
How many rows does the truth table of `(p ∨ q) ∧ (r → ¬s) ∧ t` have?

<details>
**Solution:** Count distinct variables: p, q, r, s, t = 5 variables.
Rows = 2⁵ = **32**
</details>

---

### Q2. Classify the formula
Determine whether `(p → q) ∨ (q → p)` is a tautology, contradiction, or contingency.

<details>
**Solution:** Rewrite both implications: `(¬p ∨ q) ∨ (¬q ∨ p)`
Regroup: `(¬p ∨ p) ∨ (q ∨ ¬q)` = `T ∨ T` = **T**

It is a **tautology**.

*Insight:* For any two propositions, at least one of "p implies q" or "q implies p" must be true. Non-obvious but true.
</details>

---

### Q3. Simplification
Simplify `¬(p ∨ q) ∨ (¬p ∧ q)`.

<details>
**Solution:**
- De Morgan on the first term: `(¬p ∧ ¬q) ∨ (¬p ∧ q)`
- Factor out ¬p (distributive law): `¬p ∧ (¬q ∨ q)`
- Negation law: `¬q ∨ q ≡ T`
- So: `¬p ∧ T`
- Identity law: **¬p**
</details>

---

### Q4. Counting models
How many assignments of truth values to p, q, r satisfy `(p ∨ q) ∧ (¬p ∨ r)`?

<details>
**Solution:** 2³ = 8 total assignments. Test each:

| p | q | r | p ∨ q | ¬p ∨ r | Result |
|---|---|---|---|---|---|
| T | T | T | T | T | **✓** |
| T | T | F | T | F | ✗ |
| T | F | T | T | T | **✓** |
| T | F | F | T | F | ✗ |
| F | T | T | T | T | **✓** |
| F | T | F | T | T | **✓** |
| F | F | T | F | T | ✗ |
| F | F | F | F | T | ✗ |

**Answer: 4 satisfying assignments.**
</details>

---

### Q5. Negating an implication
Write the negation of `p → (q ∧ r)` in a form with no implication symbol.

<details>
**Solution:**
- `¬(p → (q ∧ r))`
- Use `¬(A → B) ≡ A ∧ ¬B`: `p ∧ ¬(q ∧ r)`
- De Morgan: **p ∧ (¬q ∨ ¬r)**
</details>

---

### Q6. Associativity of implication (classic trap)
Is `(p → q) → r` logically equivalent to `p → (q → r)`? Prove your answer.

<details>
**Solution: NO.** A single counterexample suffices.

Take **p = F, q = F, r = F**:
- LHS: `(F → F) → F` = `T → F` = **F**
- RHS: `F → (F → F)` = `F → T` = **T**

Different values ⟹ **not equivalent**.

*This is exactly why → is defined as right-associative, and exactly why you must never drop brackets around chained implications.*
</details>

---

### Q7. Necessary vs sufficient
"Getting at least 60% is necessary to be eligible for the M.Tech program."
Let S = "scored at least 60%", E = "eligible". Express this as a formula.

<details>
**Solution:** "S is **necessary** for E" means E cannot happen without S. Necessary conditions go on the **right** of the arrow.

**Answer: E → S**

*Common wrong answer: S → E. That would mean 60% is sufficient — i.e., anyone with 60% is automatically eligible, which is a much stronger and different claim.*
</details>

---

### Q8. Contrapositive identification
Which of the following is the contrapositive of "If a program compiles, then it has no syntax errors"?

(A) If a program has no syntax errors, then it compiles.
(B) If a program has syntax errors, then it does not compile.
(C) If a program does not compile, then it has syntax errors.
(D) If a program does not compile, then it has no syntax errors.

<details>
**Solution:** Let C = compiles, N = no syntax errors. Statement is `C → N`.
Contrapositive = `¬N → ¬C` = "if it has syntax errors, then it does not compile."

**Answer: (B)**

Note: (A) is the converse. (C) is the inverse. (D) is nonsense.
</details>

---

### Q9. Valid argument or fallacy?
Premises: "If the server is down, the site is unreachable." and "The site is unreachable."
Conclusion: "The server is down."
Is this valid?

<details>
**Solution:** Let D = server down, U = unreachable. Premises: `D → U` and `U`. Conclusion: `D`.

This is **affirming the consequent** — an **invalid** fallacy. It assumes the converse `U → D`.

*Counterexample in reality:* the site could be unreachable due to a DNS failure while the server is perfectly fine.

**Answer: Invalid.**
</details>

---

### Q10. Exportation
Show that `(p ∧ q) → r ≡ p → (q → r)`.

<details>
**Solution:** Convert both sides to ¬/∨ form.

LHS: `¬(p ∧ q) ∨ r` = `(¬p ∨ ¬q) ∨ r` = `¬p ∨ ¬q ∨ r`

RHS: `¬p ∨ (q → r)` = `¬p ∨ (¬q ∨ r)` = `¬p ∨ ¬q ∨ r`

Identical ⟹ **equivalent** ✓

*This is the Exportation law. Genuinely useful for restructuring multi-premise proofs.*
</details>

---

### Q11. Counting Boolean functions
How many distinct Boolean functions of 3 variables exist?

<details>
**Solution:** Truth table for 3 variables has 2³ = 8 rows. Each row's output is independently T or F.

Total = 2⁸ = **256**
</details>

---

### Q12. XOR properties
Simplify `p ⊕ p ⊕ q`.

<details>
**Solution:** XOR is associative, so group as `(p ⊕ p) ⊕ q`.
`p ⊕ p ≡ F`, so we get `F ⊕ q` ≡ **q**

*Generalization worth remembering: XOR of an even number of copies of p is F; odd number is p. This is why XOR is used in parity checks and in cryptography — including the XOR-based obfuscation you'd have seen in security work.*
</details>

---

### Q13. Tautology check with implication chain
Is `((p → q) ∧ (q → r)) → (p → r)` a tautology?

<details>
**Solution:** Yes — this is **Hypothetical Syllogism**, and every valid rule of inference corresponds to a tautology.

*Quick argument instead of a 8-row table:* Assume the antecedent is true, so `p → q` and `q → r` both hold. Now assume p is true. Then q is true (first premise), then r is true (second premise). So `p → r` holds. The implication can never have a true antecedent with a false consequent.

**Answer: Tautology.**
</details>

---

### Q14. "Unless" translation
Translate: "The deployment will fail unless the tests pass."
Let F = deployment fails, T = tests pass.

<details>
**Solution:** "A unless B" means `¬B → A`.

**Answer: ¬T → F** (if tests don't pass, deployment fails)

Equivalent forms: `F ∨ T`, and `¬F → T`.
</details>

---

### Q15. Biconditional expansion
Express `p ↔ q` using only ¬ and ∧.

<details>
**Solution:**
- Start: `p ↔ q ≡ (p ∧ q) ∨ (¬p ∧ ¬q)`
- Need to remove ∨. Use De Morgan in reverse: `A ∨ B ≡ ¬(¬A ∧ ¬B)`
- Result: **¬( ¬(p ∧ q) ∧ ¬(¬p ∧ ¬q) )**

*This demonstrates that {¬, ∧} is functionally complete.*
</details>

---

# PART 3 — WHERE TO GET THE ACTUAL PYQs

I've written the questions above in GATE style, but you also need the **real past papers** — and there's exactly one place to get them properly:

**gateoverflow.in** — go to the Discrete Mathematics → Mathematical Logic → Propositional Logic tag. Every propositional logic question ever asked in GATE CS (1987 onwards, roughly 60–70 questions on this topic) is there with full community discussion.

**How to use it (this method matters more than the resource):**
1. Solve the question on paper, closed-book, timed at 2 minutes
2. Check your answer
3. **Read the discussion thread even when you got it right** — you'll frequently find a 3-line approach where you used 15 lines. That gap is the AIR-level skill
4. Log every mistake in your mistake notebook using the 3-line format: what I thought / what was actually true / how to catch it next time

**Video resources for today's topic specifically:**
- **Gate Smashers** — Propositional Logic playlist: fastest clean first pass on connectives and truth tables, good if any section above felt shaky
- **GO Classes** — Mathematical Logic playlist: taught by AIR 33 and AIR 53 holders, goes into proof-level rigor. This is your *second* pass, after concepts are solid. Use for the tough equivalence and validity problems
- **Ravindrababu Ravula** — Discrete Math / Logic lectures: rigorous, slower-paced, excellent for building intuition on implication and inference rules
- **Neso Academy** — Discrete Mathematics playlist: cleanest beginner explanations of truth tables if you want extra reinforcement

**Standard textbook (optional but excellent):** Kenneth Rosen, *Discrete Mathematics and Its Applications*, Chapter 1 (sections 1.1–1.3). Solve the exercises at the end of 1.1, 1.2, 1.3 — Rosen's problem sets are where GATE gets much of its inspiration.

---

# PART 4 — TODAY'S CHECKLIST

Tick each off before ending the day:

- [ ] Can write all six truth tables (¬, ∧, ∨, ⊕, →, ↔) from memory in under 2 minutes
- [ ] Can state why `p → q` is true when p is false, in my own words
- [ ] Have memorized `p → q ≡ ¬p ∨ q` and `¬(p → q) ≡ p ∧ ¬q`
- [ ] Can recite both De Morgan's laws instantly
- [ ] Know that contrapositive ≡ original, and converse ≡ inverse
- [ ] Can correctly place "necessary" and "sufficient" on the right side of an arrow
- [ ] Know the two classic fallacies by name
- [ ] Know that number of Boolean functions of n variables = 2^(2ⁿ)
- [ ] Solved all 15 questions above on paper before reading solutions
- [ ] Solved at least 10 real PYQs from gateoverflow's propositional logic tag
- [ ] Started my mistake log file — even if it only has one entry today

---

# PART 5 — WHAT TOMORROW LOOKS LIKE (Day 2 preview)

Tomorrow is **First Order Logic** — quantifiers (∀ "for all", ∃ "there exists") and predicates. It builds directly on today: everything you learned about implication and negation gets extended to statements with variables, and the negation rules become `¬∀x P(x) ≡ ∃x ¬P(x)`.

Today's material is the foundation for that, so if anything in Part 1 felt unstable, spend 30 extra minutes on it tonight rather than carrying the gap forward. Propositional logic errors compound.