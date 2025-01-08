```sql

-- 1. Conta il numero di articoli scritti da ogni utente.

select u.nome, u.cognome, a.id_utente, count(*) as 'ArticoliScritti'
from articoli a
join utenti u
on a.id_utente = u.id_utente
group by a.id_utente


-- 2. Trova la categoria con il maggior numero di articoli associati.

select c.nome_categoria, ac.id_categoria, count(*)
from categorie c
join articoli_categorie ac
on c.id_categoria = ac.id_categoria
join articoli a
on ac.id_articolo = a.id_articolo
group by ac.id_categoria
limit 1


-- 3. Recupera gli utenti che hanno scritto più di 2 articoli.

select u.nome, u.cognome, a.id_utente, count(*)
from utenti u
join articoli a
on u.id_utente = a.id_utente
group by a.id_utente
having count(*) > 2


-- 4. Calcola la data di pubblicazione più recente per ogni categoria.

select c.nome_categoria, c.id_categoria, max(data_pubblicazione) as 'PubblicazioneRecente'
from articoli a
join articoli_categorie ac
on a.id_articolo = ac.id_articolo
join categorie c
on ac.id_categoria = c.id_categoria
group by c.id_categoria


-- ?? 5. Trova il numero medio di articoli per utente. ?? (non risolta)

select u.nome, u.cognome, avg(a.id_utente) as 'NumMedio'
from utenti u
join articoli a
on u.id_utente = a.id_utente
group by a.id_utente


-- 6. Recupera le categorie che hanno almeno 3 articoli associati.

select c.nome_categoria, COUNT(*) as 'NumeroArticoli'
from categorie c
join articoli_categorie ac
on c.id_categoria = ac.id_categoria
join articoli a
on a.id_articolo = ac.id_articolo
group by c.nome_categoria
having COUNT(*) >= 3


-- 7. Calcola il totale degli articoli pubblicati per ogni mese del 2024.

select month(a.data_pubblicazione) as 'MesePubblicazione', COUNT(*) as 'TotaleArticoli'
from articoli a
group by month(a.data_pubblicazione)


-- 8. Trova l'utente che ha la data di iscrizione più antica.

select u.nome, u.cognome, u.data_iscrizione
from utenti u
order by u.data_iscrizione
limit 1


-- 9. Recupera le categorie e il numero di articoli associati a ciascuna, ordinati dal più al meno.

select c.nome_categoria, COUNT(*) as 'NumeroArticoli'
from categorie c
join articoli_categorie ac
on c.id_categoria = ac.id_categoria
join articoli a
on a.id_articolo = ac.id_articolo
group by c.nome_categoria
order by COUNT(*) desc


-- 10. Calcola il numero totale di articoli pubblicati da utenti iscritti nel 2024.

select u.nome, u.cognome, year(u.data_iscrizione), a.id_utente, COUNT(*) AS 'NumeroArticoli'
from articoli a
join utenti u
on a.id_utente = u.id_utente
where YEAR(u.data_iscrizione) = 2024
group by a.id_utente
