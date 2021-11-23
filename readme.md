# Intro

## debezium-with-oracle-jdbc
I uploaded all the public information found on the debezium download sites to reproduce this issue in an easy way. This is not my intellectual property! The problem is that I had to deviate from the original documentation.

Please make sure to download the oracle client under debezium-with-oracle-jdbc/oracle_instantclient for the ojdbc8.jar.

## Database Config
The database has to have the LOG_MODE=ARCHIVELOG activated.
Otherwise, you get the following error: The Oracle server is not configured to use a archive log LOG_MODE, which is required for this connector to work properly. Change the Oracle configuration to use a LOG_MODE=ARCHIVELOG and restart the connector.

Details to activate are here: https://www.oracle.com/ocom/groups/public/@otn/documents/webcontent/283263.htm

## Start
```
# Set the Version for the docker tags
export DEBEZIUM_VERSION=1.7

# Start the services
docker-compose -f docker-compose.yml up --build

#Create a new connector for the oracle database
curl -i -X POST -H "Accept:application/json" -H  "Content-Type:application/json" http://localhost:8083/connectors/ -d @register-oracle-logminer.json
```