# Working with Databases

## Notes

### Stateful Database Containers

- Stateful application have persistent date while stateless applications do not.
- Best practices:
  - Use the `VOLUME` instruction in `Containerfiles`: This avoids using the copy-on-write file system and helps with performance.
  - Mount the data directory to a named volume: Offers more portability than a bind mount since the source directory doesn't need to exist on the host machine.
  - Create a database network: Create a Podman network for isolation since only applications that share the network have access to the databases.

### Import Database Data

- You can load data by using the database client.
- If the db already has a client, run `podman cp <sql_file> <target_db_container>:<container_path>`.

### Export Database Data

- To export the data, you need to do a database dump.
- `podman exec <postgresql_container> pg_dump -Fc <database> -f <backup_dump_name>`

## References

1. [Red Hat Container Registry](https://access.redhat.com/RegistryAuthentication)
2. [Red Hat: PostgreSQL Container](https://github.com/sclorg/postgresql-container)
3. [Red Hat: Mariadb Container](https://github.com/sclorg/mariadb-container)
4. [Red Hat: Mongodb Container](https://github.com/sclorg/mongodb-container)
5. [Red Hat: Redis Container](https://github.com/sclorg/redis-container)
