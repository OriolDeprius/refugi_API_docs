# Endpoints Client

Aquí es mostrarà informació dels endpoints creats pels usuaris clients i el resultat de la seva petició.

!!! warning "Atenció"

    Totes les sol·licituds a l'API es faran a l'URL del servidor:

    http://elrefugidelbongust.daw.institutmontilivi.cat + /API + l'end point desitjat.

!!! question "Com fem les crides a la API?"

    En els nostres exemples mostrarem les crides des de JavaScript amb la biblioteca d'<a href="https://axios-http.com/" target="_blank">axios</a>.

## **/login (POST)**

### _Crida_

És necessari enviar tant l'api-key com a paràmetre de l'URL, com les dades de login a través del body de la petició.

```js title="Exemple de crida" linenums="1"

axios.post(`/API/login?apiKey=${apiKey}`, 
{
    nomUser: user,
    pass: password,
})
.then(res => {
    //tractar resposta
})
.catch(err =>{
    //tractar errors
});

```

### _Respostes_

- Si les dades **son correctes** rebrà un `json` amb codi `200`

```json title="Exemple de resposta" linenums="1"

{
    "token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ1c2VyX2lkIjozNX0.Dc8c1OzG5JnyxO4KNsgGmBtv7sF_vcD6LZ_6nqRYTiQ",
    "nomUser": "josep",
    "admin": false
}

```

- Si la contrasenya **no és correcta** rebrà un `string` amb codi `249`

```json title="Exemple de resposta" linenums="1"
"La contrasenya no és correcta"
```

- Si l'usuari **no existeix** rebrà un `string` amb codi `250`

```json title="Exmeple de resposta" linenums="1"

"La consulta no ha tornat dades"

```

- Si la petició **no porta API Key** rebrà un `string` amb codi `404`

```json title="Exemple de resposta" linenums="1"

"No s'ha enviat la api key"

```

- Si l'**API Key no és correcta** rebrà un `string` amb codi `300`

```json title="Exemple de resposta" linenums="1"

"Api key no correcte"

```

## **/register (POST)**

### _Crida_

És necessari enviar les dades del nou usuari a registrar a través del body de la petició.

### _Respostes_

Rebras

## **/historial (POST)**

### _Crida_

És necessari enviar el token d'identificació per header.

### _Respostes_

Rebras

## **/demanar (PUT)**

### _Crida_

És necessari enviar el token d'identificació per header.

És necessari enviar el preu del menú demanat i els id's dels plats (primer, segon i postres).

### _Respostes_

Rebras

## **/preuMenu (POST)**

### _Crida_

No és necessari enviar el token d'identificació.

És necessari enviar l'id del menú del qual sol·licites informació.

### _Respostes_

Rebras

## **/plats (GET)**

### _Crida_

És necessari enviar el token d'identificació per header.

### _Respostes_

Rebras

## **/platsDia (POST)**

### _Crida_

No és necessari enviar el token d'identificació.

És necessari enviar el dia del qual es volen veure els plats.

### _Respostes_

Rebras

## **/admin (GET)**

### _Crida_

És necessari enviar el token d'identificació.

### _Respostes_

Rebras
