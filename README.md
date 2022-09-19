## Data Dictionnary

|NOM             |TYPE                           |DESIGNATION                  |
|----------------|-------------------------------|-----------------------------|
| _**CLIENT**_                  |
|ID_Client       |Alphanumérique                 |ID du client                 |
|Nom             |Alphanumérique                 |Nom du client                |
|Prénom          |Alphanumérique                 |Prénom du client             |
|DDN             |Date                           |Date de naissance du client  |
|Email           |Alphanumérique                 |Adresse mail du client       |
|Téléphone       |Alphanumérique                 |Numéro de téléphone du client|
|----------------|-------------------------------|-----------------------------|
| _**COMPAGNIE**_                  |
|ID_Compagnie          |Alphanumérique|ID de la compagnie aérienne|
|Nom          |Alphanumérique|Nom de la compagnie aérienne|
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


## Régles de gestion

### Client

* Un client doit renseigner son nom, son prénom, sa date de naissance, son email et son numéro de téléphone.

* Un client peut réserver plusieurs billets. Il peut également réserver pour une tier personne.

* Lors d'une réservation, un client se voit attribué un passager.

### Passager

* Un passager a un nom, un prénom, un numéro de passeport.

* Le passager peut être un client. 

* On attribut, lors de la réservation, l'identifiant unique du client qui a réservé.

* Le passager lui voit attribué un numéro de vol lors de la réservation.

### Compagnie

* La compagnie possède un nom et un identifiant.

* Les vols depende des compagnies, chaque compagnie possède ces propres vols.

### Vol

* Un vol existe seulement lorsque la compagnie l'assure.

* Un vol doit avoir une date et heure de départ, une date et heure d'arrivée, un aéroport de départ et d'arrivée, un nom de compagnie, une destination et les escales s'il y en a.

* Si le client reçoit le billet, cela veut dire que le vol a été créé par la compagnie et qu'il est disponible (ouvrirVol = true). La compagnie peut toujours fermer le vol (fermerVol = true) dans ce cas le vol n'est plus disponible et le programme avertira automatiquement le client que son vol (identifié grâce à son ID) est annulé. 

* Le vol dépend de la compagnie, il est créé par la compagnie et peut être aussi supprimé. 

### Aéroport 

* Un aéroport peut avoir plusieurs vols. 

* Un aéroport dessert plusieurs villes.

### Escale 

* Une escale est un héritage de l'aéroport au vu des escales qui peuvent pas être des destinations finales.

* L'escale possède une heure d'arrivée, une heure de départ et un identifiant.

---

# Requête SQL

