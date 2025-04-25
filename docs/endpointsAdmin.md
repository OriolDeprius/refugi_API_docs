<!-- markdownlint-disable MD046 -->
<!-- markdownlint-disable MD010 -->

# Endpoints Admin

Aquí es mostrarà informació dels endpoints creats pels usuaris Administradors i el resultat de la seva petició.

!!! warning "Atenció"

    Totes les sol·licituds a l'API es faran a l'URL del servidor:

    http://elrefugidelbongust.daw.institutmontilivi.cat + /API + l'end point desitjat.

!!! question "Com fem les crides a l'API?"

    En els nostres exemples mostrarem les crides des de JavaScript amb la biblioteca d'<a href="https://axios-http.com/" target="_blank">axios</a>.

!!! info "Tots els tokens enviats han de ser d'administrador perquè la petició retorni dades"

## **/eliminarComanda (DELETE)**

### _Crida /eliminarComanda_

És necessari enviar el token d'identificació per header.

És necessari enviar l'id de comanda.

```js title="Exemple de crida" linenums="1"
axios.delete('/API/eliminarComanda', {
	data: {
		idComanda: "idComandaEliminar"
	},
	headers: {
		'Authorization': `Bearer ${token}`
	}
}).then(res => {
	//Tractar resposta
}).catch(err => {
	//Tractar errors
});
```

### _Respostes /eliminarComanda_

- Si es fa una sol·licitud correcta rebrà un codi `200`

- Si es fa una sol·licitud amb un **token invàlid** rebrà un codi `500`

- Si es fa una sol·licitud amb un token que **no és d'administrador** rebrà un `string` amb codi `401`

```json title="Exemple sortida" linenums="1"
"No admin"
```

- Si es fa una sol·licitud **sense dades** o amb **alguna faltant** rebrà un codi `230 plat no trobat`

```json title="Exemple sortida" linenums="1"
"Falta enviar el idComanda a eliminar!"
```

## **/comandesAdmin (GET)**

### _Crida /comandesAdmin_

És necessari enviar el token d'identificació per header.

```js title="Exemple de crida" linenums="1"
axios.get('/API/comandesAdmin', {
	headers: {
		'Authorization': `Bearer ${token}`,
	}
}).then(res => {
	//Tractar resposta
});
```

### _Respostes /comandesAdmin_

- Si es fa una sol·licitud correcta rebrà un `JSON` amb codi `200`

```json title="Exemple sortida" linenums="1"
[
    {
        "idComanda": 52314,
        "estat": 0,
        "data": "2025-04-03 12:43:14",
        "preu": "20.00",
        "nom": "Crema de Tomquet",
        "tipus": "entrant",
        "sumplement": 2,
        "temps": 20,
        "nomUser": "admin"
    },
    {
        "idComanda": 52314,
        "estat": 0,
        "data": "2025-04-03 12:43:14",
        "preu": "20.00",
        "nom": "Entrecot a la Brasa",
        "tipus": "principal",
        "sumplement": 7,
        "temps": 45,
        "nomUser": "admin"
    },
]
```

- Si es fa una sol·licitud amb un **token invàlid** rebrà un codi `500`

```json title="Exemple sortida" linenums="1"
"Token invalid Signature verification failed"
```

- Si es fa una sol·licitud amb un token que **no és d'administrador** rebrà un codi `500`

## **/deletePlat (PUT)**

### _Crida /deletePlat_

??? note "Informació"
    Realment no esborra el plat, sinó que canvia la propietat `disponible` de `true` a `false`

És necessari enviar el token d'identificació per header.

És necessari enviar l'id del plat a esborrar.

```js title="Exemple de crida" linenums="1"
axios.put("/API/deletePlat",
	{
		'idPlat': "idPlat"
	},
	{
		headers: { 'Authorization': `Bearer ${token}` }
	}
)
	.then(res => {
		//Tractar resposta
	})
	.catch(err => {
		//Tractar error
	});

```

### _Respostes /deletePlat_

- Si es fa una sol·licitud correcta rebrà un `string` amb codi `200`

```json title="Exemple sortida" linenums="1"
"Plat eliminat"
```

- Si es fa una sol·licitud amb un **token invàlid** rebrà un codi `500`

```json title="Exemple sortida" linenums="1"
"Token invalid Signature verification failed"
```

- Si es fa una sol·licitud amb un token que **no és d'administrador** rebrà un `string` amb codi `401`

```json title="Exemple sortida" linenums="1"
"No admin"
```

- Si es fa una sol·licitud **sense dades** o amb **alguna faltant** rebrà un codi `404 Plat no trobat`

## **/habilitarPlat (PUT)**

### _Crida /habilitarPlat_

És necessari enviar el token d'identificació per header.

