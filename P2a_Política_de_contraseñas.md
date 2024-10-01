# Política de contraseñas

## Contexto
Por defecto, la mayoría de sistemas operativos, vienene con una política de contraseña muy laxa, una contraseña segura presenta una barrera más al atacante, que en su intento de acceder al sistema, indudablemete dejará más rastro y en algunos casos a provocar el abandondo de ataque.

## Objetivos
* Entender el sistema de contraseñas del sistema operativo linux
* Entender el PAM (Plugable authentication Module)
* Instalar y configurar la libreria _pwquality_
* Comprobar y verificar que se ha llevado la práctica de forma correcta
* Documentar la práctica.

# RESOLUCION

* Encontramos las contraseñas de linux en el archivo __/etc/shadow__, ahi encontraremos las contraseñas de los usuarios. Linux utiliza un algoritmo __hash__ para convertir la contraseña de texto en una cadena de caracteres de longitud fija que se llama _hash_.

* __PAM__ es para autenticar usuarios locales y remotos, el usuaria proporciona un token la cual normalmente es una contraseña

> Instalacion y configuracion de la libreria __pwquality__

* Primero instalamos con el siguiente comando:

```bash
sudo apt-get install libpam-pwquality
```

Ahora necesitamos encontrar el siguiente archivo __"pwquality.conf"__ en la siguiente ruta.

```bash
cd /etc/security/
```

Nos pidieron:

* Politica debil (min 6*)
* Politica media (min 8, [0-9], [A-Z], *)
* Politica extrema (min 12, [0-9][A-Z], [], [#$%&...])

Modificamos el archivo de configuracion:

```bash
# Política mínima (débil)
minlen = 6
# Requiere al menos 1 símbolo
minclass = 1

# Política media
minlen = 8
# Requiere al menos 1 número, 1 letra mayúscula y 1 símbolo
minclass = 3
ucredit = -1
lcredit = -1
ocredit = -1

# Política extrema
minlen = 12
# Requiere al menos 1 número, 1 letra mayúscula, 1 símbolo y otros caracteres especiales
minclass = 4

#Aqui uso minClass, ya que abarca (mayusculas, minusculas, digitos y no alfa)
```

### Politica minima comprobacion:

Comando de comprobacion:

```bash
pwscore | cambio+
```
Resultado:
```bash

```

### Politica media comprobacion:

Comando de comprobacion:

```bash
pwscore | C4mbios*
```
Resultado:

```bash

```


### Politica extrema comprobacion:

Comando de comprobacion:

```bash
pwscore | Cambioseguri
```
Resultado:

```bash

```

|         |Score    |l.min|Requisitos  |Ejemplos    |
|---------|---------|-----|------------|------------|
|No valido|   <40   |  -  |minlen:8    |Procavsion  |
|         |         |     |            |            |
|Debil    | 35 - 50 |  6  |minlen:6    |P#k.5n      |
|         |         |     |ucredit:-1  |            |
|         |         |     |minclass:-1 |            |
|         |         |     |lcredit:-1  |            |
|         |         |     |            |            |
|Media    | 50 - 80 |  8  |minlen: 8   |Comproar2   |
|         |         |     |ucredit:1   |            |
|         |         |     |minclass:1  |            |
|         |         |     |lcredit:1   |            |
|         |         |     |            |            |
|Extrema  |   >80   |  12 |minlen:12   |Comprasion1`|
|         |         |     |ucredit:-1  |            |
|         |         |     |minclass:-1 |            |
|         |         |     |lcredit:-1  |            |
