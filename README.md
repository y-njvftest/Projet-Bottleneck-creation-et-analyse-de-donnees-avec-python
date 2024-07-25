

# Projet Bottleneck (nettoyage de données et analyse avec python)

<img width="407" alt="Screenshot 2024-07-05 at 17 25 27" src="https://github.com/y-njvftest/Projet-Bottleneck/assets/166219135/57cf0013-d3f9-4594-add9-975bdc68d4db">


Le projet Bottleneck est un projet fictif de formation avec une mise en situation portant sur le nettoyage d'une base de données et son analyse avec python.

La situation est la suivante:
La société Bottleneck nous solicite afin de pouvoir relier définitivement la base de données liée à leur site internet de ventes de vin, et leurs tenus de stocks en physique. Nous effecturons ensuite des analyses une fois les base de données fusionnées.

Plusieurs étapes ont été mis en oeuvre afin d'atteindre le but recherché notamment :

Le chargement et l'exploration des fichiers :

```Python
#Afficher les dimensions du dataset
print("Le tableau comporte {} observation(s) ou article(s)".format(df_erp.shape[0]))
print("Le tableau comporte {} colonne(s)".format(df_erp.shape[1]))
```

<img width="1383" alt="Screenshot 2024-07-16 at 02 53 09" src="https://github.com/user-attachments/assets/65f6d22d-43b5-4c8e-abf9-96796f24c6e2">



La jonction et la création d'une base de données :

<img width="766" alt="Screenshot 2024-07-16 at 02 58 21" src="https://github.com/user-attachments/assets/974eccce-4292-42e3-a450-286f75a040a7">

Une exploration des "outliers" et comparaison avec la concurrrence:

<img width="1278" alt="SCR-20240723-cetq" src="https://github.com/user-attachments/assets/5c2951ba-6373-4a96-8c59-6fd118984024">


Des analyses univariées et bivariées des produits...

<img width="1241" alt="SCR-20240723-ccdt" src="https://github.com/user-attachments/assets/d1c30f6d-f2d7-4a68-843d-2d844cb8290a">

...Dont on peut tirer des informations cruciales sur la proportion de bouteilles réellement vendues!

```Python
#Créer une colonne calculant la part du CA de la ligne dans le dataset
df_merge['part_du_ca']=df_merge['ca_par_article']/df_merge['ca_par_article'].sum()
#Grâce au deux colonnes créées précedemment, calculer le nombre d'articles représentant 80% du CA
#Afficher la proportion que représentent ce groupe d'articles dans le catalogue entier du site web
part_du_CA_triées=df_merge['part_du_ca'].sort_values(ascending=True)
nombres_individus=df_merge['id_web'].nunique()
nombres_individus_1=int(nombres_individus/5)
premier_quintile_CA=part_du_CA_triées[:nombres_individus_1].sum()
second_quintile_CA=part_du_CA_triées[:(nombres_individus_1*2)].sum()
troisième_quintile_CA=part_du_CA_triées[:(nombres_individus_1*3)].sum()
quatrième_quintile_CA=part_du_CA_triées[:(nombres_individus_1*4)].sum()
cinquième_quintile_CA=part_du_CA_triées[:nombres_individus].sum()
print(quatrième_quintile_CA)
```

<img width="592" alt="Screenshot 2024-07-16 at 02 53 47" src="https://github.com/user-attachments/assets/d15b183f-0cf0-46d6-9242-3f6bfdacde92">
