# -Conectar-un-esp32-a-internet-
import network
import time

# Configurar los parámetros de la red Wi-Fi
SSID = 'tu_red_wifi'  # Nombre de la red Wi-Fi
PASSWORD = 'tu_contraseña_wifi'  # Contraseña de la red Wi-Fi

# Crear un objeto de red Wi-Fi
wifi = network.WLAN(network.STA_IF)

# Activar la interfaz Wi-Fi
wifi.active(True)

# Conectar a la red Wi-Fi
print('Conectando a la red Wi-Fi...')
wifi.connect(SSID, PASSWORD)

# Esperar a que se establezca la conexión
timeout = 10  # Tiempo de espera máximo en segundos
start_time = time.time()

while not wifi.isconnected():
    if time.time() - start_time > timeout:
        print('No se pudo conectar a la red Wi-Fi en el tiempo especificado.')
        break
    time.sleep(1)

# Si está conectado, mostrar la dirección IP
if wifi.isconnected():
    print('Conexión exitosa!')
    print('Dirección IP:', wifi.ifconfig()[0])
else:
    print('Error de conexión.')
