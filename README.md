# serverAda

// http -> Herramienta que nos permite crear servidores

const http = require('http');
const port = 3000;
const host = 'localhost';

/**
 * solicitud -> de recibir la informacion desde el cliente
 * request
 * 
 * respuesta -> de enviar la informacion hacia el cliente
 * response
 */
const server = http.createServer((req, res) => {
    /**
     * method -> Tipo de peticion (POST, PUT, GET, DELETE)
     * url ----> Al endpoint (la direccion exacta de nuestro recurso)
     */

    if (req.method == 'GET' && req.url == '/users') {
        /**
         * La logica debe encargarse de devolver informacion al usuario
         * informacion de users
         */

         const users = [
            { name: 'Juan', email: 'juan@mail.com' },
            { name: 'Maria', email: 'maria@mail.com' },
            { name: 'Carlos', email: 'carlos@mail.com' },
          ];

          res.statusCode = 200;
          res.end(JSON.stringify(users))
    } else if (req.method == 'POST' && req.url == '/users') {
        /**
         * Reciba informacion y almacenela
         */

        let body = '';
        req.on('data', (chunk) => {
            body += chunk.toString();
        });

        req.on('end', () => {
            const user = JSON.parse(body);
            console.log(`Usuario recibido: ${user.name} - ${user.email}`);
            res.writeHead(200, { 'Content-Type': 'application/json' });
            res.end(JSON.stringify({ message: 'Usuario creado correctamente' }));
        });
    }
})

server.listen(port, host, () => {
    console.log(`Estoy escuchando en ${host} la puerta ${port}`)
})






