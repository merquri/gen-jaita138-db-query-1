```sql

-- 1. Recupera tutti gli utenti registrati nel sistema.  

select *
from utenti u


-- 2. Recupera il nome, cognome e email di tutti gli utenti iscritti dopo il 1° marzo 2024.

select nome, cognome, email
from utenti u
where data_iscrizione > '2024-03-01'


-- 3. Recupera tutti gli articoli insieme al nome e cognome dell'autore.

select u.nome, u.cognome, a.titolo, a.contenuto
from utenti u
join articoli a
on u.id_utente = a.id_utente
  

-- 4. Recupera i titoli degli articoli pubblicati nel mese di maggio 2024.

select titolo, data_pubblicazione
from articoli
where data_pubblicazione between '2024-05-01' and '2024-05-31'
  

-- 5. Recupera le prime 5 categorie ordinate alfabeticamente per nome.

select *
from categorie
order by nome_categoria
limit 5
  

-- 6. Recupera gli articoli che appartengono alla categoria 'Tecnologia'.
  
select a.titolo, c.nome_categoria
from articoli a
join articoli_categorie ac
on a.id_articolo = ac.id_articolo
join categorie c
on ac.id_categoria = c.id_categoria
where c.id_categoria = 1
  

-- 7. Recupera le email degli utenti che hanno scritto almeno un articolo.

select u.email
from utenti u
join articoli a
on u.id_utente = a.id_utente
where a.id_utente >= 1


-- 8. Recupera tutti gli articoli pubblicati tra il 1° giugno 2024 e il 31 agosto 2024.

select *
from articoli a
where data_pubblicazione between '2024-06-01' and '2024-08-31'

-- 9. Recupera i dettagli delle categorie associate all'articolo con `id_articolo` = 10.

select a.id_articolo, a.titolo, a.contenuto, c.nome_categoria, c.descrizione
from articoli a
join articoli_categorie ac
on a.id_articolo = ac.id_articolo
join categorie c
on ac.id_categoria = c.id_categoria
where a.id_articolo = 10


-- 10. Recupera i nomi degli utenti ordinati per data di iscrizione più recente.

select nome, cognome, data_iscrizione
from utenti
order by data_iscrizione desc
