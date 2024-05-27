FROM python:3.8-slim

ENV DEBIAN_FRONTEND=noninteractive \
    PYTHONUNBUFFERED=1

RUN apt-get update && apt-get install -y --no-install-recommends \
git \
gcc \
g++ \
libc6-dev \
libldap2-dev \
libsasl2-dev 

RUN git clone --depth 1 --branch 15.0 https://www.github.com/odoo/odoo.git /odoo

WORKDIR /odoo

COPY requirements.txt ./requirements.txt

RUN pip install psycopg2-binary

RUN pip install --no-cache-dir -r requirements.txt

COPY odoo.config /odoo/
COPY start.sh /start.sh
RUN chmod +x /start.sh

CMD ["/start.sh"]
