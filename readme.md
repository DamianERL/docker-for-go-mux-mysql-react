
# STEP for golang-gorilla/mux

structure folder

```
	|--client
	|	-Dockerfile
	|	-etc
	|--server
	|	-Dockerfile
	|	-go.mod
	|	-go.sum
	|	-main.go
	|--database
	|	-docker-compose.yaml
```



## make hello world

1. Initializing project

```bash
go mod init appsname
```

2. Install gorilla/mux

```bash
go get -u github.com/gorilla/mux
```
3. Create main.go file and write this below code to print 'Hello wolrd'

```go

package main

import (
	"fmt"
	"net/http"
	"github.com/gorilla/mux"
)

func main() {

	// On Terminal/Command Propt
  fmt.Println("Hello World!")

	// On http (API)
	r := mux.NewRouter()

	r.HandleFunc("/", func (w http.ResponseWriter, r *http.Request){
		w.Header().Set("Content-Type", "application/json")
		w.WriteHeader(http.StatusOK)
		w.Write([]byte("Hello World"))
	}).Methods("GET")

	fmt.Println("server running localhost:5000")
	http.ListenAndServe("localhost:5000", r)
}

```


3. Create Dockerfile and write this below code

```yaml

FROM golang:1.19.2-alpine
WORKDIR /app
COPY . /app
RUN go get -d github.com/gorilla/mux
RUN go build -v /app
CMD ["go", "run", "main.go"]


```


## make mysql for docker

1. Create folder database

2. Create docker-compose.yaml and write this below code

```yaml

version: '3.3'
services:
  mysql:
    container_name: mysql-8
    image: mysql:8.0.32-debian
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: 'mysqlpassword'
    ports:
      # <Port exposed> : < MySQL Port running inside container>
      - '3333:3306'
    expose:
      # Opens port 3306 on the container
      - '3306'
      # Where our data will be persisted
    volumes:
      - my-db:/var/lib/mysql
    networks:
      - mysql-8
    #restart: always

# Names our volume
volumes:
  my-db:

networks:
  mysql-8:
    external: true


```

## make react for docker



```yaml

FROM node:15.13-alpine
WORKDIR  /app
COPY . /app
RUN npm install
RUN npm run build
CMD ["npm", "start"]





```





