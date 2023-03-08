FROM golang:1.19.2-alpine
WORKDIR /app
COPY . /app
RUN go get -d github.com/gorilla/mux
RUN go build -v /app
CMD ["go", "run", "main.go"]
