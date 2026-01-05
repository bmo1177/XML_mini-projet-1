# 📘 Mini-Projet XML : Solutions Complètes

> **Travaux Pratiques sur le Formalisme XML**  
> Ce projet couvre la syntaxe XML, la validation DTD/XSD et les requêtes XPath

[![XML](https://img.shields.io/badge/XML-1.0-orange.svg)](https://www.w3.org/TR/xml/) [![XSD](https://img.shields.io/badge/XSD-Schema-blue.svg)](https://www.w3.org/TR/xmlschema-0/) [![XPath](https://img.shields.io/badge/XPath-2.0-green.svg)](https://www.w3.org/TR/xpath20/)

---

## 📂 Structure du Projet

```
MiniProjet/
├── 1. Question 1/
│   └── questions-les7erreurs/
│       ├── document_original.xml          # Document avec erreurs
│       └── document_corrige.xml           # Document corrigé
├── 2. Exercice01/
│   ├── dtd1.dtd                           # DTD 1
│   ├── dtd2.dtd                           # DTD 2
│   ├── doc_valide_dtd1_nondtd2.xml       # Valide pour DTD1 seulement
│   └── doc_valide_dtd2_nondtd1.xml       # Valide pour DTD2 seulement
├── 3. Exercice 02/
│   ├── schema_xml.xsd                     # Schéma XSD
│   └── xml_valide_pour_xsd.xml           # Document valide pour le schéma
├── 4. Exercice XPath/
│   ├── cinema.xml                         # Base de données XML
│   ├── queries.xbook                      # Fichier de requêtes XPath
│   └── screenshots/
│       ├── 1.png                          # Requêtes 1-4
│       ├── 2.png                          # Requêtes 5-8
│       ├── 3.png                          # Requêtes 9-12
│       └── 4.png                          # Requête 13
└── README.md
```

---

## 📋 Table des Matières

1. [Question 1 : Correction des 7 erreurs XML](https://claude.ai/chat/077ca655-a1ff-4591-aa86-a402593aacee#1-question-1--correction-des-7-erreurs-xml)
2. [Exercice 1 : Comparaison de DTD](https://claude.ai/chat/077ca655-a1ff-4591-aa86-a402593aacee#2-exercice-1--comparaison-de-dtd)
3. [Exercice 2 : Schéma XML (XSD)](https://claude.ai/chat/077ca655-a1ff-4591-aa86-a402593aacee#3-exercice-2--sch%C3%A9ma-xml-xsd)
4. [Exercice XPath : Requêtes sur cinema.xml](https://claude.ai/chat/077ca655-a1ff-4591-aa86-a402593aacee#4-exercice-xpath--requ%C3%AAtes-sur-cinemaxml)
5. [Outils et Validation](https://claude.ai/chat/077ca655-a1ff-4591-aa86-a402593aacee#-outils-et-validation)
6. [Concepts Clés](https://claude.ai/chat/077ca655-a1ff-4591-aa86-a402593aacee#-concepts-cl%C3%A9s)

---

## 1. Question 1 : Correction des 7 erreurs XML

### 🔴 Document XML original (avec erreurs)

<details> <summary>Cliquez pour voir le code</summary>

```xml
<?xml version="3.0" encoding="utf-8"?>
<logiciel Comptablite>
    <version>1</version/>
    <user>
    <uid>bgirot</uid>
    </user>
    <contact>
    <lastName>Girot</lastName>
    <firstName>Bernadette</firstName>
    <email>ggirot@petites.fleurs.com</email>
    </contact>
    <author aulda="ghuret" lastName="Huret" firstName="George" organism="">
    <company>
    <labld>3987</labld>
    <name>Analyse Informatique des Données & Informations</name>
    <shortName></shortName>
    </company>
    </author>
    <author aulda="mgirard" lastName="Girard" firstName="Matin" firstName="Matin" organism="">
    <company>
    <labld>6670</labld>
    <name>La compta en vogue</name>
    <shortName>Vogue la compta</shortName>
    </company>
    <company>
    <labld>4621</labld>
    <name>En avant les chiffres</name>
    <shortName>EAC</shortName>
    </author>
    </company>
    </logiciel Comptablite>
    <date_mise_en_service>
    2007–09–17
    </date_mise_en_service>

</details>

### 🔍 Les 7 erreurs identifiées

|#|🔴 Erreur|✅ Correction|📝 Explication|
|---|---|---|---|
|**1**|`version="3.0"`|`version="1.0"`|Les versions XML valides sont **1.0** ou **1.1** uniquement|
|**2**|`<logiciel Comptablite>`|`<logiciel_Comptabilite>`|Les noms de balises **ne peuvent pas contenir d'espaces**|
|**3**|`<version>1</version/>`|`<version>1</version>`|**Syntaxe mixte invalide** : choisir soit `<tag/>` soit `<tag></tag>`|
|**4**|`&` dans le texte|`&amp;`|Le caractère `&` doit être **échappé en entité** (`&amp;`)|
|**5**|`firstName="Matin"` × 2|Supprimer le doublon|Un attribut **ne peut apparaître qu'une seule fois** par élément|
|**6**|`</author></company>`|`</company></author>`|Les balises doivent être fermées dans l'**ordre inverse d'ouverture** (LIFO)|
|**7**|`<date_mise_en_service>` après `</logiciel>`|Déplacer avant `</logiciel>`|Un document XML doit avoir **un seul élément racine** englobant tout|

```xml
<?xml version="1.0" encoding="utf-8"?>
<logiciel_Comptabilite>
    <version>1</version>
    <user>
        <uid>bgirot</uid>
    </user>
    <contact>
        <lastName>Girot</lastName>
        <firstName>Bernadette</firstName>
        <email>ggirot@petites.fleurs.com</email>
    </contact>
    <author aulda="ghuret" lastName="Huret" firstName="George" organism="">
        <company>
            <labld>3987</labld>
            <name>Analyse Informatique des Données &amp; Informations</name>
            <shortName></shortName>
        </company>
    </author>
    <author aulda="mgirard" lastName="Girard" firstName="Matin" organism="">
        <company>
            <labld>6670</labld>
            <name>La compta en vogue</name>
            <shortName>Vogue la compta</shortName>
        </company>
        <company>
            <labld>4621</labld>
            <name>En avant les chiffres</name>
            <shortName>EAC</shortName>
        </company>
    </author>
    <date_mise_en_service>2007-09-17</date_mise_en_service>
</logiciel_Comptabilite>
```


> **✨ Règles à retenir :**
> 
> - Un document **bien formé** respecte la syntaxe XML
> - Un document **valide** respecte en plus une DTD ou un schéma XSD

---

## 2. Exercice 1 : Comparaison de DTD

### 📜 DTD 1 vs DTD 2

|DTD|Expression Régulière|Description|
|---|---|---|
|**DTD 1**|`((a,b*,a) \| b)*`|Répétition de : **soit** `a` + 0+ `b` + `a`, **soit** un `b` seul|
|**DTD 2**|`(a \| (b,a*,b))*`|Répétition de : **soit** un `a` seul, **soit** `b` + 0+ `a` + `b`|

### 📄 a) Document valide pour DTD1 mais **pas** DTD2

```xml
<?xml version="1.0"?>
<!DOCTYPE root [
    <!ELEMENT root ((a,b*,a)|b)*>
    <!ELEMENT a (#PCDATA)>
    <!ELEMENT b (#PCDATA)>
]>
<root>
    <a>contenu1</a>
    <b>contenu2</b>
    <a>contenu3</a>
</root>
```

**💡 Explication :**

- ✅ **DTD1** : Suit le pattern `(a, b*, a)` avec un seul `b`
- ❌ **DTD2** : Invalide car `b` n'est pas suivi d'un autre `b` (nécessite `b, a*, b`)

### 📄 b) Document valide pour DTD2 mais **pas** DTD1

```xml
<?xml version="1.0"?>
<!DOCTYPE root [
    <!ELEMENT root (a|(b,a*,b))*>
    <!ELEMENT a (#PCDATA)>
    <!ELEMENT b (#PCDATA)>
]>
<root>
    <b>contenu1</b>
    <a>contenu2</a>
    <a>contenu3</a>
    <b>contenu4</b>
</root>
```

**💡 Explication :**

- ✅ **DTD2** : Suit le pattern `(b, a*, b)` avec deux `a` au milieu
- ❌ **DTD1** : Invalide car DTD1 exige soit `b` seul, soit `(a, b*, a)`

---

## 3. Exercice 2 : Schéma XML (XSD)

### 🎯 Concepts du schéma

Le schéma définit :

- Un type **abstrait** `I` (Integer avec attribut `sign` optionnel)
- Un type **dérivé** `P` (Positive, restreint à `nonNegativeInteger`, `sign` interdit)
- Un élément racine contenant **2 à 3** éléments `i` de type `I`

### 📐 Schéma XSD

<details> <summary>Cliquez pour voir le schéma complet</summary>

```xml
<?xml version="1.0" encoding="UTF-8"?>
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema">
    
    <!-- Type abstrait : entier avec signe optionnel -->
    <xsd:complexType name="I" abstract="true">
        <xsd:simpleContent>
            <xsd:extension base="xsd:integer">
                <xsd:attribute name="sign">
                    <xsd:simpleType>
                        <xsd:restriction base="xsd:string">
                            <xsd:enumeration value="+"/>
                            <xsd:enumeration value="-"/>
                        </xsd:restriction>
                    </xsd:simpleType>
                </xsd:attribute>
            </xsd:extension>
        </xsd:simpleContent>
    </xsd:complexType>
    
    <!-- Type dérivé : entier positif sans signe -->
    <xsd:complexType name="P">
        <xsd:simpleContent>
            <xsd:restriction base="I">
                <xsd:simpleType>
                    <xsd:restriction base="xsd:nonNegativeInteger"/>
                </xsd:simpleType>
                <xsd:attribute name="sign" use="prohibited"/>
            </xsd:restriction>
        </xsd:simpleContent>
    </xsd:complexType>
    
    <!-- Élément racine : 2 à 3 éléments i -->
    <xsd:element name="root">
        <xsd:complexType>
            <xsd:sequence>
                <xsd:element name="i" type="I" minOccurs="2" maxOccurs="3"/>
            </xsd:sequence>
        </xsd:complexType>
    </xsd:element>
    
</xsd:schema>
```

</details>

### ✅ Document XML valide

```xml
<?xml version="1.0" encoding="UTF-8"?>
<root xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
      xsi:noNamespaceSchemaLocation="schema_xml.xsd">
    <i xsi:type="P">42</i>
    <i xsi:type="P">100</i>
</root>
```

**✅ Conditions de validation :**

- ✔️ Contient exactement **2 éléments** `i` (entre 2 et 3)
- ✔️ Type `P` spécifié via `xsi:type` (car `I` est abstrait)
- ✔️ Valeurs **entières non-négatives** (42, 100)
- ✔️ Attribut `sign` **absent** (interdit par le type `P`)

---

## 4. Exercice XPath : Requêtes sur cinema.xml

### 🎬 Structure du document cinema.xml

<details> <summary>Cliquez pour voir le document complet</summary>

```xml
<?xml version="1.0" encoding="UTF-8"?>
<cinema>
    <film id="lb78" type="comédie">
        <titre>Les Bronzés</titre>
        <annee>1978</annee>
        <realisateur>Patrice Leconte</realisateur>
        <role>
            <nom>Popeye</nom>
            <acteur>Thierry Lhermite</acteur>
        </role>
        <role>
            <nom>Jean-Claude Dusse</nom>
            <acteur>Michel Blanc</acteur>
        </role>
    </film>
    <film id="gf94" type="comédie">
        <titre>Grosse fatigue</titre>
        <annee>1994</annee>
        <realisateur>Michel Blanc</realisateur>
        <role>
            <nom>Patrick Olivier</nom>
            <acteur>Michel Blanc</acteur>
        </role>
        <role>
            <nom>Carole Bouquet</nom>
            <acteur>Carole Bouquet</acteur>
        </role>
        <prix>Cannes, meilleur scénario</prix>
    </film>
    <film id="av83" type="aventure">
        <titre>L'Avaleur de sabres</titre>
        <annee>1983</annee>
        <realisateur>Philippe Clair</realisateur>
        <role>
            <nom>Morin</nom>
            <acteur>Philippe Clair</acteur>
        </role>
        <role>
            <nom>Micheline Morin</nom>
            <acteur>Micheline Dax</acteur>
        </role>
    </film>
    <film id="am10" type="drame">
        <titre>Les Amours imaginaires</titre>
        <annee>2010</annee>
        <realisateur>Xavier Dolan</realisateur>
        <role><nom>Francis</nom><acteur>Xavier Dolan</acteur></role>
        <role><nom>Marie</nom><acteur>Monia Chokri</acteur></role>
        <role><nom>David</nom><acteur>Niels Schneider</acteur></role>
        <role><nom>La mère</nom><acteur>Anne Dorval</acteur></role>
        <role><nom>Le père</nom><acteur>Pierre Chagnon</acteur></role>
        <role><nom>L'amie</nom><acteur>Catherine Bégin</acteur></role>
        <prix>Prix de la jeunesse, Festival de Cannes</prix>
    </film>
    
    <producteur>
        <nom>Daniel Toscan du Plantier</nom>
        <film ref="gf94"/>
        <film ref="av83"/>
    </producteur>
    <producteur>
        <nom>Yves Rousset-Rouard</nom>
        <film ref="lb78"/>
        <film ref="am10"/>
    </producteur>
    <producteur>
        <nom>Claude Berri</nom>
        <film ref="lb78"/>
    </producteur>
</cinema>
```

</details>

### 🔍 Les 13 Requêtes XPath

|#|Description|Requête XPath|Résultats|
|---|---|---|---|
|**1**|Titres de tous les films|`//film/titre/text()`|Les Bronzés, Grosse fatigue, L'Avaleur de sabres, Les Amours imaginaires|
|**2**|Titres des films avec Michel Blanc|`//film[role/acteur='Michel Blanc']/titre/text()`|Les Bronzés, Grosse fatigue|
|**3**|Types de films distincts|`distinct-values(//film/@type)`|comédie, aventure, drame|
|**4**|Rôles de Michel Blanc|`//role[acteur='Michel Blanc']/nom/text()`|Jean-Claude Dusse, Patrick Olivier|
|**5**|Acteur principal (1er rôle)|`//film/role[1]/acteur/text()`|Thierry Lhermite, Michel Blanc, Philippe Clair, Xavier Dolan|
|**6**|Producteur après Yves Rousset-Rouard|`//producteur[nom='Yves Rousset-Rouard']/following-sibling::producteur[1]/nom/text()`|Claude Berri|
|**7**|Acteurs avant Michel Blanc (Leconte)|`//film[realisateur='Patrice Leconte']//role[acteur='Michel Blanc']/preceding-sibling::role/acteur/text()`|Thierry Lhermite|
|**8**|Réalisateurs (Blanc ET Lhermite)|`//film[role/acteur='Michel Blanc' and role/acteur='Thierry Lhermite']/realisateur/text()`|Patrice Leconte|
|**9**|Films avec >5 acteurs|`//film[count(role) > 5]/titre/text()`|Les Amours imaginaires|
|**10**|Réalisateurs-acteurs|`distinct-values(//film[realisateur = role/acteur]/realisateur/text())`|Michel Blanc, Philippe Clair, Xavier Dolan|
|**11**|Producteurs de comédies|`//producteur[film/@ref = //film[@type='comédie']/@id]/nom/text()`|Yves Rousset-Rouard, Claude Berri, Daniel Toscan du Plantier|
|**12**|Films sans prix|`//film[not(prix)]/titre/text()`|Les Bronzés, L'Avaleur de sabres|
|**13**|Acteurs avec "Morin" dans le rôle|`//role[contains(nom, 'Morin')]/acteur/text()`|Philippe Clair, Micheline Dax|

### 📸 Captures d'écran des résultats

| Requêtes  | Aperçu                                                                          |
| --------- | ------------------------------------------------------------------------------- |
| **1**     | ![Screenshot 1](https://claude.ai/chat/4.%20Exercice%20XPath/screenshots/1.png) |
| **2-4**   | ![Screenshot 2](https://claude.ai/chat/4.%20Exercice%20XPath/screenshots/2.png) |
| **5-10**  | ![Screenshot 3](https://claude.ai/chat/4.%20Exercice%20XPath/screenshots/3.png) |
| **11-13** | ![Screenshot 4](https://claude.ai/chat/4.%20Exercice%20XPath/screenshots/4.png) |

---

## 🛠️ Outils et Validation

### Outils utilisés

|Outil|Usage|Installation|
|---|---|---|
|**VS Code**|Éditeur principal|[code.visualstudio.com](https://code.visualstudio.com/)|
|**XML Tools** (extension)|Validation XML/XSD|`ext install DotJoshJohnson.xml`|
|**XPath Notebook** (extension)|Test des requêtes XPath|`ext install TatsuOu.xpath-notebook`|
|**xmllint**|Validation en ligne de commande|`sudo apt install libxml2-utils`|

### Commandes de validation

```bash
# Valider un document XML bien formé
xmllint --noout document.xml

# Valider avec une DTD
xmllint --noout --valid --dtdvalid schema.dtd document.xml

# Valider avec un XSD
xmllint --noout --schema schema.xsd document.xml

# Tester une requête XPath
xmllint --xpath "//film/titre/text()" cinema.xml
```

---

## 📚 Concepts Clés

### 🟢 XML Bien Formé (Well-Formed)

Un document XML est **bien formé** s'il respecte :

1. ✅ **Déclaration XML valide** : `<?xml version="1.0"?>`
2. ✅ **Un seul élément racine** englobant tout
3. ✅ **Balises correctement imbriquées** (fermeture LIFO)
4. ✅ **Attributs uniques** par élément
5. ✅ **Entités échappées** : `&amp;` `&lt;` `&gt;` `&quot;` `&apos;`
6. ✅ **Noms de balises valides** : pas d'espaces, commencent par lettre/underscore

### 🔵 XML Valide (Valid)

Un document XML est **valide** s'il est :

- ✅ **Bien formé** +
- ✅ **Conforme à une DTD ou XSD**

### 🟡 DTD (Document Type Definition)

**Opérateurs de cardinalité :**

- `*` : 0 ou plusieurs
- `+` : 1 ou plusieurs
- `?` : 0 ou 1
- `,` : séquence (ordre imposé)
- `|` : choix (alternatives)

**Exemple :**

```dtd
<!ELEMENT livre (titre, auteur+, (prix | gratuit)?)>
```

### 🟠 XSD (XML Schema Definition)

**Avantages sur DTD :**

- ✅ Typage fort des données
- ✅ Espaces de noms
- ✅ Types abstraits et héritage
- ✅ Contraintes avancées (patterns, ranges)

**Concepts clés :**

- `simpleType` : types de base (string, integer, date...)
- `complexType` : éléments avec sous-éléments ou attributs
- `restriction` : restreindre un type
- `extension` : étendre un type
- `abstract="true"` : type non instanciable

### 🟣 XPath (XML Path Language)

**Axes principaux :**

- `child::` (par défaut) : enfants directs
- `descendant::` ou `//` : tous les descendants
- `parent::` ou `..` : parent
- `ancestor::` : tous les ancêtres
- `following-sibling::` : frères suivants
- `preceding-sibling::` : frères précédents

**Prédicats :**

- `[position()=1]` ou `[1]` : premier élément
- `[last()]` : dernier élément
- `[@attribut='valeur']` : filtrage par attribut
- `[condition1 and condition2]` : ET logique
- `[condition1 or condition2]` : OU logique

**Fonctions utiles :**

- `count(nodeset)` : nombre de nœuds
- `contains(string, substring)` : test de sous-chaîne
- `distinct-values(nodeset)` : valeurs uniques
- `text()` : contenu textuel
- `not(condition)` : négation

---

## 📝 Conclusion

Ce mini-projet couvre **les 4 piliers du formalisme XML** :

|Pilier|Compétence|Exercice|
|---|---|---|
|🟢 **Syntaxe**|XML bien formé|Question 1 (7 erreurs)|
|🔵 **Validation**|DTD et contraintes|Exercice 1 (DTD1 vs DTD2)|
|🟡 **Schémas**|XSD, types, héritage|Exercice 2 (types abstraits)|
|🟣 **Requêtes**|XPath, navigation|Exercice XPath (13 requêtes)|

### 🎯 Compétences acquises

- ✅ Identifier et corriger des erreurs de syntaxe XML
- ✅ Comprendre les différences entre DTD similaires
- ✅ Créer et valider des documents avec XSD
- ✅ Maîtriser XPath pour extraire des données complexes
- ✅ Utiliser des outils de validation (xmllint, VS Code)

---

## 👤 Auteur

**Belalia Mohamed Oussama**  
📧 Email : mohamedoussama.belalia@univ-tiaret.dz  
🔗 GitHub : [github.com/bmo1177](https://github.com/1177)

---

## 📄 Licence

Ce projet est à usage éducatif dans le cadre d'un TP universitaire.

---

**Date de réalisation** : Janvier 2026  
**Cours** : Formalisme XML - Mini Projet
