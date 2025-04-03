# Endpoints Admin

Aquí es mostrarà informació dels endpoints creats pels usuaris Administradors i el resultat de la seva petició.

!!! warning "Atenció"

    Totes les sol·licituds a l'API es faran a l'URL del servidor:

    http://elrefugidelbongust.daw.institutmontilivi.cat + /API + l'end point desitjat.

!!! info "Tots els tokens enviats han de ser d'administrador perquè la petició retorni dades"

!!! question "Com fem les crides a la API?"

    En els nostres exemples mostrarem les crides des de JavaScript amb la biblioteca d'<a href="https://axios-http.com/" target="_blank">axios</a>.

## **/eliminarComanda (DELETE)**

### _Crida_

És necessari enviar el token d'identificació per header.

És necessari enviar l'id de comanda.

### _Respostes_

Rebras

## **/comandesAdmin (GET)**

### _Crida_

És necessari enviar el token d'identificació per header.

### _Respostes_

Rebras

## **/deletePlat (PUT)**

### _Crida_

??? note "Informació"
    Realment no esborra el plat, sinó que canvia la propietat `disponible` de `true` a `false`

És necessari enviar el token d'identificació per header.

És necessari enviar l'id del plat a esborrar.

### _Respostes_

Rebras

## **/habilitarPlat (PUT)**

### _Crida_

És necessari enviar el token d'identificació per header.

És necessari enviar l'id del plat a activar.

### _Respostes_

Rebras

## **/updatePlat (PUT)**

### _Crida_

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

### _Respostes_

Rebras

## **/deleteDiaPlat (PUT)**

### _Crida_

És necessari enviar el token d'identificació per header.

És necessari enviar per body l'id del plat sobre el qual es vol actuar.

### _Respostes_

Rebras

## **/insertDiaPlat (PUT)**

### _Crida_

És necessari enviar el token d'identificació per header.

És necessari enviar per body l'id del plat sobre el qual es vol actuar i els dies que es vol posar el plat.

### _Respostes_

Rebras

## **/nouPlat (PUT)**

### _Crida_

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
axios
	.put(
		"/API/nouPlat",
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
		}
	)
	.then((res) => {
		//tractar resposta
	})
	.catch((err) => {
		//tractar errors
	});
```

### _Respostes_

- Si es fa una sol·licitud correcta rebrà un `string` amb codi `200`

```json title="Exemple sortida" linenums="1"
"Plat afegit"
```

- Si es fa una sol·licitud amb un **token invàlid** rebrà un `string` amb codi `401`

```json title="Exemple sortida" linenums="1"
"Token invalid Signature verification failed"
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

### _Crida_

És necessari enviar el token d'identificació per header.

```js title="Exemple crida" linenums="1"
axios
	.get("/API/platsTots", {
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

### _Respostes_

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
"Token invalid Signature verification failed"
```

## **/admin (GET)**

### _Crida_

És necessari enviar el token d'identificació.

```js title="Exemple crida" linenums="1" hl_lines="3"
axios
	.get("/API/admin", {
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

### _Respostes_

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
