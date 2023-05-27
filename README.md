// A partir de este archivo se va a ejecutar toda la aplicación

//Importamos http
const http = require('http');
const puerto = 3000;
const host = 'localhost';


/**
 * createServer -> Es la funcion que se encarga de crear el servidor
 * 
 * Callback recibe dos objetos:
 * 
 * req (request = solicitud) -> viene desde el cliente
 * 
 * res (response = respuesta) -> viene desde els ervidor
 */

// Configuramos el servidor
const server = http.createServer((req, res) => {
    /**
     * tipo de solicitud = metodo = req.method
     * 
     * url = destino del recurso = req.url
     * 
     * 
     * /usuarios, GET
     * /usuarios, POST
     */

    if (req.method === 'GET' && req.url === '/usuarios' ) {
        // Devolver todos los usuarios que tengo en base de datos

        /**
         * Ejemplo:
         * Si la conexion a la base de datos funciona y obtengo a los usuarios
         * devuelvo 200
         * Si la conexion a la base de datos no funciona devuelvo 500
         */
        res.statusCode = 200;
        res.end('Aqui se enviará la lista de usuarios')
    } else if(req.method === 'POST' && req.url === '/usuarios' ) {
        res.statusCode = 200;
        res.end('Aqui se almacenará un usuario')
    } else {
        res.statusCode = 404;
        res.end('Recurso no encontrado')
    }

})


// Encedemos el servidor
server.listen(puerto, host, () => {
    console.log('Servidor encendido')
})

