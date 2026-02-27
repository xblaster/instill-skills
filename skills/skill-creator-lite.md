---
name: skill-creator-lite
description: Crée, améliore et teste des skills Claude de manière autonome, sans dépendances externes. Utilise ce skill quand l'utilisateur veut créer un nouveau skill, modifier un skill existant, ou tester qu'un skill fonctionne bien — même sans accès à des scripts Python, CLI ou navigateur. Déclenche ce skill pour tout ce qui ressemble à "crée-moi un skill pour X", "améliore ce skill", "ce skill ne se déclenche pas bien", ou "je veux automatiser ce workflow".
---

# Skill Creator Lite

Crée et itère sur des skills Claude **sans aucune dépendance externe** : pas de scripts Python, pas de CLI, pas de navigateur. Tout se passe dans la conversation.

## Vue d'ensemble du processus

```
Comprendre l'intention → Rédiger le skill → Tester dans la conversation → Évaluer → Améliorer → Répéter
```

L'idée centrale : tu *simules* toi-même l'exécution du skill sur des prompts de test, tu montres les résultats à l'utilisateur, et tu itères jusqu'à satisfaction.

---

## Étape 1 — Comprendre l'intention

Avant d'écrire quoi que ce soit, pose les bonnes questions. Si la conversation contient déjà le contexte (un workflow montré, des corrections faites), extrais les réponses depuis l'historique avant de demander.

**Ce qu'il faut clarifier :**

1. Que doit faire ce skill concrètement ? Quel problème résout-il ?
2. Dans quelles situations doit-il se déclencher ? Quels types de phrases ou de contextes ?
3. Quel est le format de sortie attendu ? (fichier, texte structuré, réponse conversationnelle...)
4. Y a-t-il des cas limites importants à gérer ?

