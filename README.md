# Logic
Book: Logic In Computer Science by M.Huth and M.Ryan
## Propositional Logic
$\phi_1, \phi_2,...,\phi_n \vdash \psi$
Here, $\phi_i$ is the premise and $\psi$ is the conlusion. 

Rules for natural deduction:
1. $\wedge$ (AND)
   1. $\frac{\phi\quad\psi}{\phi \wedge \psi}_{\wedge i}$
   2. $\frac{\phi \wedge \psi}{\phi}_{\wedge e_1}$
   3. $\frac{\phi \wedge \psi}{\psi}_{\wedge e_2}$ 
2. $\neg\neg$ (Double negation)
   1. $\frac{\neg\neg\phi}{\phi}_{\neg\neg e}$ 
   2. $\frac{\phi}{\neg\neg\phi}_{\neg\neg i}$
3. $\implies$ (Implies)
   1. Modus Ponens: $\frac{\phi\quad\phi\implies\psi}{\psi}_{\implies e/MP}$
   2. Modus Tollens: $\frac{\phi\implies\phi\quad\neg\psi}{\neg\phi}_{MT}$
   3. For introducting an implication, make an assumption, arrive at a result, then create an implication from the assumption to the result. TODO: Add symbolic expression of the same
4. If $(\phi\vdash\psi) \wedge (\psi\vdash\phi)$ then $\phi \dashv \vdash \psi$
5. $\vee$ (Disjunction) 
   1. $\frac{\phi}{\phi\vee\psi}_{\vee i}$  
   2. $\frac{\psi}{\phi\vee\psi}_{\vee i}$  
   3. For eliminating a disjunction, arrive at another term $\chi$ from all terms in the disjunction and then conclude $\chi$. TODO: Add symbolic expression for the same. 
6. $\neg$ (Negation)
   1. $\frac{\phi\quad\neg\phi}{\perp}_{\neg e}$
   2. For introducing a negation $\neg\phi$, arrive at a contradiction from $\phi$
7. $\perp$ (Contradiction)
   1. $\frac{\perp}{\phi}_{\perp e}$
8. Proof by Contradiction
   1. Start from a $\neg\phi$ and arrive at a contradiction($\perp$). Then infer $\phi$
9. Law of Excluded Middle ($LEM$) 
   1.  $\vdash \phi \vee \neg\phi$
   2.  Used to prove $p \implies q \vdash \neg p \vee q$

#### Soundness:
> If, for all valuations in which all $\phi_1, \phi_2, ..., \phi_n$ evaluate to $T$, $\psi$ evaluates to T as well, we say that $\phi_1, \phi_2, ..., \phi_n \models \psi$

$\models$ is also called semantic entailment relation(truth table).

#### Completeness

$\phi_1, \phi_2, ..., \phi_n \vdash \psi$ is valid iff $\phi_1, \phi_2, ..., \phi_n \models \psi$ holds

#### Satisfiability
$\phi$ is satisfiable if it has a valuation that evaluates to $T$. 

#### Semantic Equivalence
$\phi \equiv \psi$ holds iff $\phi \models \psi$ and $\psi \models \phi$

### Normals forms 
#### Conjunctive Normal Form (CNF)
$L ::= p \mid \neg p$  
$D ::= L \mid L \vee D$  
$C ::= D \mid D \vee C$  
Eg: $(\neg q \vee p \vee r) \wedge (\neg p \vee r) \wedge q$

Fast check for validity of $\models \psi$: In the CNF($\phi_1, ..., \phi_n \models \psi$), look for $\phi$ and $\neg\phi$ in the conjuncts. If not found, it is not valid. 

To convert a propositional logic formula to CNF:
1. Remove all implications using $p\implies q \vdash \neg p \vee q$
2. Convert to Negation normal form(NNF) using De-Morgan's Laws
3. Do case analysis:
   1. If $\phi$ is literal/atom, return $\phi$
   2. If $\phi$ is a conjunction, get the CNF of it too
   3. Apply distributivity law on CNFs


#### Horn Clauses
Grammar for Horn Clauses:  
$P ::= \perp  \mid \top \mid P$  
$A ::= P \mid P \wedge A$  
$C ::= A \rightarrow P$  
$H ::= C \mid C \wedge H$  
> Horn formulas are conjunctions of Horn clauses. $A$ Horn clause is an implication whose assumption $A$ is a conjunction of propositions of type $P$ and whose conclusion is also of type $P$.

Eg: $(p_2 \wedge p_3 \wedge p_5 \implies p_{13}) \wedge (\top \implies p_5)\wedge(p_5 \wedge p_{11} \implies \perp)$