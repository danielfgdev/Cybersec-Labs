# Bandit 21

[Link Bandit 21](https://overthewire.org/wargames/bandit/bandit21.html)

---

### Enviar la contraseña del nivel actual a un binario setuid en localhost y recibir la contraseña del siguiente nivel

```There is a setuid binary in the homedirectory that does the following: it makes a connection to localhost on the port you specify as a commandline argument. It then reads a line of text from the connection and compares it to the password in the previous level (bandit20). If the password is correct, it will transmit the password for the next level (bandit21).```

Conectarse para hacer el reto:  
```ssh bandit20@bandit.labs.overthewire.org -p 2220```

La contraseña es ```0qXahG8ZjOVMN9Ghs7iOWsCfZyXOUbYO```

Este nivel se trata de utilizar un binario setuid que, al ejecutarlo con un puerto en localhost, acepta la contraseña de bandit20 y, si es correcta, devuelve la contraseña de bandit21.

Lo primero que voy a hacer es abrir dos terminales y conectarme en ambas al reto:

![](images/Bandit21/2025-07-06-01-59-41.png)

En primer lugar usaré ***ls -l*** para confirmar que el binario que busco está donde debe:

```ls -l```

![](images/Bandit21/2025-07-06-02-00-14.png)

En una de las terminales, en la primera por ejemplo, uso el comando:

```nc -lvp 4444```

![](images/Bandit21/2025-07-06-02-02-50.png)

Lo que hace ese comando es poner netcat a escuchar en el puerto 4444:

***nc*** , es la herramienta netcat.

***-l*** , listen, pone a netcat a escuchar (modo servidor).

***v*** , modo verbose, da mensajes detallados.

***p 4444*** , indica el puerto en el que nc debe escuchar.

Ahora, en la otra terminal, la segunda, usamos el comando:

```./suconnect 4444```

![](images/Bandit21/2025-07-06-02-08-07.png)

***./suconnect*** , ejecuta el binario llamado suconnect que está en el directorio actual.

***4444*** , representa el número de puerto al que el binario se debe conectar en localhost.

El comando ejecuta el binario suconnect que está en el directorio actual y le indica que se conecte al puerto 4444 en localhost.

Una vez ejecutado ese comando, en la primera terminal nos muestra que recibió la conexión:

![](images/Bandit21/2025-07-06-02-11-20.png)

Ahora, en la primera terminal, pegamos la misma contraseña que usamos para conectarnos a este reto y se la enviamos:

![](images/Bandit21/2025-07-06-02-13-09.png)

A su vez, en la segunda terminal nos muestra:

![](images/Bandit21/2025-07-06-02-13-34.png)

Y en la primera terminal, ya tengo la contraseña para el siguiente nivel:

![](images/Bandit21/2025-07-06-02-14-16.png)

---

**Contraseña: ```EeoULMCra2q0dSkYj561DX7s1CpBuOBt```**