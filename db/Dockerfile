FROM ubuntu:latest

ENV DEBIAN_FRONTEND=noninteractive

# Instala PostgreSQL y elimina las listas de paquetes para reducir el tamaño de la imagen
RUN apt-get update && apt-get install -y postgresql postgresql-contrib && rm -rf /var/lib/apt/lists/*

# Inicializa la base de datos y crea el usuario y la base de datos
RUN service postgresql start && \
    su - postgres -c "psql -c \"CREATE USER odoo WITH PASSWORD 'odoo';\"" && \
    su - postgres -c "createdb -O odoo odoodb" && \
    service postgresql stop

# Encuentra el directorio correcto de configuración de PostgreSQL y modifica los archivos de configuración
RUN config_dir=$(find /etc/postgresql/ -type d -name main) && \
    echo "listen_addresses='*'" >> ${config_dir}/postgresql.conf && \
    echo "host all all 0.0.0.0/0 md5" >> ${config_dir}/pg_hba.conf

# Expone el puerto 5432
EXPOSE 5432

# Comando para iniciar PostgreSQL y mantener el contenedor en ejecución
CMD ["sh", "-c", "service postgresql start && tail -f /dev/null"]
