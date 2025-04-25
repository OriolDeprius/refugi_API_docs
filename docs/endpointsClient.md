<!-- markdownlint-disable MD046 -->

# Endpoints Client

Aquí es mostrarà informació dels endpoints creats pels usuaris clients i el resultat de la seva petició.

!!! warning "Atenció"

    Totes les sol·licituds a l'API es faran a l'URL del servidor:

    http://elrefugidelbongust.daw.institutmontilivi.cat + /API + l'end point desitjat.

!!! question "Com fem les crides a la API?"

    En els nostres exemples mostrarem les crides des de JavaScript amb la biblioteca d'<a href="https://axios-http.com/" target="_blank">axios</a>.

## **/login (POST)**

Fa l'inici de sessió. Envies per `body` el nom d'usuari i contrasenya introduït per l'usuari juntament amb l'API Key per `header`.

???tip
    Recomenem sanejar les dades abans d'enviar-les. Així evitem SQL Injection.

Reps un `token` generat per identificar l'usuari, el nom d'usuari el qual ha iniciat sessió, i si és administrador o no.

!!!warning
    És important guardar el `token` rebut per fer la resta de consultes a l'API. Ja sigui a les `cookies`, `localstorage`, o de qualsevol altra manera.

### _Crida /login_

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

### _Respostes /login_

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

Fa un registre d'un nou usuari. Totes les dades requerides són obligatòries excepte el d'administrador. Les dades s'han d'enviar per body.

???tip
    Recomenem sanejar les dades abans d'enviar-les. Així evitem SQL Injection.

### _Crida /register_

És necessari enviar les dades del nou usuari a registrar a través del body de la petició.

- nomUser `string`
- pass `string`
- email `string`
- telefon `string`
- direccio `string`
- admin `boolean default false`

!!! warning "Atenció"
    Totes les dades mencionades anteriorment s'han d'enviar obligatòriament excepte `admin`. Si no saltarà error.

```js title="Exemple crida /register" linenums="1"
axios.post(`/API/register`, 
    {
        "nomUser": "Josep",
        "pass": "easjkhf18374ajshd!sa-3",
        "email": "josep34561@gmail.com",
        "telefon": "666666666",
        "direccio": "carrer antoni mercader 23, casa"
        //"admin": true
    })
    .then(res => {
        //tractar resposta
    })
```

### _Respostes /register_

- Si les dades són correctes rebràs un `json` amb codi `200`

```json title="Exemple resposta /register" linenums="1"
{
    "token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ1c2VyX2lkIjozNX0.Dc8c1OzG5JnyxO4KNsgGmBtv7sF_vcD6LZ_6nqRYTiQ",
    "nomUser": "Josep",
    "admin": false
}
```

- Si no envies les dades requerides rebràs un `string` amb codi `481`

```json title="Exemple resposta /register" linenums="1"
"Falten dades"
```

## **/historial (GET)**

Recuperes l'historial de comandes d'un usuari.

### _Crida /historial_

És necessari enviar el token d'identificació per header.

```js title="Exemple crida /historial" linenums="1"
axios.get('/API/historial',
    {
        headers: { 'Authorization': `Bearer ${token}`,
    }
})
    .then(res => {
        //tractar resposta
    })
    .catch(err => {
        //tractar errors
    });
```

### _Respostes /historial_

- Si el token és vàlid rebràs un `json` amb l'historial de l'usuari amb codi `200`

```json title="Exemple resposta" linenums="1"
[
    {
        "idComanda": 6,
        "estat": 1,
        "data": "2025-02-24 19:52:47",
        "preu": "24.00",
        "nom": "Amanida Alvocat",
        "tipus": "entrant",
        "sumplement": 3,
        "temps": 20
    },
    {
        "idComanda": 6,
        "estat": 1,
        "data": "2025-02-24 19:52:47",
        "preu": "24.00",
        "nom": "Suprema de Pollastre",
        "tipus": "principal",
        "sumplement": 6,
        "temps": 35
    },
    {
        "idComanda": 6,
        "estat": 1,
        "data": "2025-02-24 19:52:47",
        "preu": "24.00",
        "nom": "Tarta de Taronja",
        "tipus": "postre",
        "sumplement": 3,
        "temps": 15
    },
    {
        "idComanda": 24,
        "estat": 1,
        "data": "2025-02-25 16:44:24",
        "preu": "28.00",
        "nom": "Pat de Foie",
        "tipus": "entrant",
        "sumplement": 3,
        "temps": 25
    },
    {
        "idComanda": 24,
        "estat": 1,
        "data": "2025-02-25 16:44:24",
        "preu": "28.00",
        "nom": "Entrecot a la Brasa",
        "tipus": "principal",
        "sumplement": 7,
        "temps": 45
    },
    {
        "idComanda": 24,
        "estat": 1,
        "data": "2025-02-25 16:44:24",
        "preu": "28.00",
        "nom": "Tiramis",
        "tipus": "postre",
        "sumplement": 3,
        "temps": 20
    }
]
```

- Si no envies el token rebràs un `string` amb codi `230`

```json title="Exmeple resposta" linenums="1"
"Token invalid Token no enviat"
```

- Si el token enviat és invàlid rebràs un `string` amb codi `230`

```json title="Exmeple resposta" linenums="1"
"Token invalid Syntax error, malformed JSON"
```

## **/demanar (PUT)**

Fa una crida per guardar una comanda demanada per un client.

### _Crida /demanar_

És necessari enviar el token d'identificació per header.

És necessari enviar el preu del menú demanat i els id's dels plats (primer, segon i postres).

