# Installing Hasura on Docker

## Start services via docker-compose

```
docker-compose up
```

You should see a lot of log output. The containers should now be running.

## Open Hasura Console

Head to [Hasura Console](http://localhost:8080/console) to open the Hasura console.

## Create Table in Posgres

Click the 'Data' tab at the top and press 'Add Table' button. Create the table with the following structure:

```
profile (
  id INT PRIMARY KEY,
  name TEXT
)
```

Make sure to set `id` column as the Primary Key and click save button.

### Sanity check in Postgres DB

Head to [pgAdmin Console](http://localhost:5050/) to open the pgAdmin console.

Connect to the database. The details are in the [docker-compose file](./docker-compose.yml). Assuming this file has not changed the required connection details are:

* Server: postgres
* Port: 5432
* Database: postgres
* Password: @postgres

Navigate to the table that we have just created by expanding the left navigation tree as follows: **servers -> postgres-hasura -> databases -> postgres -> schemas -> public -> Tables -> profile -> columns**. You should see the colums *id* and *name*.

## Insert Data into Table

Now right click on the table name and select from the context menu 'View/Edit Data -> All Rows'. The results should show an empty table. Now add two rows to that table and save the data.

Note it is also possible to insert data via the Hasura Dashboard.

## View the data in Hasura

Flip back to the [Hasura Console](http://localhost:8080/console) and click on *GraphQL* tab. Now run the following query:

```
query {
  profile {
    id
    name
  }
}
```

You will see the results from the database displayed!

### Conclusion

With this tutorial you have installed Postgres, Hasura and pgAdmin. You have created a single table with two columns. You have inserted data into this table using pgAdmin and you have queried the database table via Hasura Graph QL engine.