FROM postgres:latest
USER postgres

# Copy postgres config file into container
COPY ./postgresql.conf /etc/postgresql

# Override default postgres config file
CMD ["postgres", "-c", "config_file=/etc/postgresql/postgresql.conf"]