```js title="Exemple crida /demanar" linenums="1"
axios.put("/API/demanar",
    {
        'preu': 23,
        'idEntrant': 2,
        'idPrincipal': 15,
        'idPostre': 34,
    },
    {
        headers: {
            'Authorization': `Bearer ${token}`
        }
    }
    ).then(res => {
        //tractar resposta
    })
```

### _Respostes /demanar_

- Si tot és correcte rebràs un `string` amb codi `200`

```json title="Exemple de resposta" linenums="1"
"Comanda guardada"
```

- Si falten dades rebràs un `string` amb codi `212`

```json title="Exemple de resposta" linenums="1"
"Falten parametres de body!!"
```

!!!failure "Compte!"
    Si els ids dels plats no son vàlids, tornarà `500 Internal Server Error`

- Si no envies el token rebràs un `string` amb codi `212`

```json title="Exemple de resposta" linenums="1"
"Token invalid Token no enviat"
```

## **/preuMenu (POST)**

Reps la suma sense suplements del cost d'un menú.

### _Crida /preuMenu_

No és necessari enviar el token d'identificació.

És necessari enviar l'id del menú del qual sol·licites informació.

```js title="Exemple crida /preuMenu" linenums="1"
axios.post("/API/preuMenu",
    {
        'idMenu': 2
    })
    .then(res => {
        //tractar resposta
    })
```

### _Respostes /preuMenu_

- Si tot és correcte rebràs un `json` amb codi `200`

```json title="Exemple resposta" linenums="1"
{
    "preu": 15
}
```

- Si no envies l'id del menú que es vol el preu rebràs un `string` amb codi `292`

```json title="Exemple resposta" linenums="1"
"Falta idMenu"
```

## **/plats (GET)**

Llista els plats disponibles pel dia d'avui.

### _Crida /plats_

És necessari enviar el token d'identificació per header.

```js title="Exemple crida /plats" linenums="1"
axios.get("/API/plats", {
    headers: 
    {
        'Authorization': `Bearer ${token}`,
    }
})
    .then(res => {
        //tractar resposta
    });
```

### _Respostes /plats_

- Si la crida és correcta, rebràs un `json` amb codi `200`

```json title="Exemple resposta" linenums="1"
[
    {
        "idPlat": 195,
        "nom": "nom",
        "descripcio": "descripcio",
        "disponible": 1,
        "tipus": "entrant",
        "sumplement": 1,
        "temps": 1,
        "gluten": 1,
        "lactosa": 0,
        "idMenu": 4
    },
    {
        "idPlat": 196,
        "nom": "nom",
        "descripcio": "descripcio",
        "disponible": 1,
        "tipus": "pinciapl",
        "sumplement": 1,
        "temps": 1,
        "gluten": 1,
        "lactosa": 0,
        "idMenu": 4
    },
    {
        "idPlat": 199,
        "nom": "nom",
        "descripcio": "descripcio",
        "disponible": 1,
        "tipus": "postre",
        "sumplement": 1,
        "temps": 16,
        "gluten": 0,
        "lactosa": 1,
        "idMenu": 4
    }
]
```

- Si el servidor no rep el token o és invàlid tornarà un `string` amb codi `403`

```json title="Exemple resposta" linenums="1"
"Token invalid Token no enviat"
```

## **/platsDia (POST)**

Llista els plats disponibles per un dia en concret de la setmana (1-7).

### _Crida /platsDia_

No és necessari enviar el token d'identificació.

És necessari enviar el dia del qual es volen veure els plats.

```js title="Exemple crida /platsDia" linenums="1"
axios.post("/API/platsDia",
    {
        "dia": "[numero entre 1 i 7]"
    })
    .then(res => {
        //tractar la resposta
    });
```

### _Respostes /platsDia_

- Resposta d'una consulta ben executada. Rebràs un `json` amb codi `200`

```json title="Exemple resposta" linenums="1"
[
    {
        "idPlat": 31,
        "nom": "nom",
        "descripcio": "descripcio",
        "disponible": 1,
        "tipus": "entrant",
        "sumplement": 25,
        "temps": 11,
        "gluten": 0,
        "lactosa": 1,
        "idMenu": 1
    },
    {
        "idPlat": 52,
        "nom": "nom",
        "descripcio": "descripcio",
        "disponible": 1,
        "tipus": "principal",
        "sumplement": 1,
        "temps": 1,
        "gluten": 1,
        "lactosa": 1,
        "idMenu": 1
    },
    {
        "idPlat": 191,
        "nom": "nom",
        "descripcio": "descripcio",
        "disponible": 1,
        "tipus": "postres",
        "sumplement": 2,
        "temps": 2,
        "gluten": 0,
        "lactosa": 1,
        "idMenu": 1
    }
]
```

- Resposta amb un `dia` no vàlid. Rebràs un `string`amb codi `404`

```json title="Exemple resposta" linenums="1"
"Falten dades"
```

## **/admin (GET)**

Segons el token enviat, sabràs si l'usuari és administrador o no.

### _Crida /admin_

És necessari enviar el token d'identificació.

```js title="Exemple crida /admin" linenums="1"
axios.get('/API/admin',
{
    headers: {
        'Authorization': `Bearer ${token}`
    }
})
    .then(res => {
        // tractar resposta
    })
```

### _Respostes /admin_

- Resposta amb `token` no administrador. Rebràs un `string` amb codi `200`

```json title="Exemple resposta" linenums="1"
"no admin"
```

- Resposta amb `token` no vàlid. Rebràs un `string`amb codi `403

```json title="Exemple resposta" linenums="1"
"Token invalid Signature verification failed"
```

???question "Com cridar /admin com administrador?"
    [Crida /admin com administrador](/endpointsAdmin/#admin-get)