És necessari enviar l'id del plat a activar.

```js title="Exemple de crida" linenums="1"
axios.put("/API/habilitarPlat",
	{
		'idPlat': "idPlat"
	},
	{
		headers: { 'Authorization': `Bearer ${token}` }
	}
)
	.then(res => {
		//Tractar resposta
	})
	.catch(err => {
		//Tracta error
	});

```

### _Respostes /habilitarPlat_

- Si es fa una sol·licitud correcta rebrà un `string` amb codi `200`

```json title="Exemple sortida" linenums="1"
"Plat habilitat"
```

- Si es fa una sol·licitud amb un **token invàlid** rebrà un codi `500`

```json title="Exemple sortida" linenums="1"
"Token invalid Signature verification failed""
```

- Si es fa una sol·licitud amb un token que **no és d'administrador** rebrà un `string` amb codi `401`

```json title="Exemple sortida" linenums="1"
"No admin"
```

- Si es fa una sol·licitud **sense dades** o amb **alguna faltant** rebrà un codi `404 Plat no trobat`

## **/updatePlat (PUT)**

### _Crida /updatePlat_

És necessari enviar el token d'identificació per header.

És necessari enviar per body:

- idPlat
- nom
- descripcio
- tipus
- suplement
- temps
- gluten
- lactosa

```js title="Exemple de crida" linenums="1"
axios.put("/API/updatePlat",
	{
		'nom': "nom",
		'descripcio': "descripcio",
		'suplement': "suplement",
		'temps': "temps",
		'tipus': "tipus",
		'gluten': "gluten",
		'lactosa': "lactosa",
		'idPlat': "idPlat"
	},
	{
		headers: { 'Authorization': `Bearer ${token}` }
	})
	.then(res => {
		//Tractar resposta
	}).catch(err => {
		//Tractar error
		})
```

### _Respostes /updatePlat_

- Si es fa una sol·licitud correcta rebrà un `JSON` amb codi `200` i la informacio del plat modificat

```json title="Exemple sortida" linenums="1"
{
	"idPlat": 31,
	"nom": "nomCanviat",
	"descripcio": "descripcioCanviada",
	"tipus": "tipusCanviat",
	"suplement": 25,
	"temps": "11",
	"gluten": 0,
	"lactosa": 1
}
```

- Si es fa una sol·licitud amb un **token invàlid** rebrà un string amb codi `404 NO ADMIN`

```json title="Exemple sortida" linenums="1"
"Token invalid. Token no enviat. No admin"
```

- Si es fa una sol·licitud amb un token que **no és d'administrador** rebrà un `string` amb codi `404 NO ADMIN`

```json title="Exemple sortida" linenums="1"
"No admin"
```

- Si es fa una sol·licitud **sense dades** o amb **alguna faltant rebrà un string amb un codi `404 PLAT NO TROBAT`

```json title="Exemple sortida" linenums="1"
"Plat no trobat"
```

## **/deleteDiaPlat (PUT)**

### _Crida /deleteDiaPlat_

És necessari enviar el token d'identificació per header.

És necessari enviar per body l'id del plat sobre el qual es vol actuar i els id's dels dies que ja no es vol servir el plat en qüestio.

```js title="Exemple de crida" linenums="1"
 axios.put("/API/deleteDiaPlat",
		{
			idPlat: "idPlatModificarDies"
		},
		{
			headers: { 'Authorization': `Bearer ${token}` }
		}
	).then(res => {
		//Tractar resposta
	}).catch(err => {
		//Tractar error
	})
```

### _Respostes /updatePlat_

- Si es fa una sol·licitud correcta rebrà un `string` amb codi `200`

```json title="Exemple sortida" linenums="1"
"Plat eliminat del dia"
```

- Si es fa una sol·licitud amb un **token invàlid** rebrà un string amb codi `500 INTERNAL SERVER ERROR`

- Si es fa una sol·licitud **sense idPlat**  rebra un `string` amb codi `403 FORBIDDEN`

```json title="Exemple sortida" linenums="1"
"Falten dades"
```

- Si es fa una sol·licitud **amb idPlat inexistent** rebra un `string` amb codi `404 NO OK`

```json title="Exemple sortida" linenums="1"
"Plat no eliminat del dia"
```

## **/insertDiaPlat (PUT)**

### _Crida /insertDiaPlat_

És necessari enviar el token d'identificació per header.

És necessari enviar per body l'id del plat sobre el qual es vol actuar i els dies que es vol posar el plat (array de id's).

```js title="Exemple de crida" linenums="1"
axios.put("/API/insertDiaPlat",
		{
			idPlat: "idPlat",
			dies: ["arrayPlats"]
		},
		{
			headers: { Authorization: `Bearer ${token}` },
		}
	).then(res => {
		//tractar resposta
	}).catch(err => {
		//tractar resposta
	})
```

