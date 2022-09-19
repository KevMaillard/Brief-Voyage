## Data Dictionnary

|NOM             |TYPE                           |DESIGNATION                  |
|----------------|-------------------------------|-----------------------------|
| _**CLIENT**_                  |
|ID_Client       |Alphanumérique                 |Identifiant du client                 |
|Nom             |Alphanumérique                 |Nom du client                |
|Prénom          |Alphanumérique                 |Prénom du client             |
|Date de naissance             |Date                           |Date de naissance du client  |
|Email           |Alphanumérique                 |Adresse mail du client       |
|Numéro de téléphone       |Alphanumérique                 |Numéro de téléphone du client|
|Id_Passager      |Alphanumérique                 |Identifiant du passager|
|----------------|-------------------------------|-----------------------------|
|_**PASSAGER**_|
|ID_Passager      |Alphanumérique                 |Identifiant du passager                 |
|Nom             |Alphanumérique                 |Nom du passager                |
|Prénom          |Alphanumérique                 |Prénom du passager             |
|Id_Vol             |Alphanumérique                           |Identifiant du vol  |
|Numéro de passeport           |Alphanumérique                 |Numéro de passeport du passager       |
|Id_Client    |Alphanumérique                 |Identifiant du client ayant réservé le vol|
|----------------|-------------------------------|-----------------------------|
| _**VOL**_                  |
|ID_vol          |Alphanumérique|ID du vol|
|Compagnie          |Alphanumérique|ID de la compagnie assurant le vol|
|Date de départ          |Alphanumérique|Date et heure de départ du vol|
|Aéroport de départ          |Alphanumérique|ID de l'aéroport de départ du vol|
|Aéroport d'arrivée          |Alphanumérique|ID de l'aéroport d'arrivée du vol|
|Ouvrir_vol          |Boolean|Ouverture de la réservation par la compagnie|
|Fermer_vol          |Boolean|Fermeture de la réservation par la compagnie|
|Escale          |Alphanumérique|ID de l'aéroport de l'escale|
|----------------|-------------------------------|-----------------------------|
| _**AEROPORT**_
|ID Aéroport          |Alphanumérique|ID de l'aéroport|
|Villes desservies          |Alphanumérique|Villes desservies par l'aéroport|
|Vols au départ          |Alphanumérique|ID des vols au départ de l'aéroport|
|Vols à l'arrivée          |Alphanumérique|ID des vols à l'arrivée de l'aéroport|
|----------------|-------------------------------|-----------------------------|
| _**ESCALE**_
|ID_Escale         |Alphanumérique|ID de l'aéroport de l'escale du vol|
|Date d'arrivée        |Alphanumérique|Date et heure d'arrivée du vol|
|Date de départ       |Alphanumérique|Date et heure de départ du vol|
