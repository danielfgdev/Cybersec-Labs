# Bandit 28

[Link Bandit 28](https://overthewire.org/wargames/bandit/bandit28.html)

---

### Clonar el repositorio git accesible por SSH y extraer la contraseña del siguiente nivel

```There is a git repository at ssh://bandit27-git@localhost/home/bandit27-git/repo via the port 2220. The password for the user bandit27-git is the same as for the user bandit27. Clone the repository and find the password for the next level.```

Conectarse para hacer el reto:  
```ssh bandit27@bandit.labs.overthewire.org -p 2220```

La contraseña es ```upsNCc7vzaRDx6oZC6GiR6ERwe1MowGB```

En primer lugar, me cambiaré a ***/tmp*** y crearé un directorio allí, ya que es el único sitio donde tengo permisos para guardar archivos.

```cd /tmp```

![](images/Bandit28/2025-08-11-22-58-06.png)

Usaré ***mkdir*** para crear el directorio y ***cd*** para cambiarme a ese directorio.

```mkdir bandit28_1```

```cd bandit28_1```

![](images/Bandit28/2025-08-11-23-06-40.png)

Ahora voy a clonar el repositorio. Para ello usaré ***git clone*** y el SSH que me dan en el enunciado del reto:

```git clone ssh://bandit27-git@localhost:2220/home/bandit27-git/repo```

![](images/Bandit28/2025-08-11-23-09-38.png)

Ahora me pide una contraseña. Ponemos la misma que usamos para conectarnos a este reto (es lo que me indica en el enunciado):

```upsNCc7vzaRDx6oZC6GiR6ERwe1MowGB```

![](images/Bandit28/2025-08-11-23-12-02.png)

En este momento ya tendría clonado el repositorio. Ahora voy a mirar qué me encuentro en el repositorio:

```ls -l```

![](images/Bandit28/2025-08-11-23-14-02.png)

Voy a cambiarme al directorio ***repo***, que es lo que muestra que tengo, y después voy a hacer un ***ls*** para ver qué contiene:

```cd repo```

```ls```

![](images/Bandit28/2025-08-11-23-15-57.png)

Veo que me aparece que hay un ***README***. Voy a mirar qué contiene:

```cat README```

![](images/Bandit28/2025-08-11-23-18-37.png)

Eso me devuelve la contraseña para el siguiente nivel:

![](images/Bandit28/2025-08-11-23-20-31.png)

---

**Contraseña: ```Yz9IpL0sBcCeuG7m9uQFt8ZNpS4HZRcN```**