
  PROIECT BAZE DE DATE

Baza de date a unei facultati


 							 Cuprins


1.	Descrierea temei alese	3
2.	Schema conceptuala	4
3.	Construirea bazei de date	5
Stergerea tabelelor:	5
Construirea tabelei GRUPA:	5
Construirea tabelei STUDENTI:	5
Crearea tabelei Cursuri:	6
Crearea tabelei ORAR:	7
Crearea tabelei TAXE:	7
Adaugare constrangeri si coloane:	8
4.	Operaţii de actualizare a datelor	9
Inserare valori in tabelele GRUPA si STUDENTI	9
Actualizare valori in tabelul STUDENTI	10
Stergere valori din tabelul STUDENTI	11
Completare tabele	12
Combinarea tabelei studenti	16
5.	Exemple de interogări	16
Exemplu >, <, >=, <=, !=, IS NULL, LIKE, IN, BETWEEN:	16
Joncţiuni (outer, inner):	17
Functii de grup:	18
Utilizarea funcțiilor la nivel de rând	19
Utilizarea operatorilor UNION, MINUS, INTERSECT	23
Subcereri simple şi corelate	24
Construirea şi utilizarea altor obiecte ale bazei de date	25
Cereri ierarhice	27
Functiile MONTHS_BETWEEN, ADD_MONTHS, NEXT_DAY, LAST_DAY	28
Concatenare	29
Operatorii ANY si ALL	29

1.	Descrierea temei alese 


O bază de date este un instrument pentru colectarea și organizarea informațiilor. Bazele de date pot stoca informații despre persoane, produse, comenzi sau orice altceva.
Datele din cele mai obișnuite tipuri de baze de date sunt distribuite de regulă pe linii și coloane, în diferite tabele, pentru eficientizarea procesării și interogării datelor. Datele pot fi accesate, gestionate, modificate, actualizate, controlate și organizate cu ușurință. Majoritatea bazelor de date utilizează un limbaj structurat de interogare (SQL) pentru scrierea și interogarea datelor.
In acest proiect am dorit sa evidentiez importanta unei baze de date intr-o facultate. Consider ca prin baza de date creata este mult mai usor de tinut evidenta notelor, informatiilor si restantelor respectiv taxelor care trebuie incasate de la studentii facultatii, aceasta putand asigura o organizare si functionare eficienta a facultatii.
Folosind interogari simple SQL, putem afla intr-un mod facil situatia scolara a unui student aceasta incluzand note, restante, etc.










2.	Schema conceptuala




























3.	Construirea bazei de date


Stergerea tabelelor:

DROP TABLE GRUPA CASCADE CONSTRAINTS;
DROP TABLE STUDENTI CASCADE CONSTRAINTS;
DROP TABLE CURSURI CASCADE CONSTRAINTS;
DROP TABLE ORAR CASCADE CONSTRAINTS;
DROP TABLE TAXE CASCADE CONSTRAINTS;

Construirea tabelei GRUPA:

create table GRUPA
(
  id_grupa  NUMBER constraint pk_g_grupa primary key,
  facultate VARCHAR2(120),
  specialitate VARCHAR2(120)
);
 

Construirea tabelei STUDENTI:

create table STUDENTI
(
  id_student VARCHAR2(25) constraint pk_s_studenti primary key,
  nume VARCHAR2(25),
  prenume VARCHAR(20),
  an_nastere NUMBER(4),
  cnp NUMBER(13),
  id_grupa NUMBER,
  constraint fk_studenti foreign key (id_grupa) references GRUPA (id_grupa)
);
 

Crearea tabelei Cursuri:

create table CURSURI
(
  id_curs VARCHAR2(3) constraint pk_c_cursuri primary key, 
  nume_curs VARCHAR2(38),
  profesor  VARCHAR2(35),
 id_grupa NUMBER,
 data_incepere DATE,
 salariul number,
 comision number,
 constraint fk_cursuri foreign key (id_grupa) references GRUPA(id_grupa)
);
 	        
Crearea tabelei ORAR:

	create table ORAR