```sql
CREATE TABLE Client(
   Id_Client COUNTER,
   Id_Passager VARCHAR(50),
   Nom VARCHAR(50),
   Prénom VARCHAR(50),
   Date_de_naissance DATE,
   Email VARCHAR(50),
   Numéro_de_téléphone VARCHAR(50),
   PRIMARY KEY(Id_Client, Id_Passager)
);

CREATE TABLE Vol(
   Id_Vol COUNTER,
   Compagnie VARCHAR(50),
   Aéroport_de_départ VARCHAR(50),
   Aéroport_d_arrivée VARCHAR(50),
   Escale VARCHAR(50),
   Date_de_départ DATETIME,
   Date_d_arrivée DATETIME,
   Destination VARCHAR(50),
   Ouvrir_Vol LOGICAL,
   Fermer_Vol LOGICAL,
   PRIMARY KEY(Id_Vol, Compagnie, Aéroport_de_départ, Aéroport_d_arrivée, Escale)
);

CREATE TABLE Compagnie(
   Id_Compagnie COUNTER,
   Nom VARCHAR(50),
   PRIMARY KEY(Id_Compagnie)
);

CREATE TABLE Aéroport(
   Id_Aéroport COUNTER,
   Vols_au_départ VARCHAR(50),
   Vols_à_l_arrivée VARCHAR(50),
   Villes_desservies VARCHAR(50),
   PRIMARY KEY(Id_Aéroport, Vols_au_départ, Vols_à_l_arrivée)
);

CREATE TABLE Passager(
   Id_Passager COUNTER,
   Id_Vol COUNTER,
   Id_Client VARCHAR(50),
   Nom VARCHAR(50),
   Prenom VARCHAR(50),
   Numéro_de_passeport VARCHAR(50),
   PRIMARY KEY(Id_Passager, Id_Vol, Id_Client)
);

CREATE TABLE Escale(
   Id_Escale COUNTER,
   Heure_d_arrivé TIME,
   Heure_de_départ TIME,
   Id_Aéroport INT NOT NULL,
   Vols_au_départ VARCHAR(50) NOT NULL,
   Vols_à_l_arrivée VARCHAR(50) NOT NULL,
   PRIMARY KEY(Id_Escale),
   UNIQUE(Id_Aéroport),
   UNIQUE(Vols_au_départ),
   UNIQUE(Vols_à_l_arrivée),
   FOREIGN KEY(Id_Aéroport, Vols_au_départ, Vols_à_l_arrivée) REFERENCES Aéroport(Id_Aéroport, Vols_au_départ, Vols_à_l_arrivée)
);

CREATE TABLE Reserver(
   Id_Client INT,
   Id_Passager VARCHAR(50),
   Id_Vol INT,
   Compagnie VARCHAR(50),
   Aéroport_de_départ VARCHAR(50),
   Aéroport_d_arrivée VARCHAR(50),
   Escale VARCHAR(50),
   Id_Passager_1 INT,
   Id_Vol_1 INT,
   Id_Client_1 VARCHAR(50),
   PRIMARY KEY(Id_Client, Id_Passager, Id_Vol, Compagnie, Aéroport_de_départ, Aéroport_d_arrivée, Escale, Id_Passager_1, Id_Vol_1, Id_Client_1),
   FOREIGN KEY(Id_Client, Id_Passager) REFERENCES Client(Id_Client, Id_Passager),
   FOREIGN KEY(Id_Vol, Compagnie, Aéroport_de_départ, Aéroport_d_arrivée, Escale) REFERENCES Vol(Id_Vol, Compagnie, Aéroport_de_départ, Aéroport_d_arrivée, Escale),
   FOREIGN KEY(Id_Passager_1, Id_Vol_1, Id_Client_1) REFERENCES Passager(Id_Passager, Id_Vol, Id_Client)
);

CREATE TABLE Assurer(
   Id_Vol INT,
   Compagnie VARCHAR(50),
   Aéroport_de_départ VARCHAR(50),
   Aéroport_d_arrivée VARCHAR(50),
   Escale VARCHAR(50),
   Id_Compagnie INT,
   PRIMARY KEY(Id_Vol, Compagnie, Aéroport_de_départ, Aéroport_d_arrivée, Escale, Id_Compagnie),
   FOREIGN KEY(Id_Vol, Compagnie, Aéroport_de_départ, Aéroport_d_arrivée, Escale) REFERENCES Vol(Id_Vol, Compagnie, Aéroport_de_départ, Aéroport_d_arrivée, Escale),
   FOREIGN KEY(Id_Compagnie) REFERENCES Compagnie(Id_Compagnie)
);

CREATE TABLE Atterrir(
   Id_Vol INT,
   Compagnie VARCHAR(50),
   Aéroport_de_départ VARCHAR(50),
   Aéroport_d_arrivée VARCHAR(50),
   Escale VARCHAR(50),
   Id_Aéroport INT,
   Vols_au_départ VARCHAR(50),
   Vols_à_l_arrivée VARCHAR(50),
   PRIMARY KEY(Id_Vol, Compagnie, Aéroport_de_départ, Aéroport_d_arrivée, Escale, Id_Aéroport, Vols_au_départ, Vols_à_l_arrivée),
   FOREIGN KEY(Id_Vol, Compagnie, Aéroport_de_départ, Aéroport_d_arrivée, Escale) REFERENCES Vol(Id_Vol, Compagnie, Aéroport_de_départ, Aéroport_d_arrivée, Escale),
   FOREIGN KEY(Id_Aéroport, Vols_au_départ, Vols_à_l_arrivée) REFERENCES Aéroport(Id_Aéroport, Vols_au_départ, Vols_à_l_arrivée)
);

CREATE TABLE Decollage(
   Id_Vol INT,
   Compagnie VARCHAR(50),
   Aéroport_de_départ VARCHAR(50),
   Aéroport_d_arrivée VARCHAR(50),
   Escale VARCHAR(50),
   Id_Aéroport INT,
   Vols_au_départ VARCHAR(50),
   Vols_à_l_arrivée VARCHAR(50),
   PRIMARY KEY(Id_Vol, Compagnie, Aéroport_de_départ, Aéroport_d_arrivée, Escale, Id_Aéroport, Vols_au_départ, Vols_à_l_arrivée),
   FOREIGN KEY(Id_Vol, Compagnie, Aéroport_de_départ, Aéroport_d_arrivée, Escale) REFERENCES Vol(Id_Vol, Compagnie, Aéroport_de_départ, Aéroport_d_arrivée, Escale),
   FOREIGN KEY(Id_Aéroport, Vols_au_départ, Vols_à_l_arrivée) REFERENCES Aéroport(Id_Aéroport, Vols_au_départ, Vols_à_l_arrivée)
);
```
---

# MLD Textuel

```
Client = (Id_Client COUNTER, Id_Passager VARCHAR(50), Nom VARCHAR(50), Prénom VARCHAR(50), Date_de_naissance DATE, Email VARCHAR(50), Numéro_de_téléphone VARCHAR(50));
Vol = (Id_Vol COUNTER, Compagnie VARCHAR(50), Aéroport_de_départ VARCHAR(50), Aéroport_d_arrivée VARCHAR(50), Escale VARCHAR(50), Date_de_départ DATETIME, Date_d_arrivée DATETIME, Destination VARCHAR(50), Ouvrir_Vol LOGICAL, Fermer_Vol LOGICAL);
Compagnie = (Id_Compagnie COUNTER, Nom VARCHAR(50));
Aéroport = (Id_Aéroport COUNTER, Vols_au_départ VARCHAR(50), Vols_à_l_arrivée VARCHAR(50), Villes_desservies VARCHAR(50));
Passager = (Id_Passager COUNTER, Id_Vol COUNTER, Id_Client VARCHAR(50), Nom VARCHAR(50), Prenom VARCHAR(50), Numéro_de_passeport VARCHAR(50));
Escale = (Id_Escale COUNTER, Heure_d_arrivé TIME, Heure_de_départ TIME, #(Id_Aéroport, Vols_au_départ, Vols_à_l_arrivée));
Reserver = (#(Id_Client, Id_Passager), #(Id_Vol, Compagnie, Aéroport_de_départ, Aéroport_d_arrivée, Escale), #(Id_Passager_1, Id_Vol_1, Id_Client_1));
Assurer = (#(Id_Vol, Compagnie, Aéroport_de_départ, Aéroport_d_arrivée, Escale), #Id_Compagnie);
Atterrir = (#(Id_Vol, Compagnie, Aéroport_de_départ, Aéroport_d_arrivée, Escale), #(Id_Aéroport, Vols_au_départ, Vols_à_l_arrivée));
Decollage = (#(Id_Vol, Compagnie, Aéroport_de_départ, Aéroport_d_arrivée, Escale), #(Id_Aéroport, Vols_au_départ, Vols_à_l_arrivée));

```