Pour les skills avec des sorties **objectivement vérifiables** (transformation de fichier, extraction de données, génération de code, workflow précis), propose de créer des cas de test. Pour les skills avec des sorties **subjectives** (style d'écriture, analyse créative), les tests qualitatifs suffisent.

---

## Étape 2 — Rédiger le skill

### Structure d'un skill

Un skill, c'est un dossier avec :
- `SKILL.md` (obligatoire) — frontmatter YAML + instructions en markdown
- Des ressources optionnelles : scripts, références, assets

```
mon-skill/
├── SKILL.md
└── references/   (optionnel, pour les skills complexes)
    └── details.md
```

### Anatomie du SKILL.md

```markdown
---
name: nom-du-skill
description: Ce que fait le skill ET dans quels contextes le déclencher.
             Sois un peu "pushy" : mentionne explicitement les cas d'usage
             pour éviter que le skill soit sous-utilisé.
---

# Titre

Intro courte qui explique l'objectif.

## Section principale

Instructions claires, en mode impératif.
Explique le *pourquoi* plutôt que d'empiler des MUST en majuscules.
```

### Principes de rédaction

**Explique le pourquoi.** Les LLMs sont intelligents — si tu expliques la raison d'une instruction, ils vont mieux la respecter et l'adapter aux cas non prévus. Évite les "TOUJOURS faire X" sans justification.

**Reste concis.** Vise moins de 500 lignes. Si tu dépasses, c'est souvent le signe qu'il faut extraire des sous-références.

**Format de sortie.** Si le skill a un output structuré, définis-le explicitement avec un exemple ou un template.

**Exemples.** Quand c'est utile, montre des exemples entrée/sortie. Ça ancre mieux les instructions abstraites.

**Description = déclencheur.** La description dans le frontmatter est ce que Claude lit pour décider d'utiliser le skill. Elle doit couvrir : ce que fait le skill + les contextes typiques d'usage + quelques mots-clés que l'utilisateur pourrait employer.

---

## Étape 3 — Définir des cas de test

Propose 2 à 4 prompts réalistes — le genre de chose qu'un vrai utilisateur écrirait. Montre-les à l'utilisateur et demande confirmation avant de continuer.

**Format des cas de test :**

```
Cas 1 — [nom descriptif]
Prompt : "..."
Résultat attendu : [description de ce qu'on veut obtenir]
```

Un bon cas de test :
- Ressemble à un vrai usage (avec du contexte, des détails concrets)
- N'est pas trop évident ni trop ambigu
- Couvre des angles différents du skill

---

## Étape 4 — Simuler l'exécution et évaluer

### Comment simuler

Pour chaque cas de test, tu joues toi-même le rôle de "Claude avec accès au skill" :

1. Lis le SKILL.md que tu viens de rédiger
2. Exécute la tâche du prompt de test en suivant les instructions du skill
3. Produis l'output comme si tu étais l'agent qui utilise le skill
4. Présente le résultat dans la conversation

Fais ça pour chaque cas, un par un ou en parallèle dans ta réponse.

### Présenter les résultats à l'utilisateur

Organise les résultats clairement :

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
CAS 1 — [nom]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Prompt : "..."

Résultat avec le skill :
[output produit]

Questions pour l'utilisateur :
- Est-ce que le format correspond à ce que tu voulais ?
- Quelque chose manque ou te semble de trop ?
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

### Évaluation qualitative (toujours)

Pose des questions ciblées après chaque résultat :
- Le format est-il bon ?
- Le niveau de détail est-il adapté ?
- Y a-t-il des choses superflues ?
- Est-ce que ça couvre le cas d'usage réel ?

### Évaluation quantitative (quand pertinent)

Pour les skills avec des critères vérifiables, définis des assertions simples et vérifie-les toi-même sur l'output produit :

```
Assertions pour le cas 1 :
✅ L'output contient un titre H1
✅ Les étapes sont numérotées
❌ Le résumé exécutif est absent (attendu mais manquant)
```

Présente le bilan après chaque itération :

```
Bilan itération 1 :
- Cas 1 : 3/4 assertions passées
- Cas 2 : 4/4 assertions passées  
- Cas 3 : 2/4 assertions passées ← à améliorer
```

---

## Étape 5 — Itérer

### Comment lire le feedback

Le feedback vide ou positif = ça marche, passe à la suite.
Le feedback ciblé = comprends le problème sous-jacent avant de modifier.

**Ne sur-optimise pas pour les exemples.** Tu travailles sur 2-4 cas, mais le skill sera utilisé dans des milliers de contextes différents. Généralise plutôt qu'ajuste finement.

### Stratégies d'amélioration

- **Problème de format :** Ajoute un template ou un exemple de sortie
- **Problème de déclenchement :** Reformule la description frontmatter
- **Comportement trop rigide :** Remplace les MUST par des explications du pourquoi
- **Output trop verbeux :** Précise la cible de longueur et ce qu'il faut éliminer
- **Output trop pauvre :** Identifie ce qui manque et explique pourquoi c'est important

### Boucle d'itération

```
Modifier le skill → Re-simuler les cas → Présenter les nouveaux résultats → Feedback → Recommencer
```

Organise visuellement les itérations dans la conversation :

```
═══ ITÉRATION 2 ═══════════════════════
Changements apportés :
- Ajout d'un template de sortie
- Reformulation de la section "Cas limites"

[Résultats des cas de test...]
```

Continue jusqu'à ce que :
- L'utilisateur dit qu'il est satisfait
- Le feedback est vide ou minimal
- Tu ne fais plus de progrès significatif

---

## Étape 6 — Optimiser la description (déclencheur)

Une fois le skill stable, propose d'optimiser sa description frontmatter pour qu'il se déclenche au bon moment.

### Créer des requêtes de test pour le déclenchement

Génère 16-20 requêtes, réparties entre :
- **Doit déclencher (8-10)** : Phrasés variés, certains implicites, certains sans nommer le skill
- **Ne doit pas déclencher (8-10)** : Cas adjacents, faux positifs potentiels, domaines similaires mais différents

Qualité des requêtes : concrètes, réalistes, avec du contexte. Évite les cas évidents dans les deux sens.

**Exemple de bonne requête "doit déclencher" :**
> "j'ai un fichier xlsx que mon boss m'a envoyé, Sales_Q4_final_v3.xlsx, il faut que j'ajoute une colonne avec la marge en % — le CA est en colonne C et les coûts en D"

**Exemple de mauvaise requête "ne doit pas déclencher" :**
> "écris une fonction fibonacci" ← trop évident, ne teste rien d'utile

### Évaluer et améliorer la description

Présente les requêtes à l'utilisateur pour validation, puis simule le déclenchement sur chacune :

```
ÉVALUATION DU DÉCLENCHEMENT
Description actuelle : "..."

Requête : "..."
→ Déclencherait-il ? [OUI/NON]
→ Devrait-il ? [OUI/NON]
→ Résultat : ✅ correct / ❌ faux positif / ❌ faux négatif
```

Itère sur la description jusqu'à maximiser le score.

---

## Étape 7 — Livrer le skill

Présente le skill final dans un bloc de code markdown complet, prêt à copier :

````
```markdown
---
name: mon-skill
description: [description optimisée]
---

[Corps du SKILL.md]
```
````

Donne un résumé de ce qui a été accompli :
- Nombre d'itérations
- Principaux changements
- Cas de test couverts
- Score de déclenchement final (si l'optimisation a été faite)

---

## Notes sur la communication

Adapte ton niveau de langage au profil de l'utilisateur. Si tu parles à quelqu'un qui découvre les skills, évite le jargon sans l'expliquer. Si c'est un développeur expérimenté, vas droit au but.

En cas de doute sur le niveau, explique brièvement les termes techniques la première fois que tu les utilises.