(
  id_zi VARCHAR2(9) constraint pk_zi_orar primary key,
  	interval_orar VARCHAR2(8),
 	 id_curs VARCHAR2(3),
  constraint fk_orar foreign key (id_curs) references CURSURI(id_curs)
);

 
Crearea tabelei TAXE:

create table TAXE
(
    denumire_taxa VARCHAR(120) constraint pk_t_taxa primary key,
    valoare_taxa number,
    id_student VARCHAR2(25),
    constraint fk_taxe foreign key (id_student) references STUDENTI(id_student)
);

 


Adaugare constrangeri si coloane: 

alter table GRUPA
  add constraint FACULTATE_NN
  check ("FACULTATE" IS NOT NULL)
  add sef_grupa VARCHAR(120);
 

alter table STUDENTI
  add constraint ID_STUDENT_NN
  check ("ID_STUDENT" IS NOT NULL)
  add constraint PRENUME_NN
  check ("PRENUME" IS NOT NULL)
  add constraint NUME_NN
  check ("NUME" IS NOT NULL);
 
alter table CURSURI
  drop column nr_studenti_inscrisi;

 

4.	Operaţii de actualizare a datelor

Inserare valori in tabelele GRUPA si STUDENTI

insert into GRUPA(id_grupa,facultate, specialitate, sef_grupa)
values(1043,'ASE','CSIE', 'Popescu Ionel');
insert into GRUPA(id_grupa,facultate, specialitate, sef_grupa)
values(1047,'ASE','CSIE', 'Antonio Alexandru');
insert into GRUPA(id_grupa,facultate, specialitate, sef_grupa)
values(1046,'ASE','CSIE','Stanciu Violeta');
 

INSERT INTO STUDENTI (id_student, nume, prenume, an_nastere, cnp, id_grupa) VALUES ('2131', 'Popescu','Ionel',2002,6582568267921, 1043);
SELECT * FROM STUDENTI;

INSERT INTO STUDENTI (id_student, nume, prenume, an_nastere, cnp, id_grupa) VALUES ('345', 'Antonio','Alexandru',2003,582926267914, 1047);
SELECT * FROM STUDENTI;

INSERT INTO STUDENTI (id_student, nume, prenume, an_nastere, cnp, id_grupa) VALUES ('456', 'Stanciu','Violeta',2001,482967867412, 1046);
SELECT * FROM STUDENTI;

INSERT INTO STUDENTI  (id_student, nume, prenume, an_nastere, cnp, id_grupa)
VALUES ('&id_student','&nume','&prenume', '&an_nastere','&cnp', '&id_grupa');

 

Actualizare valori in tabelul STUDENTI

UPDATE STUDENTI
SET id_student=id_student+100
WHERE an_nastere<2002;
SELECT * FROM Studenti;
 	 
UPDATE STUDENTI
SET id_grupa=(SELECT id_grupa FROM STUDENTI WHERE id_student=345)
WHERE an_nastere=2002;
SELECT * FROM Studenti;
 

Stergere valori din tabelul STUDENTI

DELETE FROM Studenti
WHERE id_grupa IN (1047);
 

DELETE FROM STUDENTI;
SELECT * FROM STUDENTI;
	 
insert into GRUPA(id_grupa,facultate, specialitate)
values(1023,'ASE','CSIE');
insert into GRUPA(id_grupa,facultate, specialitate)
values(1028,'ASE','CSIE');
insert into GRUPA(id_grupa,facultate, specialitate)
values(1072,'ASE','CSIE');
insert into GRUPA(id_grupa,facultate, specialitate)
values(1048,'ASE','CSIE');
insert into GRUPA(id_grupa,facultate, specialitate)
values(1077,'ASE','CSIE');
commit;

Completare tabele 

GRUPA:
	insert into GRUPA(id_grupa,facultate, specialitate, sef_grupa)
values(1023,'ASE','CSIE','Lupu Bianca');
insert into GRUPA(id_grupa,facultate, specialitate, sef_grupa)
values(1028,'ASE','CSIE','Teaca Lucian');
insert into GRUPA(id_grupa,facultate, specialitate, sef_grupa)
values(1072,'ASE','CSIE','Valentin Gabriel');
insert into GRUPA(id_grupa,facultate, specialitate, sef_grupa)
values(1048,'ASE','CSIE','Militaru Marius');
insert into GRUPA(id_grupa,facultate, specialitate, sef_grupa)
values(1077,'ASE','CSIE','Anghel Nicoleta');
commit;
 
