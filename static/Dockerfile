#base image
FROM golang as base

#application working directory 
WORKDIR /app

#copy the  go.mod file into the working directory
COPY go.mod .

#download and install application packages
RUN go mod download

#copy the entire source code 
COPY .  .

#command to run the application in the container
RUN go build -0 main .

#Security Implementation
#Final stage using Distroless Image
FROM gcr.io/distroless/base

#copy the binary package 
COPY --from=base /app/main .

#Copy all static files
COPY --from=base /app/static ./static

#Expose the container port
EXPOSE 8080

CMD [ "./main" ]