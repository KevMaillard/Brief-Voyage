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