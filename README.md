# Odoo Example

####
### Local Testing with Docker

**Build**
```sh
docker build -t klovercloud/odoo:13.0 .
```

**Run Postgres**
```sh
docker run -d -e POSTGRES_USER=odoo -e POSTGRES_PASSWORD=odoo -e POSTGRES_DB=postgres --name db postgres:10
```

**Run Odoo**
```sh
docker run -d -p 8069:8069 --name odoo --link db:db -e HOST=db -e USER=odoo -e PASSWORD=odoo --read-only --tmpfs=/tmp -v /vol/odoo/data:/var/lib/odoo klovercloud/odoo:13.0
```

####
### Run in KloverCloud
**Database**
- Create a Postgres Server with a PgAdmin
- Connect to your Postgres Server via PgAdmin and create a user for odoo having the priviledge to create databases
- Do not create any database for odoo
####
**Application**
- Fork this GitHub repository
- Update the odoo.conf file based on your needs
- Upload your extra addons inside the addons directory
- Do Git Commit & Push
- On-board your forked repository as Application
- Set Application Port to `8069`
- Assign minimum 1vCPU and 2.75GB RAM
- Persistent Volume is required (Min 10 GB)
- The following paths should be in the Volume Mount paths
```
/var/lib/odoo
```
- Create Application
- Set Environment Variables / Secrets to provide configurations for PostgreSQL
```
HOST=<YOUR_POSTGRES_ENDPOINT>
USER=<YOUR_POSTGRES_ODOO_USERNAME>
PASSWORD=<YOUR_POSTGRES_ODOO_PASSWORD>
```
- Deploy Odoo
