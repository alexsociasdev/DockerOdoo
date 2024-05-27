FROM ubuntu:latest

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && apt-get install -y postgresql postgresql-contrib

RUN service postgresql start && \
    su - postgres -c "psql -c \"CREATE USER odoo WITH PASSWORD 'odoo';\"" && \
    su - postgres -c "createdb -O odoo odoodb" && \
    service postgresql stop

COPY start.sh /start.sh

RUN chmod +x /start.sh

CMD ["/start.sh"]
