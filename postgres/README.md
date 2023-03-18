# Installing Postgres
```
brew install postgres
```
# Starting Postgres
```
brew services start postgres
```
# Stopping Postgres
```
brew services stop postgres
```
# Creating a database
```
createdb <database_name>
```
# Creating a user
```
createuser <user_name>
```
# Start Shell
```
psql postgres
```
# Listing users
```
\du list users
```
# Listing databases
```
\l list databases
```
# Connecting to a database
```
\c <database_name>
```
# Listing tables
```
\dt list tables
```
# Listing columns
```
\d <table_name>
```
## Note: if not configures, default user is the name of `system user` and password is `none` - database name: `postgres`
