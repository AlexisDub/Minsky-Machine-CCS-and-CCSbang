# Minsky Machine en CCSd et CCS!

**Projet réalisé par DUBARRY Alexis et NOEL Shanti**

Ce projet présente deux implémentations d’une machine de Minsky à deux registres :

1. **CCSd** (CCS déterministe, supporté par CAAL, sans opérateur de réplication)
2. **CCS!** (CCS avec réplication)

Les deux approches s’appuient sur la méthode présentée dans le papier :  
Busi, Ferrara & Gorrieri (1999), *On the Expressive Power of Recursion, Replication and Iteration in Process Calculi*, § 4.3.1.

---

## Table des matières

- [Lancement](#lancement)  
- [1. Encodage en CCSd](#1-encodage-en-ccsd)  
- [2. Encodage en CCS!](#2-encodage-en-ccs)  
- [3. Vérification sous CAAL](#3-v%C3%A9rification-sous-caal)  
- [Références](#r%C3%A9f%C3%A9rences)  

---

## Lancement

1. Ouvrez [l’interface CAAL](https://caal.cs.aau.dk/)  
2. Allez dans **Project → Load → From file**  
3. Sélectionnez le fichier `minsky_ccsd.caal` pour CCSd ou `minsky_ccsbang.caal` pour CCS!

---

## 1. Encodage en CCSd

Les définitions de variables en CCS determinstique (CCSd) sont déjà supportées par CAAL.  
Il suffit d’implémenter la machine conformément à la méthode décrite dans le papier de Busi et al.

---

## 2. Encodage en CCS!

Dans le papier, la réplication (`!`) peut être encodée à l’aide de la récursion :

```
P := D
où D :=def P | D
```

Pour que CAAL accepte la définition récursive, on introduit un préfixe silencieux `tau` :
```
D_Zj = tau.( Zj | D_Zj );
```

Le système devient alors :
```
System = Inst1 | D_Z1 | D_Z2;
```

---

## 3. Vérification sous CAAL

Dans l’onglet **Vérification**, utilisez la formule suivante :
```
X min= <w>tt or <->X
```
Cette propriété garantit que toutes les exécutions atteignent l’état `w`.

---

## Références

- Busi, Ferrara & Gorrieri, *On the Expressive Power of Recursion, Replication and Iteration in Process Calculi*, 1999.
