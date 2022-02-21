DROP TABLE GRUPA CASCADE CONSTRAINTS;
DROP TABLE STUDENTI CASCADE CONSTRAINTS;
DROP TABLE CURSURI CASCADE CONSTRAINTS;
DROP TABLE ORAR CASCADE CONSTRAINTS;
DROP TABLE TEST CASCADE CONSTRAINTS;
prompt
prompt Creating table GRUPA
prompt ======================
prompt
create table GRUPA
(
  id_grupa  NUMBER constraint pk_g_grupa primary key,
  facultate VARCHAR2(35),
  specialitate VARCHAR2(30)
)
;
alter table GRUPA
  add constraint FACULTATE_NN
  check ("FACULTATE" IS NOT NULL); 

prompt
prompt Creating table STUDENTI
prompt ======================
prompt
create table STUDENTI
(
  id_student VARCHAR2(25) constraint pk_s_studenti primary key,
  nume VARCHAR2(25),
  prenume VARCHAR(20),
  an_nastere NUMBER(4),
  cnp NUMBER(13),
  id_grupa NUMBER,
  constraint fk_studenti foreign key (id_grupa) references GRUPA (id_grupa)
)
;

alter table STUDENTI
  add constraint ID_STUDENT_NN
  check ("ID_STUDENT" IS NOT NULL);
alter table STUDENTI
  add constraint NUME_NN
  check ("NUME" IS NOT NULL);
alter table STUDENTI
  add constraint PRENUME_NN
  check ("PRENUME" IS NOT NULL);
  
   
  
prompt
prompt Creating table CURSURI
prompt ======================
prompt
create table CURSURI
(
  id_curs      VARCHAR2(3) constraint pk_c_cursuri primary key, 
  nume_curs VARCHAR2(38),
  profesor      VARCHAR2(35),
 id_grupa NUMBER,
 data_incepere DATE,
 salariul number,
 comision number,
 constraint fk_cursuri foreign key (id_grupa) references GRUPA(id_grupa)
)
;

alter table CURSURI
  add constraint ID_CURS_NN
  check ("ID_CURS" IS NOT NULL); 
  
prompt
prompt Creating table ORAR
prompt ======================
prompt
create table ORAR
(
  id_zi              VARCHAR2(9) constraint pk_zi_orar primary key,
  interval_orar      VARCHAR2(8),
  id_curs          VARCHAR2(3),
  constraint fk_orar foreign key (id_curs) references CURSURI(id_curs)
)
;


prompt 5 exemple insert
insert into GRUPA(id_grupa,facultate, specialitate)
values(1043,'ASE','CSIE');

insert into GRUPA(id_grupa,facultate, specialitate)
values(1047,'ASE','CSIE');

INSERT INTO STUDENTI (id_student, nume, prenume, an_nastere, cnp, id_grupa) VALUES ('2131', 'Popescu','Ionel',2001,6582568267921, 1043);
SELECT * FROM STUDENTI;

INSERT INTO STUDENTI (id_student, nume, prenume, an_nastere, cnp, id_grupa) VALUES ('345', 'Antonio','Alexandru',2001,582926267914, 1047);
SELECT * FROM STUDENTI;

INSERT INTO STUDENTI  (id_student, nume, prenume, an_nastere, cnp, id_grupa)
VALUES ('&id_student','&nume','&prenume', '&an_nastere','&cnp', '&id_grupa');

prompt 2 exemple update 

UPDATE STUDENTI
SET id_grupa=id_grupa+10
WHERE an_nastere>2001;
SELECT * FROM Studenti;

UPDATE STUDENTI
SET id_grupa=(SELECT id_grupa FROM STUDENTI WHERE id_student=2131)
WHERE an_nastere=2002;
SELECT * FROM Studenti;

prompt 2 exemple delete

DELETE FROM Studenti
WHERE id_grupa IN (1047);

DELETE FROM STUDENTI;
SELECT * FROM STUDENTI;

prompt Loading Grupa
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
prompt 5 records loaded

