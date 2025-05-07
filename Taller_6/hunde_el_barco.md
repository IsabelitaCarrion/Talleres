# API de un sistema del juego Hunde la Flota
El objetivo del ejercicio es diseñar una API REST que será implementada (en otros ejercicios) por un microservicio o aplicación que se encargará de tratar todos los datos de las diferentes partidas. En este ejercicio nos centraremos únicamente en el diseño de la API y no trataremos ningún detalle de la implementación.

Las operaciones que la API debe soportar son las siguientes:
Crear una partida.
Eliminar una partida.
Modificar datos de una partida.
Iniciar una partida.
Finalizar una partida.
Consultar todos los datos (jugadores asociados, barcos de cada jugador, disparos realizados, ganador...) de una partida.
Añadir un barco a la cuadrícula de un jugador en una partida.
Eliminar un barco de la cuadrícula de un jugador en una partida.
Consultar todos los barcos de un jugador de una partida.
Registrar un disparo de un jugador a otro en una partida.
Crear un usuario.
Obtener datos de un usuario.
Eliminar un usuario.
Ten en cuenta que podría no ser necesario definir un endpoint por cada una de las operaciones que se han listado. No obstante, dichas operaciones deben ser satisfechas por la API diseñada. Las primeras preguntas que deberás hacerte son:

¿Qué recursos tiene que manejar la API?
¿Cómo se relacionan entre sí?
¿Qué información (atributos) guarda cada recurso?
# Recursos
    Partida (partidas): Recurso que permitira ser creado, modificado y eliminado. Cuenta con un estado que inicia o finaliza. 
    Barco (barcos): Recurso que permite tener los datos de los barcos. 
    Tablero (tableros): Recurso que registra los disparos en la partida.
    Disparo (disparos): Recurso que registra los disparos realizados por el jugador.
    Usuario (usuarios): Recurso que permite la gestion de los usarios. 

# Atributos
    Partida: ID, jugador1, jugador2, estado (iniciado, finalizado)
    Barco: ID, coordenadas, tipo, tableroID
    Tablero: ID, partidaID, usuarioID, 
    Disparo: ID, Coordenada, estado (agua, tocado, hundido)
    Usuario: ID, nomhre, correo 

# Relaciones
    Una partida se crea con jugadores
    Cada jugardor tendra un tablero.
    Cada jugador puede añadir barcos a su tablero.
    Cada jugador registra los disparos en el tablero segun coordenadas.
    Cada usuario sea registrado o anonimo puede iniciar una partida.

| Método Http | Endpoint            | Query Params             | Cuerpo JSON de la petición     | Respuesta JSON de la petición                              | Códigos HTTP de respuesta posibles       |
|-------------|---------------------|--------------------------|--------------------------------|------------------------------------------------------------|----------------------------------------------------|
| POST        | /partidas          | Ninguno                  | `{"jugador1ID":"integer","jugador2ID" :"integer"}`     |  `{"id": "integer",jugadorID1":"integer","jugadorID2":"integer"}`                    | 201 Created, 400 Bad Request            |    
| PATCH      | /partidas/{partidaID}          | Ninguno                  | `{"estado":"string"}`     |  `{"id": "integer","jugadorID1":"integer","jugador2ID":"integer","estado": "string"}`                    | 200 OK, 404 Not Found              |    
| DELETE     | /partidas/{partidaID}          | Ninguno                  |        |             | 200 OK, 404 Not Found              |    
| GET       | /partidas/{partidaID}          | Ninguno                  |      |  `{"id": "integer",jugador1ID":"integer","jugador2ID":"integer","ganador":"integer", "barcos":"array","disparos": "array"}`            | 200 OK, 404 Not Found              |    
| POST        | /partidas/{partidaID}/tableros    | Ninguno                  | `{"jugadorID":"integer"}`     |  `{"id": "integer", "partidaID":"integer","jugadorID":"integer"}`                    | 201 Created, 400 Bad Request              | 
| POST        | /partidas/{partidaID}/tableros{tableroID}/barcos   | Ninguno                  | `{"tipo":"string","coordenadas":"["x":"integer", "y":"ïnteger"] "}`     |  `{"id": "integer", "coordenadas":"array", "tipo":"strig"}`            | 201 Created, 400 Bad Request              |    
| DELETE        | /partidas/{partidaID}/tableros{tableroID}/barcos{barcoID}   | Ninguno                  | ` |                     | 200 OK, 404 Not Found     |    
| GET       | /partidas/{partidaID}/tableros{tableroID}/barcos          | Ninguno                  |      |  `{"id": "integer",jugadorID":"integer", "barcos":"array"}`            | 200 OK, 404 Not Found              |   
| POST        | /partidas/{partidaID}/disparos  | Ninguno                  | `{"jugadorID":"integer","coordenadas":"["x":"integer", "y":"ïnteger"] "}`     |  `{"disparoID": "integer", "resultado":"string"}`               | 201 Created, 400 Bad Request              |    
| POST        | /usuarios          | Ninguno                   | `{"nombre":"string","correo":"string"}`     |  `{"iduser": "integer","nombre":"string","correo":"string"}`                    | 201 Created, 400 Bad Request              |    
| GET       | /usuarios/{usuarioID} | Ninguno                  |     | `{"iduser":"integer", "nombre":"string","correo":"string"}`        | 200 OK, 404 NO Found              |    
| DELETE      | /usuarios/{usuarioID}      | Ninguno             |                                                                         |     | 200 OK,404 Not Found              |    