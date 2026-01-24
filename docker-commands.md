# Linux/Mac Commands


### Docker Clean Unsafe
```
docker system df                  # Uso de disco de docker para antes y después
docker container prune            # Borra contenedores detenidos
docker image prune                # Borra imágenes sin uso
docker volume prune               # Borra volumen sin uso
docker system prune               # Borra todo lo sin uso
docker system prune --volumes     # Borra volúmenes (peligroso)
```

---

### Docker
```
docker compose up -d              # Para iniciar un contenedor
docker compose down               # Para detener un contenedor
```

---