prompt  Loading Cursuri...
insert into CURSURI(id_curs,nume_curs, profesor,id_grupa,data_incepere,salariul,comision)
values('POO','Programare Orientata Obiect', 'Alin Zamfiroiu',1043,to_date('2021-09-27', 'yyyy-mm-dd'),24000,null);
insert into CURSURI(id_curs,nume_curs, profesor,id_grupa,data_incepere,salariul,comision)
values('BDD','Baze de date', 'Stefan Preda',1047,to_date('2021-12-23', 'yyyy-mm-dd'), 17000,null);
insert into CURSURI(id_curs,nume_curs, profesor,id_grupa,data_incepere,salariul,comision)
values('PSM','Probabilitati si statistica matematica', 'Liana Manu Iosifescu',1023,to_date('2022-02-25', 'yyyy-mm-dd'), 17000,null);
insert into CURSURI(id_curs,nume_curs, profesor,id_grupa,data_incepere,salariul,comision)
values('SM','Statistica macroeconomica', ' Simona Andreea Apostu',1028,to_date('2022-04-15', 'yyyy-mm-dd'), 9000,null);
insert into CURSURI(id_curs,nume_curs, profesor,id_grupa,data_incepere,salariul,comision)
values('FIN','Finante', ' Stefan Cristian Gherghina',1072,to_date('2021-11-12', 'yyyy-mm-dd'), 11000,null);
insert into CURSURI(id_curs,nume_curs, profesor,id_grupa,data_incepere,salariul,comision)
values('MAN','Managemant', 'Ovidiu Andrei Cristian Buzoianu',1043,to_date('2021-10-19', 'yyyy-mm-dd'), 14000,null);
insert into CURSURI(id_curs,nume_curs, profesor,id_grupa,data_incepere,salariul,comision)
values('EFS','Educatie fizica si sport', 'Dumitru Vasilescu',1048,to_date('2022-06-12', 'yyyy-mm-dd'), 13000,null);
commit;
prompt 7 records loaded

prompt Loading Studenti...
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
prompt 7 records loaded



prompt Loading Orar...
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

prompt 1 exemplu merge

MERGE INTO STUDENTI USING GRUPA
ON (STUDENTI.id_GRUPA = GRUPA.id_grupa)
WHEN MATCHED THEN 
UPDATE SET STUDENTI.id_student=STUDENTi.id_student+2;

prompt 1 exemplu ANY

SELECT id_student, prenume, id_grupa
FROM STUDENTI
WHERE an_nastere < ANY
 (SELECT an_nastere FROM STUDENTI
WHERE id_grupa = '1023') 
AND id_grupa <> '1023'
ORDER BY an_nastere DESC; 

prompt 1 exemplu ALL

SELECT id_student, prenume, id_grupa
FROM STUDENTI
WHERE an_nastere > ALL
 (SELECT an_nastere FROM STUDENTI
WHERE id_grupa = '1023') 
AND id_grupa <> '1023'
ORDER BY an_nastere DESC; 

prompt 1 exemplu jonctiune egalitate

SELECT STUDENTI.*, GRUPA.* 
FROM STUDENTI, GRUPA
WHERE STUDENTI.id_grupa=GRUPA.id_grupa;

prompt 1 exemplu jonctiune externa

SELECT STUDENTI.id_STUDENT, STUDENTI.prenume, GRUPA.id_grupa, GRUPA.facultate
FROM STUDENTI, GRUPA
WHERE STUDENTI.id_grupa = GRUPA.id_grupa (+);

prompt 1 exemplu interogari subordonate

SELECT nume, prenume, id_student, id_grupa FROM STUDENTI WHERE id_grupa = 1043;

prompt 1 exemplu pentru upper

SELECT id_student, UPPER(nume)
FROM STUDENTI
WHERE id_grupa=1043;

prompt 1 exemplu concatenare

SELECT 'Studentul: ' || INITCAP(nume)|| ' face parte din grupa ' || id_grupa
FROM STUDENTI;

prompt 1 exemplu SUBSTR