CURSURI:
insert into CURSURI(id_curs,nume_curs, profesor,id_grupa,data_incepere,salariul,comision)
values('POO','Programare Orientata Obiect', 'Alin Zamfiroiu',1043,to_date('2021-02-25', 'yyyy-mm-dd'),24000,null);
insert into CURSURI(id_curs,nume_curs, profesor,id_grupa,data_incepere,salariul,comision)
values('BDD','Baze de date', 'Stefan Preda',1047,to_date('2021-12-23', 'yyyy-mm-dd'), 17000,null);
insert into CURSURI(id_curs,nume_curs, profesor,id_grupa,data_incepere,salariul,comision)
values('PSM','Probabilitati si statistica matematica', 'Liana Manu Iosifescu',1048,to_date('2021-02-25', 'yyyy-mm-dd'), 17000,null);
insert into CURSURI(id_curs,nume_curs, profesor,id_grupa,data_incepere,salariul,comision)
values('SM','Statistica macroeconomica', ' Simona Andreea Apostu',1043,to_date('2022-04-15', 'yyyy-mm-dd'), 9000,null);
insert into CURSURI(id_curs,nume_curs, profesor,id_grupa,data_incepere,salariul,comision)
values('FIN','Finante', ' Stefan Cristian Gherghina',1047,to_date('2021-11-12', 'yyyy-mm-dd'), 11000,null);
insert into CURSURI(id_curs,nume_curs, profesor,id_grupa,data_incepere,salariul,comision)
values('MAN','Managemant', 'Ovidiu Andrei Cristian Buzoianu',1043,to_date('2021-10-19', 'yyyy-mm-dd'), 14000,null);
insert into CURSURI(id_curs,nume_curs, profesor,id_grupa,data_incepere,salariul,comision)
values('EFS','Educatie fizica si sport', 'Dumitru Vasilescu',1047,to_date('2022-06-12', 'yyyy-mm-dd'), 13000,null);
insert into CURSURI(id_curs,nume_curs, profesor,id_grupa,data_incepere,salariul,comision)
values('MC','Microeconomie cantitativa', 'ALDEA ANA-MARIA',1048,to_date('2022-06-12', 'yyyy-mm-dd'), 13000,null);
commit;  

STUDENTI:
insert into STUDENTI (id_student, nume, prenume, an_nastere, cnp, id_grupa)
values ('2131', 'Popescu','Ionel',2001,6582568267921, 1043);
insert into STUDENTI (id_student, nume, prenume, an_nastere, cnp, id_grupa)
values ('345', 'Antonio','Alexandru',2001,5829262679214, 1047);
insert into STUDENTI (id_student, nume, prenume, an_nastere, cnp, id_grupa)
values ('2341', 'Cazacu','Dumitru',2002,6582352967921, 1023);
insert into STUDENTI (id_student, nume, prenume, an_nastere, cnp, id_grupa)
values ('1723', 'Costea','Sorin',2002,5582552926653, 1028);
insert into STUDENTI (id_student, nume, prenume, an_nastere, cnp, id_grupa)
values ('8383', 'Mihai','Catalin',2001,5082352926741, 1072);
insert into STUDENTI (id_student, nume, prenume, an_nastere, cnp, id_grupa)
values ('9383', 'Nicolae','George',2003,5582352926875, 1043);
insert into STUDENTI (id_student, nume, prenume, an_nastere, cnp, id_grupa)
values ('7253', 'Popa','Dorin',2000,5782352346921, 1048);
commit;
 

