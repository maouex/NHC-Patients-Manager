# Guide des Templates d'Ordonnance Word

## Comment préparer votre template Word

Pour que vos templates Word fonctionnent correctement avec le système de génération d'ordonnances, vous devez utiliser des **placeholders** (marqueurs de substitution) dans votre document.

## Syntaxe des placeholders

Utilisez la syntaxe `{nom_du_champ}` dans votre document Word.

**Exemple :**
```
Je soussigné {medecin_nom}, certifie avoir examiné {patient_nom_complet}
```

## Placeholders disponibles

### Informations du Médecin
- `{medecin_nom}` - Nom complet du médecin
- `{nom_medecin}` - Nom complet du médecin (variante)
- `{medecin}` - Nom complet du médecin (variante)

### Informations du Patient
- `{patient_prenom}` - Prénom du patient
- `{patient_nom}` - Nom de famille du patient
- `{patient_nom_complet}` - Prénom et nom complet du patient
- `{nom_complet}` - Prénom et nom complet (variante)
- `{patient_date_naissance}` - Date de naissance du patient (format JJ/MM/AAAA)
- `{date_naissance}` - Date de naissance (variante)
- `{patient_id}` - Numéro d'identification NHC du patient
- `{cycle}` - Cycle actuel du patient

### Dates de l'Ordonnance
- `{date_debut}` - Date de début de l'ordonnance (format JJ/MM/AAAA)
- `{date_debut_ordonnance}` - Date de début (variante)
- `{date_fin}` - Date de fin de l'ordonnance (format JJ/MM/AAAA)
- `{date_fin_ordonnance}` - Date de fin (variante)
- `{duree}` - Durée de l'ordonnance (ex: "3 mois")

### Date du Jour
- `{date_jour}` - Date du jour de génération (format JJ/MM/AAAA)
- `{date}` - Date du jour (variante)
- `{current_date}` - Date du jour (variante)

## Exemple de Template Word

Voici un exemple de template d'ordonnance :

```
──────────────────────────────────────────────────────────
                    ORDONNANCE MÉDICALE
──────────────────────────────────────────────────────────

Médecin prescripteur : {medecin_nom}

Date : {date_jour}

──────────────────────────────────────────────────────────
INFORMATIONS PATIENT
──────────────────────────────────────────────────────────

Nom et Prénom : {patient_nom_complet}
Date de naissance : {patient_date_naissance}
N° Patient : {patient_id}

──────────────────────────────────────────────────────────
PRESCRIPTION
──────────────────────────────────────────────────────────

Je soussigné {medecin_nom}, certifie avoir examiné
{patient_nom_complet} et prescris le traitement suivant :

[Insérez ici votre prescription]

Période de validité :
Du {date_debut} au {date_fin}
Durée : {duree}

──────────────────────────────────────────────────────────

Signature :


{medecin_nom}
```

## Comment créer votre template

### Méthode 1 : Modifier un document existant
1. Ouvrez votre document Word d'ordonnance existant
2. Remplacez les informations variables par les placeholders correspondants
3. Sauvegardez le document

### Méthode 2 : Créer un nouveau template
1. Créez un nouveau document Word
2. Concevez votre mise en page d'ordonnance
3. Insérez les placeholders aux endroits où les informations doivent apparaître
4. Sauvegardez le document

## Conseils importants

✅ **À FAIRE :**
- Utilisez exactement la syntaxe `{nom_du_champ}` (avec accolades)
- Vérifiez l'orthographe des placeholders
- Testez votre template après l'avoir créé

❌ **À NE PAS FAIRE :**
- N'utilisez pas d'autres syntaxes comme `{{nom}}`, `[nom]`, ou `<nom>`
- N'ajoutez pas d'espaces dans les accolades : `{ nom }` ne fonctionnera pas
- N'utilisez pas de placeholders inexistants

## Uploader votre template

1. Allez dans **Paramètres** → **Templates d'Ordonnance**
2. Cliquez sur **Nouveau Template**
3. Sélectionnez votre fichier Word (.docx)
4. Donnez-lui un nom
5. Associez-le à un protocole si nécessaire

## Générer une ordonnance

1. Ouvrez la fiche d'un patient
2. Cliquez sur **Générer Ordonnance**
3. Sélectionnez votre template personnalisé
4. Choisissez les dates de début et fin
5. Cliquez sur **Générer**
6. Le fichier Word sera téléchargé avec toutes les informations remplies !

## Dépannage

### Le fichier téléchargé ne contient pas les bonnes informations
- Vérifiez que vous utilisez la bonne syntaxe : `{nom_du_champ}`
- Vérifiez l'orthographe des placeholders
- Assurez-vous que votre fichier est au format .docx (pas .doc)

### Les placeholders apparaissent toujours dans le document final
- Vérifiez que vous utilisez les accolades simples `{` et `}`, pas doubles
- Vérifiez qu'il n'y a pas d'espaces dans les accolades

### Erreur lors de la génération
- Assurez-vous que votre document Word n'est pas corrompu
- Réessayez d'uploader le template
- Vérifiez la console du navigateur pour plus de détails

## Support

Si vous rencontrez des problèmes, vérifiez :
1. Que votre document est au format .docx
2. Que les placeholders utilisent la syntaxe correcte
3. Que toutes les informations du patient sont remplies dans sa fiche
