# Database Setup

The backend uses PostgreSQL through TypeORM. Create the database and configure
the connection values in `backend/.env` (copy `backend/.env.example` first).
The example file contains placeholders only; replace them with local
credentials.

## Local development

For a local PostgreSQL installation, create the application role and database:

```bash
sudo -u postgres createuser --pwprompt smartuser
sudo -u postgres createdb --owner=smartuser smart_restaurant
```

Set `DB_HOST`, `DB_PORT`, `DB_USERNAME`, `DB_PASSWORD`, and `DB_NAME` in
`backend/.env`. The backend enables TypeORM `synchronize` outside production,
which creates and updates tables from the registered entities when it starts.

## Production

Set `NODE_ENV=production`; the backend then disables TypeORM `synchronize`.
The repository does not yet contain TypeORM PostgreSQL migrations. Add and
review versioned migrations before deploying or upgrading a production schema.

## Legacy SQL files

`migrations/001_initial_schema.sql`, `migrations/verify_migration.sql`, and
`seeds/001_initial_data.sql` are historical MySQL scripts for an older schema.
They are not used by the current backend and must not be run against PostgreSQL.
The current local-development schema is defined by the TypeORM entities under
`backend/src`.
