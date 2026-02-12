# Linux/Mac Commands


### Docker Clean Unsafe

# Uso de disco de docker para antes y después
docker system df
# Borra contenedores detenidos
docker container prune
# Borra imágenes sin uso
docker image prune
# Borra volumen sin uso
docker volume prune
# Borra todo lo sin uso
docker system prune
# Borra volúmenes (peligroso)
docker system prune --volumes




### Docker

# Para iniciar un contenedor
docker compose up -d
# Para detener un contenedor
docker compose down


