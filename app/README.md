# App & MySQL Stack

## Getting Started

Start: `docker-compose up -d`
Stop: `docker-compose down`

Use DB
`docker exec -it <container_id> mysql -p todos`
>>>    msql> <exec commands>

### Logs

app: `docker-compose logs -f app`

mysql: `docker-compose logs -f mysql`
