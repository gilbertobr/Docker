# Elixir Phoenix 1.4.9 Docker

Criar Docker

```
docker build -t app/elixir-phoenix .
```

Executar Docker

```
docker run --name elixir-phoenix --privileged -ti -p 22222:22 -p 80:80 -p 443:443 -p 3306:3306 -p 5432:5432 -p 4000:4000 -d app/elixir-phoenix
```

Iniciar shell

```
docker exec -i -t elixir-phoenix /bin/bash
```

## Estudos

 * https://docs.docker.com/
 * https://elixirschool.com/pt/
