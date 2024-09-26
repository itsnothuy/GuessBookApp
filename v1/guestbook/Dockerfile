# Please choose from the below set of Docker commands to complete your Dockerfile:

# COPY
# RUN
# ADD
# EXPOSE
# FROM
# CMD
# PUSH
# PULL
# WORKDIR


# Stage 1: Build the Go application
FROM golang:1.18 as builder

WORKDIR /app

COPY main.go .

RUN go mod init guestbook
RUN go mod tidy

RUN go build -o main main.go

# Stage 2: Create a smaller final image to run the application
FROM ubuntu:18.04

# Copy the compiled Go binary from the builder stage
COPY --from=builder /app/main /app/guestbook

# Copy static files like HTML, CSS, and JavaScript to the /app/public directory
COPY public/index.html /app/public/index.html
COPY public/script.js /app/public/script.js
COPY public/style.css /app/public/style.css
COPY public/jquery.min.js /app/public/jquery.min.js

# Set the working directory to /app
WORKDIR /app

# Expose port 3000 on the container to allow access to the Guestbook app
EXPOSE 3000

# Define the command to run the application when the container starts
CMD ["./guestbook"]
