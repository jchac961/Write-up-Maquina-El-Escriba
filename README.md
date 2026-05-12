# Write-up-Maquina-El-Escriba
Maquina de la plataforma www.whoami-labs.com

Lo primero es iniciar la maquina vulnerable

<img width="1901" height="1130" alt="Captura de pantalla 2026-05-09 215138" src="https://github.com/user-attachments/assets/d9eb68f7-0424-4662-914c-4460f28ecab6" />

# RECONOMIENTO

Una vez iniciada la maquina vulnerable hice un escaneo de puertos utilizando la herramienta nmap, para verificar que puertos contaba la maquina abiertos, los servicios que corren en los mismos con sus respectivas versiones, para de esta manera poder saber si existia alguno vuonerable

<img width="1901" height="1130" alt="Captura de pantalla 2026-05-09 215151" src="https://github.com/user-attachments/assets/ecec189f-76be-4c2c-9936-08b312526934" />

Ya sabiendo que en esta maquina teniamos los puertos #22 y el puerto #80 procedi a verificar en un navegador a ver que información estaba manejando el servicio http que estaba corriendo en el puerto #80

<img width="1901" height="1130" alt="Captura de pantalla 2026-05-09 215210" src="https://github.com/user-attachments/assets/eb64def9-0d7e-431e-bf72-4bf398912599" />

Luego de esto por regla general procedi a verificar el codigo de la pagina a ver si encontraba algo importante o que me ayudra con la explltación de la maquina, y en efecto encontre información muy importante

<img width="1901" height="1130" alt="Captura de pantalla 2026-05-09 221534" src="https://github.com/user-attachments/assets/a0d54f88-3a7f-44a0-9dff-6905f11859b5" />

<img width="1901" height="1130" alt="Captura de pantalla 2026-05-09 221556" src="https://github.com/user-attachments/assets/1714d52c-303a-454a-b33e-1be58de6a099" />

Como podemos observar en la imgenes anteriores en la primera captura vemos que hay un mensaje que nos dice "INTERNAL API CONFIGURATION-DO NOT MODIFI" TODO: Move these variables to a secure vault before the Q4 audit"; asi como tambien en la segunda captura se encuentran unas credenciales codificadas claramente en base64, y  algunos metadatos del sistema que claramente no deben encontrarse ahi; "node_id ("ND-992-XC") y la versión de la API (2.4.1)"

Teniendo estas credenciales me diriji a decodificar el contenido y obtuve en texto plano las credenciales, que posteriormente utilizare

<img width="1901" height="1130" alt="Captura de pantalla 2026-05-09 222052" src="https://github.com/user-attachments/assets/40c3b914-d2fe-4833-8ba7-8cfd85b4ef6b" />

# EXPLOTACIÓN

Ya teniendo las credenciales procedi a utilizarlas para ingresar a la maquina utilizando el servicio ssh, y obtuve acceso

<img width="1901" height="864" alt="Captura de pantalla 2026-05-09 222210" src="https://github.com/user-attachments/assets/12dcd158-6333-4263-8b35-54f6b69a842c" />

Encontre la flag de usuario

<img width="1901" height="1130" alt="Captura de pantalla 2026-05-09 222228" src="https://github.com/user-attachments/assets/52d29333-98e0-424b-ad85-8e814ea584c9" />

<img width="1901" height="1130" alt="Captura de pantalla 2026-05-09 222254" src="https://github.com/user-attachments/assets/0d5d8038-0504-4069-aa7b-94e68f66fd16" />

# ESCALADA DE PRIVILEGIOS

Como ya teniamos el spoiler de las posibles vulnerabilidades con la que contaban estos laboratorios intente primero buscar algunos cronjob, pero no tuve nada positivo

<img width="1901" height="1130" alt="Captura de pantalla 2026-05-09 222456" src="https://github.com/user-attachments/assets/997d9261-0093-4aed-99d6-ebe8e5f40da8" />

Luego pase a buscar si habia alguna capability activa y en efecto encontre una

<img width="1901" height="1130" alt="Captura de pantalla 2026-05-09 222740" src="https://github.com/user-attachments/assets/872b90c7-6c98-481f-ac0a-da308848da0c" />

Ingrese a este archivo para tratar de modificarlo, que aqui lo que hice fue eliminar la x el usuario root, esta x se encarga de decirle al sistema que mantenga la contraseña hasheada, y al eliminarla lo que hacemos es decirle al sistemma que no puede ingresar sin contraseña

<img width="1901" height="1130" alt="Captura de pantalla 2026-05-09 222922" src="https://github.com/user-attachments/assets/7aead156-6af8-49eb-a883-fc9250f61e61" />

<img width="1901" height="1130" alt="Captura de pantalla 2026-05-09 222931" src="https://github.com/user-attachments/assets/935979ff-cadb-411a-b9a7-40e020d8f345" />

Ya habiendo hecho esto procedi a intentar ingresar haciendo un su root, y obtuve la escalada de privilegios, ya luego de esto dirigirme a la carpeta o directorio donde s encontraba la flag

<img width="1901" height="1130" alt="Captura de pantalla 2026-05-09 231513" src="https://github.com/user-attachments/assets/5b8abf20-811e-4d8e-9150-50b1452830df" />

# RESULTADOS


<img width="1901" height="1130" alt="Captura de pantalla 2026-05-09 231531" src="https://github.com/user-attachments/assets/ce97d1d1-d4e4-455b-b692-be0367e844be" />

# MAQUINA POWNED

<img width="1901" height="1130" alt="Captura de pantalla 2026-05-09 223151" src="https://github.com/user-attachments/assets/a18aee10-79d9-4f5d-a001-3cef86202113" />