ORAR:
insert into ORAR(id_zi,interval_orar,id_curs)
values('Luni','07.30','POO');
insert into ORAR(id_zi,interval_orar,id_curs)
values('Marti','09.30','BDD');
insert into ORAR(id_zi,interval_orar,id_curs)
values('Miercuri','11.30','PSM');
insert into ORAR(id_zi,interval_orar,id_curs)
values('Joi','13.30','SM');
insert into ORAR(id_zi,interval_orar,id_curs)
values('Sambata','10.30','MAN');
insert into ORAR(id_zi,interval_orar,id_curs)
values('Sambata','07.30','EFS');
commit;

 
TAXE: 
insert into TAXE(denumire_taxa, valoare_taxa, id_student)
values('Taxa Scolarizare IF', 2000, 2135);
insert into TAXE(denumire_taxa, valoare_taxa, id_student)
values('Restanta Aaliza', 75, 2135);
insert into TAXE(denumire_taxa, valoare_taxa, id_student)
values('Restanta BDD', 2000, 2345);
insert into TAXE(denumire_taxa, valoare_taxa, id_student)
values('Restabta POO', 75, 349);
insert into TAXE(denumire_taxa, valoare_taxa, id_student)
values('Restanta SM', 7, 1727);
insert into TAXE(denumire_taxa, valoare_taxa, id_student)
values('Restanta MAN', 2000, 8387);

 
Combinarea tabelei studenti 

MERGE INTO STUDENTI USING GRUPA
ON (STUDENTI.id_GRUPA = GRUPA.id_grupa)
WHEN MATCHED THEN 
UPDATE SET STUDENTI.id_student=STUDENTI.id_student+2;
 
5.	Exemple de interogări


Exemplu >, <, >=, <=, !=, IS NULL, LIKE, IN, BETWEEN:

Se afiseaza tabela CURSURI cu salariul cuprins intre 13000 si 24000 cu exceptia unde salariul este cuprins intre 17000 si 11000.
	
SELECT * FROM CURSURI WHERE salariul BETWEEN 13000 AND 24000
MINUS
SELECT * FROM CURSURI WHERE salariul IN (17000, 11000);
 
Se afiseaza tabela STUDENTI unde numele incepe cu litra C, anul de nastere este diferit de 2001 si Id_grupa nu este null, ordonandu-se descrescator dupa id_student.

SELECT * FROM STUDENTI WHERE nume LIKE 'C%' AND an_nastere != 2001 AND ID_GRUPA IS NOT NULL
ORDER BY id_student DESC;	 

Joncţiuni (outer, inner):

Se realizeaza o jonctiune externa intre tabelele GRUPA si STUDENTI.
SELECT STUDENTI.id_STUDENT, STUDENTI.prenume, GRUPA.id_grupa, GRUPA.facultate
FROM STUDENTI, GRUPA
WHERE STUDENTI.id_grupa = GRUPA.id_grupa (+);
	 

Se realizeaza o jonctiune interna de egalitate in tabela GRUPA.

SELECT STUDENTI.*, GRUPA.* 
FROM STUDENTI, GRUPA
WHERE STUDENTI.id_grupa=GRUPA.id_grupa;
	  
	

Functii de grup:

Se calculeaza salariile platite pentru sustinerea cursurilor grupate dupa data de incepere.

SELECT SUM(SALARIUL) as Salarii, to_char(data_incepere, 'yyyy-mm-dd') as Data_incepere
FROM CURSURI
GROUP BY data_incepere;
 
Se afiseaza salariul mediu, maxim, minim si suma salariilor pentru cursurile predate grupei 1043.

SELECT AVG(salariul), MAX(salariul), MIN(salariul), SUM(salariul)
FROM CURSURI
WHERE id_grupa='1043';
 



Se afiseaza salariul total al cursurilor pe fiecare grupa.

SELECT id_grupa, SUM(salariul)
FROM CURSURI
GROUP BY id_grupa

 


Salariul total pe fiecare grupa, fara a lua in calcul cursul de Microeconomie Cantitativa, excluzand grupele cu suma salariilor sub 30000 lei cu ordonare dupa salariu.

SELECT id_grupa, SUM(salariul)
FROM CURSURI
WHERE nume_curs!='Microeconomie cantitativa'
GROUP BY id_grupa
HAVING SUM(salariul) > 30000
ORDER BY SUM(salariul)
 
Utilizarea funcțiilor la nivel de rând

Se extrage anul si luna din data de incepere a cursurilor.

SELECT EXTRACT ( year FROM data_incepere) year, EXTRACT ( month FROM data_incepere) month, nume_curs
FROM CURSURI;
 
