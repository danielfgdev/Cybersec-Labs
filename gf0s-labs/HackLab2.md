# HackLab #2  
# Sitio privado y archivo cifrado 🔐 (Forense + Cripto)  
[Link HackLab #2](http://labs.gf0s.com/R2cde2/index.html)

---

## Objetivo:

1.- Acceder a una página web privada. [Link a la página](http://labs.gf0s.com/R2cde2/login)

2.- Descifrar el contenido del archivo secreto.

---

## Analizar una captura de tráfico de red (archivo PCAP)

Descargamos el siguiente [archivo](http://labs.gf0s.com/R2cde2/captura_de_red_reto2.pcap) y lo analizamos con Wireshark (también se puede hacer mediante la web https://apackets.com/)

### Mediante ***Wireshark***:

Abrimos el archivo y filtramos por HTTP.

Veo un paquete que en "Info" dice algo de "login", lo cual me hace sospechar. En el apartado de "Hypertext Transfer Protocol" veo que dice "Authorization: Basic" y una cadena, la cual es algo codificado en base64. Directamente Wireshark nos da las credenciales descodificadas:

![](images/HackLab2/2025-04-21-23-01-31.png)

De todas formas, si probamos en alguna web a descodificar ese código:

![](images/HackLab2/2025-04-21-23-04-26.png)

### Mediante ***apackets.com***

Entramos en la web y subimos el archivo con la captura del tráfico de red. 

Después, a la izquierda, en el apartado de "Credentials", vemos: 

![](images/HackLab2/2025-04-21-23-07-09.png)

Con lo cual, ya tenemos los datos de acceso, vamos a hacer login:  
```Usuario: james Contraseña: 007BOND```

![](images/HackLab2/2025-04-21-23-08-55.png)

---

## Descifrar el contenido

Después de loguearnos, nos aparece que tenemos un archivo txt:

![](images/HackLab2/2025-04-21-23-11-42.png)

El cual contiene unos hashes:

![](images/HackLab2/2025-04-21-23-17-26.png)

```Administrator:B61CCDB6BE3458D0AAD3B435B51404EE:A7B9ECDD64AA492E449E0A619FD16E4B:::```

Podríamos atacar ese hash con algún diccionario o usar fuerza bruta para buscar coincidencias, o probar a buscarlo en [Crackstation.net](https://crackstation.net/).

### Mediante un ataque de diccionario con ***Hashcat***

En la máquina virtual de Kali, meto el hash NTLM en un archivo txt: 

![](images/HackLab2/2025-04-21-23-45-31.png)

Voy a atacarlo con Hashcat usando el diccionario rockyou:

![](images/HackLab2/2025-04-21-23-46-44.png)

![](images/HackLab2/2025-04-21-23-47-54.png)

Para eso uso el comando:  
```hashcat -m 1000 -a 0 hashNTLM.txt /usr/share/wordlists/rockyou.txt.gz```

***hashcat*** , para indicar el programa.

***-m 1000*** , el tipo de hash, 1000 = NTLM, un hash usado por Windows.

***-a 0*** , el modo de ataque, 0 = ataque de diccionario.

***hashNTLM.txt*** , el archivo que contiene el hash a atacar.

Resto, la ruta del diccionario (comprimido en .gz).

Una vez que termina:

![](images/HackLab2/2025-04-21-23-53-44.png)

Nos aparece esta salida:  
```a7b9ecdd64aa492e449e0a619fd16e4b:HACKERS```

Así que la contraseña es:  
```HACKERS```

### Mediante un ataque de diccionario con ***John the Ripper***

Para John the Ripper debemos descomprimir primero el diccionario de rockyou, ya que no lo admite en formato .gz:

![](images/HackLab2/2025-04-22-00-18-44.png)

Y lo ejecutamos con el comando:

```john --format=nt --wordlist=/usr/share/wordlists/rockyou.txt hashNTLM.txt```

***john*** , para indicar el programa.

***--format=nt*** , para especificar el formato, nt es NTLM.

***--wordlist=/usr/share/wordlists/rockyou.txt*** , el diccionario.

***hashNTLM.txt*** , el archivo que contiene el Hash.

![](images/HackLab2/2025-04-22-00-24-39.png)

### Mediante ***Crackstation***

Entramos a Crackstation, copiamos el hash NTLM y le damos a "Crack Hashes":

![](images/HackLab2/2025-04-21-23-30-22.png)

Y ya tenemos la contraseña, al igual que de la otra forma:  
```HACKERS```.

Ya está todo lo que nos pedía el reto.
