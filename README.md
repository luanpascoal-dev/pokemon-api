# Pokémon API

1.  `GET` `/api/id/:pokemon_id`

  Return the entire data entry associated with the given pokemon_id.

  If the Pokemon ID does not exist, return an empty object.

  ----

  Example Request: `GET` `/api/id/24`

  Response:
  ```js
   {
       "id": 23,
       "num": "023",
       "name": "Ekans",
       "img": "http://www.serebii.net/pokemongo/pokemon/023.png",
       "type": [
         "Poison"
       ],
       "height": "2.01 m",
       "weight": "6.9 kg",
       "candy": "Ekans Candy",
       "candy_count": 50,
       "egg": "5 km",
       "spawn_chance": 2.27,
       "avg_spawns": 227,
       "spawn_time": "12:20",
       "multipliers": [
         2.21,
         2.27
       ],
       "weaknesses": [
         "Ground",
         "Psychic"
       ],
       "next_evolution": [{
         "num": "024",
         "name": "Arbok"
       }]
   }
  ```

  Example Request: `GET` `/api/id/1000`

  Response:
  ```
  {}
  ```

2. `GET` `/api/evochain/:pokemon_name`

  Return an array of all the Pokemon in the given Pokemon's evolution chain in alphabetical. Include the given Pokemon in the array.

  If the Pokemon name does not exist, then return an empty array.

  **pokemon_name must be lower case**

  For those not familiar with Pokemon, Pokemon evolve into other Pokemon in its evochain. Think of it as a linked list. The evochain is stored in the JSON under `prev_evolution` and `next_evolution`.

  ----

  Example Request: `GET` `/api/evochain/Starmie`

  Example Response:
  ```js
  ['Starmie', 'Staryu']
  ```

  Example Request: `GET` `/api/evochain/Electabuzz`

  Example Response:
  ```js
  ['Electabuzz']
  ```

  Example Request: `GET` `/api/evochain/Timothy`

  Example Response:
  ```js
  []
  ```

3. `GET` `/api/type/:type`

  Return an array of all Pokemon of the given type in the order they appear in the data object.

  If no Pokemon are of the given type, then return an empty array.

  **pokemon_name must be lower case**

  ---

  Example Request: `GET` `/api/type/Fire`

  Response:
  ```js
  ["Charmander","Charmeleon","Charizard","Vulpix","Ninetales","Growlithe","Arcanine","Ponyta","Rapidash","Magmar","Flareon","Moltres"]
  ```

  Example Request: `GET` `/api/type/Ghost`

  Response:
  ```js
  ["Gastly","Haunter","Gengar"]
  ```

  Example Request: `GET` `/api/type/Allen`

  Response:
  ```js
  []
  ```

4. `GET` `/api/type/:type/heaviest`

  Return an object with the name and weight of the heaviest Pokemon of a given type.

  The weight of a Pokemon can be found under the attribute `weight`
  (Note: there are no ties, so they are not an issue)

  If the given type does not exist, return an empty object.


  ----

  Example Request: `GET` `/api/type/Fire/heaviest`

  Response:
  ```js
  {"name":"Arcanine","weight":155}
  ```

  Example Request: `GET` `/api/type/Water/heaviest`

  Response:
  ```js
  {"name":"Gyarados","weight":235}
  ```

  Example Request: `GET` `/api/type/Rachel/heaviest`

  ```js
  {}
  ```

5. `POST` `/api/weakness/:pokemon_name/add/:weakness_name`

  Adds the given weakness to the `weaknesses` array of a given pokemon.
  If the weakness is already there, you should not add another instance of it.


  Return an object with the name and updated Pokemon weakness array. **Weaknesses should be added to the end of the weaknesses array.**

  If the Pokemon does not exist, return an empty object.

  ----

  Example Request:

  Example Request: `POST` `/api/weakness/Fearow/add/Fire`

  Response:
  ```js
  {"name":"Fearow","weaknesses":["Electric","Rock", "Fire"]}
  ```

  **AND `poke.json` should be updated**

  Example Request: `POST` `/api/weakness/Timothy/add/Fire`

  ```js
  {}
  ```

6. `DELETE` `/api/weakness/:pokemon_name/remove/:weakness_name`

  Removes the given weakness from the `weaknesses` array of a given pokemon.
  If the does not exist, keep the weaknesses array as it is.  


  Return an objecect with the name and updated Pokemon weakness array. Order **Order all all other weaknesses should be maintained.**

  If the Pokemon does not exist, return an empty object.

  ----

  Example Request:

  Example Request: `DELETE` `/api/weakness/Fearow/remove/Rock`

  Response:
  ```js
  {"name":"Fearow","weaknesses":["Electric"]}
  ```

  **AND `poke.json` should be updated**

  Example Request: `DELETE` `/api/weakness/Timothy/remove/Fire`

  ```js
  {}
  ```
## Credits

Credit to https://github.com/Biuni/PokemonGO-Pokedex/ for the `poke.json` file.