Se afiseaza valoare unui string pornind de la pozitia 1 a coloanei nume din tabela STUDENTI si terminand la pozitia 8.

SELECT SUBSTR(nume, 1, 8) AS Nume
FROM STUDENTI;
 

Se afiseaza perioada de timp corespunzătoare (în săptămâni) între data începerii primului curs şi data curentă:

SELECT nume_curs, ROUND( (SYSDATE-data_incepere)/7 ) saptamani
FROM CURSURI;
 
Actualizarea tabelei STUDENTI folosind decode.

UPDATE STUDENTI
SET an_nastere = DECODE(id_grupa, '1043', '2004', an_nastere);
SELECT nume, prenume, an_nastere, id_grupa
FROM STUDENTI;

 
Adaugarea comisionului cu functia case.

SELECT profesor, id_curs, 
CASE WHEN UPPER(id_curs) = 'MAN' THEN 0.3
WHEN UPPER(id_curs) =  'BDD' THEN 0.2
WHEN UPPER(id_curs) = 'POO' THEN 0.1
ELSE 0 END comision
FROM CURSURI;

 
Salariul anual + comision folosinf NVL si NVL2.

SELECT profesor, salariul*12 + salariul*12*NVL(comision,0) venit_anual
FROM CURSURI;
 

SELECT profesor, NVL2(comision, 1, 0)
FROM CURSURI;
 

Utilizarea operatorilor UNION, MINUS, INTERSECT

Se calculeaza distinct comisionul fiecarui profesor folosind operatorul union( 1 curs-10% din salariu, 2 cursuri-20% din salariu, >=3 cursuri-30% din salariu ).

SELECT PROFESOR, COUNT(id_curs) numar_cursuri,
0.1* sum(salariul) valoare_comision
FROM CURSURI
GROUP BY profesor, salariul
HAVING COUNT(id_curs)=1
UNION 
SELECT profesor, COUNT(id_curs) numar_cursuri, 
0.2* SUM(salariul) valoare_comision
FROM CURSURI
GROUP BY profesor, salariul
HAVING COUNT(id_curs)=2
UNION 
SELECT profesor, COUNT(id_curs) numar_cursuri, 
0.3* SUM(salariul) valoare_comision
FROM CURSURI
GROUP BY profesor, salariul
HAVING COUNT(id_curs)>=3;
 

Se afiseaza folosindu-se operatorul intersect studentii care au cel putin o restanta, iar taxele au o valoare diferita de 7, 75.

SELECT s.nume, s.prenume, SUM(t.valoare_taxa) total_taxe, COUNT(t.id_student) numar_taxe
FROM studenti s, taxe t
WHERE t.id_student=s.id_student
GROUP BY s.nume, s.prenume
HAVING COUNT(t.id_student)>0;
	 
INTERSECT
SELECT s.nume, s.prenume, SUM(t.valoare_taxa) total_taxe, COUNT(t.id_student) numar_taxe
FROM studenti s, taxe t
WHERE t.id_student=s.id_student
GROUP BY s.nume, s.prenume
HAVING SUM(t.valoare_taxa) NOT IN (7,75);
	 

Subcereri simple şi corelate

Se afiseaza numele si salariile profesorilor care predau la aceeasi grupa ca si Ovidiu Andrei Cristian Buzoianu.

SELECT profesor, salariul, id_grupa
FROM CURSURI
WHERE id_grupa=(SELECT id_grupa FROM CURSURI  WHERE profesor='Ovidiu Andrei Cristian Buzoianu');

 

Se gasesc profesorii care au un salariu mai mare decat salariul mediu.

SELECT profesor, salariul, nume_curs
FROM CURSURI 
WHERE salariul > (SELECT avg(salariul) FROM CURSURI )
GROUP BY profesor, nume_curs, salariul;
	 
Construirea şi utilizarea altor obiecte ale bazei de date

Sa realizeaza o tabela virtuala cu toate cursurile predate grupei 1043. Actualizăm salariul.

CREATE OR REPLACE VIEW V_CURSURI
AS SELECT * FROM CURSURI
WHERE id_grupa=1043;
SELECT * FROM V_CURSURI;
UPDATE V_CURSURI
SET salariul = salariul + 1000;
 

