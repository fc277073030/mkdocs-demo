# 安装 jira-servicedesk 
## docker-compose部署
```docker
version: '3'

services:
  jira:
    depends_on:
      - postgresql
    image: fc277073030/jira-servicedesk:v1
    networks:
      - jiranet
    volumes:
      - jiradata:/var/atlassian/jira
    ports:
      - '8080:8080'
    environment:
      - 'JIRA_DATABASE_URL=postgresql://jira@postgresql/jiradb'
      - 'JIRA_DB_PASSWORD=123456'
      - 'SETENV_JVM_MINIMUM_MEMORY=2048m'
      - 'SETENV_JVM_MAXIMUM_MEMORY=4096m'
      - 'JIRA_PROXY_NAME='
      - 'JIRA_PROXY_PORT='
      - 'JIRA_PROXY_SCHEME='
    logging:
      # limit logs retained on host to 25MB
      driver: "json-file"
      options:
        max-size: "500k"
        max-file: "50"

  postgresql:
    image: postgres:13.0-alpine
    networks:
      - jiranet
    volumes:
      - postgresqldata:/var/lib/postgresql/data
    environment:
      - 'POSTGRES_USER=jira'
      # CHANGE THE PASSWORD!
      - 'POSTGRES_PASSWORD=123456'
      - 'POSTGRES_DB=jiradb'
      - 'POSTGRES_ENCODING=UNICODE'
      - 'POSTGRES_COLLATE=C'
      - 'POSTGRES_COLLATE_TYPE=C'
    logging:
      # limit logs retained on host to 25MB
      driver: "json-file"
      options:
        max-size: "500k"
        max-file: "50"

volumes:
  jiradata:
    external: false
  postgresqldata:
    external: false

networks:
  jiranet:
    driver: bridge
```

```bash
docker-compose up -d 
```