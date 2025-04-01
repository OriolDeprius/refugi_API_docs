# Endpoints Client

Aquí es mostrarà informació dels endpoints creats pels usuaris clients i el resultat de la seva petició.

!!! warning "Atenció"

    Totes les sol·licituds a l'API es faran a l'URL del servidor:
    
    http://elrefugidelbongust.daw.institutmontilivi.cat + /API + l'end point desitjat.



## /login (POST)

### Crida

És necessari enviar tant l'api-key com a paràmetre de l'URL, com les dades de login a través del body de la petició.

Retorna un token identificatiu, el nom d'usuari i si es admin o no.

### Respostes

Rebras

## /register (POST)

### Crida

És necessari enviar les dades del nou usuari a registrar a través del body de la petició.

Retorna un token identificatiu, el nom d'usuari i si es admin o no.

### Respostes

Rebras

## /historial (POST) 

### Crida

És necessari enviar el token d'identificació per header.

### Respostes

Rebras

## /demanar (PUT

### Crida

És necessari enviar el token d'identificació per header.

És necessari enviar el preu del menú demanat i els id's dels plats (primer, segon i postres).

### Respostes

Rebras

## /preuMenu (POST)

### Crida

No és necessari enviar el token d'identificació.

És necessari enviar l'id del menú del qual sol·licites informació.

### Respostes

Rebras

## /plats (GET)

### Crida

És necessari enviar el token d'identificació per header.

### Respostes

Rebras

## /platsDia (POST)

### Crida

No és necessari enviar el token d'identificació.

És necessari enviar el dia del qual es volen veure els plats.

### Respostes

Rebras

## /admin (GET)

### Crida

És necessari enviar el token d'identificació.

### Respostes

Rebras