FROM ubuntu:latest

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && apt-get install -y postgresql postgresql-contrib && rm -rf /var/lib/apt/lists/*

RUN service postgresql start && \
    su - postgres -c "psql -c \"CREATE USER odoo WITH PASSWORD 'odoo';\"" && \
    su - postgres -c "createdb -O odoo odoodb" && \
    service postgresql stop

RUN config_dir=$(find /etc/postgresql/ -type d -name main) && \
    echo "listen_addresses='*'" >> ${config_dir}/postgresql.conf && \
    echo "host all 0.0.0.0/0 md5" >> ${config_dir}/pg_hba.conf

EXPOSE 5432

CMD ["sh", "-c", "service postgresql start && tail -f /dev/null"]
