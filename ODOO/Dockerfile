FROM python:3.8-slim

ENV DEBIAN_FRONTEND=noninteractive \
    PYTHONUNBUFFERED=1

RUN apt-get update && apt-get install -y --no-install-recommends \
    git \
    gcc \
    g++ \
    libc6-dev \
    libldap2-dev \
    libsasl2-dev \
    && rm -rf /var/lib/apt/lists/*

RUN git clone --depth 1 --branch 15.0 https://www.github.com/odoo/odoo.git /odoo

WORKDIR /odoo

COPY requirements.txt ./requirements.txt

RUN pip install psycopg2-binary && \
    pip install --no-cache-dir -r requirements.txt

RUN echo "[options]\n" > /odoo/odoo.conf && \
    echo "db_host = db\n" >> /odoo/odoo.conf && \
    echo "db_port = 5432\n" >> /odoo/odoo.conf && \
    echo "db_user = odoo\n" >> /odoo/odoo.conf && \
    echo "db_password = odoo\n" >> /odoo/odoo.conf && \
    echo "addons_path = /odoo/odoo/addons,/odoo/addons" >> /odoo/odoo.conf

EXPOSE 8069

CMD ["sh", "-c", "exec /odoo/odoo-bin -c /odoo/odoo.conf -d odoodb -i base --db-filter=^odoodb$ --load-language=en_US"]