### _Respostes /insertDiaPlat_

- Si es fa una sol·licitud correcta rebrà un `string` amb codi `200`

```json title="Exemple sortida" linenums="1"
"Plat afegit al dia"
```

- Si es fa una sol·licitud amb un **token invàlid** rebrà un codi `500`

- Si es fa una sol·licitud amb un token que **no és d'administrador** rebrà un `string` amb codi `401`

```json title="Exemple sortida" linenums="1"
"No admin"
```

- Si es fa una sol·licitud **sense dades** o amb **alguna faltant** rebrà un `string` amb codi `404`

```json title="Exemple sortida" linenums="1"
"Falten dades"
```

## **/nouPlat (PUT)**

### _Crida /nouPlat_

És necessari enviar el token d'identificació per header.

És necessari enviar per body:

- nom
- descripcio
- tipus
- suplement
- temps
- gluten
- lactosa
- idMenu

```js title="Exemple de crida" linenums="1"
axios.put("/API/nouPlat",
	{
		nom: "nom",
		descripcio: "descripcio",
		suplement: 2,
		temps: 20,
		tipus: "tipus",
		idMenu: 4,
		gluten: 1,
		lactosa: 0,
	},
	{
		headers: { Authorization: `Bearer ${token}` },
	})
	.then((res) => {
		//tractar resposta
	})
	.catch((err) => {
		//tractar errors
	});
```

### _Respostes /nouPlat_

- Si es fa una sol·licitud correcta rebrà un `string` amb codi `200`

```json title="Exemple sortida" linenums="1"
"Plat afegit"
```

- Si es fa una sol·licitud amb un **token invàlid** rebrà un `string` amb codi `401`

```json title="Exemple sortida" linenums="1"
"Token invalid. Token no enviat. No admin"
```

- Si es fa una sol·licitud amb un token que **no és d'administrador** rebrà un `string` amb codi `401`

```json title="Exemple sortida" linenums="1"
"No admin"
```

- Si es fa una sol·licitud **sense dades** o amb **alguna faltant** rebrà un `string` amb codi `404`

```json title="Exemple sortida" linenums="1"
"Falten dades"
```

## **/platsTots (GET)**

### _Crida /platsTots_

És necessari enviar el token d'identificació per header.

```js title="Exemple crida" linenums="1"
axios.get("/API/platsTots", {
		headers: {
			Authorization: `Bearer ${token}`,
		},
	})
	.then((res) => {
		//tractar resposta
	})
	.catch((err) => {
		//tractar errors
	});
```

### _Respostes /platsTots_

- Si el token **és d'administrador** rebrà un `object` i codi `200`

```json title="Exemple de sortida" linenums="1"
[
	{
		"idPlat": 2,
		"nom": "Crema de Tomàquet",
		"descripcio": "Crema de tomàquet fresca amb orenga i un toc de crema de llet.",
		"disponible": 0,
		"tipus": "entrant",
		"suplement": 2,
		"temps": 20,
		"gluten": 0,
		"lactosa": 1,
		"idMenu": 1
	},
	{
		"idPlat": 3,
		"nom": "Croquetes Casolanes",
		"descripcio": "Croquetes de pernil ibèric amb una capa cruixent per fora i crems per dins.",
		"disponible": 0,
		"tipus": "entrant",
		"suplement": 3,
		"temps": 15,
		"gluten": 1,
		"lactosa": 1,
		"idMenu": 1
	}
]
```

- Si el token **no és d'administrador** rebrà un `string` amb codi `401`

```json title="Exemple de sortida" linenums="1"
"L'usuari no es admin"
```

- Si el token **no és vàlid** rebrà un `string` amb codi `403`

```json title="Exemple de sortida" linenums="1"
"Token invalid. Token no enviat"
```

## **/admin (GET)**

### _Crida /admin_

És necessari enviar el token d'identificació.

```js title="Exemple crida" linenums="1" hl_lines="3"
axios.get("/API/admin", {
		headers: {
			Authorization: `Bearer ${token}`,
		},
	})
	.then((res) => {
		//tractar la resposta
	})
	.catch((err) => {
		//tractar errors
	});
```

### _Respostes /admin_

- Si el token de l'usuari que ha fet la crida **és administrador**, rebrà un `string` i codi `200`

```json title="Exemple de sortida" linenums="1"
"admin"
```

- Si el token de l'usuari que ha fet la crida **no és administrador**, rebrà un `string` i codi `299`

```json title="Exemple de sortida" linenums="1"
"no admin"
```

- Si el **token no és vàlid**, rebrà un `string` i codi `403`

```json title="Exemple de sortida" linenums="1"
"Token invalid, signature verification failed"
```
