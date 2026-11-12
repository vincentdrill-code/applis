# FitResto : base des restaurants (OpenStreetMap)

`restaurants-osm.json` est la liste des restaurants des enseignes reconnues par l'appli FitResto
(fast-foods, boulangeries, chaînes de restaurants), utilisée par l'appli pour trouver les restaurants
proches **directement sur le téléphone**, sans envoyer la position.

- **Source** : © les contributeurs d'OpenStreetMap, <https://www.openstreetmap.org/copyright>
  (extraits Geofabrik des pays d'Europe concernés).
- **Licence** : cette base dérivée est mise à disposition sous la
  [Open Database License (ODbL) 1.0](https://opendatacommons.org/licenses/odbl/1-0/).
  Tu peux la copier, la modifier et la réutiliser, à condition de citer OpenStreetMap et de
  partager tes propres versions dérivées sous la même licence.
- **Date des données** : 11 novembre 2026 · 35 769 restaurants de 64 enseignes, 21 pays d’Europe.

## Contenu

Pour chaque restaurant : l'enseigne, la position (latitude et longitude, en entiers ×100 000) et,
si elle est renseignée dans OpenStreetMap, la ville. Les points sont rangés par cases de 0,1 degré :

```
{ "date": "AAAA-MM-JJ", "pas": 10, "enseignes": ["mcdonalds", ...], "villes": ["Paris", ...],
  "cases": { "488:23": [enseigne, lat×1e5, lon×1e5, ville, ...] } }
```

`enseigne` et `ville` sont des positions dans les listes `enseignes` et `villes` (-1 : ville inconnue).
La case `"488:23"` regroupe les points dont la latitude commence par 48,8 et la longitude par 2,3.

## Construction

Les lieux `amenity=fast_food|restaurant|cafe|pub` et `shop=bakery` sont filtrés avec osmium, puis
reconnus par les étiquettes `brand:wikidata`, `brand` ou `name`. Les noms trop courants (« Paul »,
« Max », « Leon »…) ne comptent que si l'étiquette `brand` ou `brand:wikidata` désigne l'enseigne.
Le script de construction se trouve dans le code de l'appli (`scripts/restaurants-osm.py`).