Se realizeaza un tabel virtual cu toti elevii din tabela STUDENTI care apartin grupei 1043 si se creeaza un index pe coloana id_grupa.
SELECT * FROM STUDENTI WHERE (id_grupa) = 1043;
CREATE INDEX idx_id_grupa ON STUDENTI(UPPER(id_grupa));
 
DROP INDEX idx_id_grupa;

Se creaza o secventa prin care se asigura unicitatea cheii primare a tabelei STUDENTI si se introduc noi randuri.

CREATE OR REPLACE VIEW total_studenti
AS SELECT id_student, nume, prenume, an_nastere, cnp, id_grupa FROM STUDENTI

CREATE SEQUENCE seq_id_student 
START WITH 500 INCREMENT BY 10
MAXVALUE 1000 NOCYCLE;

INSERT INTO total_studenti VALUES (seq_id_student.NEXTVAL, 'Caloian', 'Cosmin', 2001, '5013636373324', 1043);
SELECT seq_id_student.CURRVAL FROM STUENTI;
INSERT INTO total_studenti VALUES (seq_id_student.NEXTVAL, 'Gaiu', 'Narcis', 2002, '5018527373794', 1047);
SELECT seq_id_student.CURRVAL FROM STUENTI;
 

Creare, vizualizare si stergere sinonim pentru tabela Orar

CREATE SYNONYM o FOR ORAR;
SELECT * FROM USER_SYNONYMS;
DROP SYNONYM o;
 

Cereri ierarhice

 Se selecteaza studentii si gradul de subordonare numai pentru cei din grupele 1043,1047si 1023.

SELECT id_student, nume, an_nastere, level FROM  STUDENTI
WHERE id_grupa IN (1043, 1047, 1023)
CONNECT BY PRIOR id_student = an_nastere;
 

Se afiseaza studentii facultatii subordonati inregistrarii radacina specificand numarul de studenti mai mari si studentii mai mari decat ei, id-urile (se utilizeaza clauzele: SYS_CONNECT_BY_ PATH,  LEVEL-1):

SELECT id_student, nume,  
LEVEL-1 Numar_Superiori, SYS_CONNECT_BY_PATH(id_student, '/') ID_Superiori
FROM STUDENTI
START WITH ID_STUDENT= 9385
CONNECT BY PRIOR id_student = AN_NASTERE;
 

Functiile MONTHS_BETWEEN, ADD_MONTHS, NEXT_DAY, LAST_DAY

Se afişeaza id-ul cursurilor, data inceperii cursurilor, numărul de luni între data curentă şi data inceperii, următoarea zi de vineri după data inceperii, ultima zi din luna din care face parte data începerii, precum şi data corespunzătoare după 2 luni de la data începerilor cursurilor.

SELECT id_curs, data_incepere, round(MONTHS_BETWEEN(sysdate,data_incepere)),
LAST_DAY(data_incepere),
NEXT_DAY(data_incepere, 'Friday'),
ADD_MONTHS(data_incepere,2)
FROM CURSURI;
 


Concatenare

SELECT 'Studentul: ' || INITCAP(nume)|| ' face parte din grupa ' || id_grupa Grupa
FROM STUDENTI;
 

Operatorii ANY si ALL

Să se afişeze id_student, prenume si id_grupa pentru studentii care nu sunt in grupa 1043 si al caror an de nastere este mai mic decat oricare dintre anii de nastere ai studentilor care sunt in grupa 1043:

SELECT id_student, prenume, id_grupa
FROM STUDENTI
WHERE an_nastere < ANY
 (SELECT an_nastere FROM STUDENTI
WHERE id_grupa = '1043') 
AND id_grupa <> '1043'
ORDER BY an_nastere DESC;
 
Să se afişeze id_student, prenume si id_grupa pentru studentii care nu sunt in grupa 1023 si al caror an de nastere este mai mare decat fiecare dintre anii de nastere ai studentilor care sunt in grupa 1023:

SELECT id_student, prenume, id_grupa
FROM STUDENTI
WHERE an_nastere > ALL
 (SELECT an_nastere FROM STUDENTI
WHERE id_grupa = '1023') 
AND id_grupa <> '1023'
ORDER BY an_nastere DESC;
 