SELECT SUBSTR(nume, 1, 5) AS Nume
FROM STUDENTI;

prompt 1 exemplu SYSDATE

SELECT SYSDATE data_curenta FROM DUAL;

prompt 1 exemplu MONTHS_BETWEEN + ADD_MONTHS + NEXT_DAY + LAST_DAY

SELECT id_curs, data_incepere, round(MONTHS_BETWEEN(sysdate,data_incepere)),
LAST_DAY(data_incepere),
NEXT_DAY(data_incepere, 'Friday'),
ADD_MONTHS(data_incepere,2)
FROM CURSURI;


prompt 1 exemplu TO_NUMBER

TO_NUMBER(char[, 'format_model'])
SELECT TO_NUMBER('RON12.345,64', 'L99G999D99') FROM DUAL;
   ALTER SESSION SET NLS_CURRENCY = 'RON';
   CREATE TABLE test(NUMAR VARCHAR2(50));
   INSERT INTO test SELECT salariul FROM CURSURI;
   UPDATE test
   SET numar = 'RON'||numar;
   SELECT * FROM test;
   SELECT TO_NUMBER(numar,'L99999') FROM test;

prompt 1 exemplu NVL-salariul anual

SELECT profesor, salariul*12 + salariul*12*NVL(comision,0) venit_anual
FROM CURSURI;

prompt 1 exemplu COUNT- nr de studenti

SELECT COUNT(id_student) nr_studenti
FROM STUDENTI

prompt 1 exemplu SUM-total salarii pe o luna

SELECT SUM(salariul * COUNT (id_curs)) total_salarii
FROM CURSURI
GROUP BY CURSURI.salariul

prompt 1 exemplu MAX + MIN - data primul curs + ultimul

SELECT MIN(data_incepere), MAX(data_incepere) FROM CURSURI

prompt 1 exemplu TOP-DOWN

SELECT id_student, nume, an_nastere, level FROM  STUDENTI
WHERE id_grupa IN (1043, 1047)
CONNECT BY PRIOR id_student = an_nastere

prompt 1 exemplu CASE
prompt comision 0.1% POO
prompt comision 0.2% BDD
prompt comision 0.3% MAN

SELECT profesor, id_curs, 
CASE WHEN UPPER(id_curs) = 'MAN' THEN 0.3
WHEN UPPER(id_curs) =  'BDD' THEN 0.2
WHEN UPPER(id_curs) = 'POO' THEN 0.1
ELSE 0 END comision
FROM CURSURI;

prompt 1 exemplu  MINUS

SELECT * FROM CURSURI WHERE salariul BETWEEN 13000 AND 24000
MINUS
SELECT * FROM CURSURI WHERE salariul IN (17000, 11000);

prompt 2 exemple VIEW 

CREATE OR REPLACE VIEW V_CURSURI
AS SELECT * FROM CURSURI
WHERE id_grupa=1043;
SELECT * FROM V_CURSURI;
UPDATE V_CURSURI
SET salariul = salariul + 1000;

CREATE OR REPLACE VIEW salariu_pe_an
AS SELECT id_curs, nume_curs, salariul*12 salariu_an FROM CURSURI
WITH READ ONLY

prompt 2 exemple indecsi

SELECT * FROM STUDENTI WHERE (id_grupa) = 1043;
CREATE INDEX idx_id_grupa ON STUDENTI(UPPER(id_grupa));

DROP INDEX idx_id_grupa;

prompt 1 exemplu secventa

CREATE OR REPLACE VIEW total_studenti
AS SELECT id_student, nume, prenume, an_nastere, cnp, id_grupa FROM STUDENTI

CREATE SEQUENCE seq_id_student 
START WITH 500 INCREMENT BY 10
MAXVALUE 1000 NOCYCLE;

INSERT INTO total_studenti VALUES (seq_id_student.NEXTVAL, 'Caloian', 'Cosmin', 2001, '5013636373324', 1043);
SELECT seq_id_student.CURRVAL FROM DUAL;



  
  
