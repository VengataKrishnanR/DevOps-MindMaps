# 🧠 Dockerfile Learning Mind Map

## 🔹 1. Dockerfile Basics
- Dockerfile is a set of instructions to build a Docker image
- Each line is an instruction: `FROM`, `COPY`, `RUN`, `CMD`, etc.
- Instructions are case-sensitive (e.g., `FROM` not `from`)

---

## 🔹 2. Core Instructions

### ✅ `FROM`
- Specifies the base image
- Example:
  ```Dockerfile
  FROM nginx:alpine
  FROM openjdk:17-jdk-slim
  ```

### ✅ `WORKDIR`
- Sets the working directory inside the container
- Auto-creates the directory if it doesn't exist
- Example:
  ```Dockerfile
  WORKDIR /app
  ```

### ✅ `COPY`
- Copies files from build context to image
- Syntax:
  ```Dockerfile
  COPY <source> <destination>
  ```
- Example:
  ```Dockerfile
  COPY . /usr/share/nginx/html
  COPY index.html /usr/share/nginx/html/
  ```
- Absolute paths like `/home/user/file.html` ❌ not allowed — must be relative

### ✅ `RUN`
- Executes a command **during image build**
- Example:
  ```Dockerfile
  RUN rm -rf /usr/share/nginx/html/*
  RUN apt-get update && apt-get install -y vim
  ```

### ✅ `CMD`
- Specifies the default command when container starts
- Example (Nginx):
  ```Dockerfile
  CMD ["nginx", "-g", "daemon off;"]
  ```
- Container exits if CMD process ends

### ✅ `EXPOSE`
- Documents which port the container listens on
- Does **not** actually open the port — you still need `-p` during `docker run`
- Example:
  ```Dockerfile
  EXPOSE 80
  ```

---

## 🔹 3. Multi-Stage Build (for Java apps)

```Dockerfile
# Stage 1: Build with Maven
FROM maven:3.9.6-eclipse-temurin-17 AS build
WORKDIR /app
COPY pom.xml .
COPY src ./src
RUN mvn clean package -DskipTests

# Stage 2: Run with JRE
FROM eclipse-temurin:17-jre
WORKDIR /app
COPY --from=build /app/target/*.jar app.jar
EXPOSE 8080
CMD ["java", "-jar", "/app/app.jar"]
```

---

## 🔹 4. Common Errors and Fixes

| Error                         | Cause                          | Fix                                                                  |
| ----------------------------- | ------------------------------ | -------------------------------------------------------------------- |
| `COPY /abs/path/file.html`    | Absolute path                  | Use relative paths (`COPY . /app`)                                   |
| `unknown instruction`         | Typo in instruction            | Use uppercase keywords (`COPY`, `FROM`)                              |
| `container exits immediately` | No `CMD` running in foreground | Use CMD with a long-running process (e.g., Nginx with `daemon off;`) |
| `connection refused`          | Wrong port mapping             | Ensure correct `-p` host:container and app listens inside           |

---

## 🔹 5. Real-World Use Cases

### ✅ Static Web App (Nginx)

```Dockerfile
FROM nginx:1.27.0
RUN rm -rf /usr/share/nginx/html/*
COPY . /usr/share/nginx/html/
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
```

### ✅ Java App (Spring Boot)

```Dockerfile
FROM eclipse-temurin:17-jre
WORKDIR /app
COPY target/my-app.jar app.jar
EXPOSE 8080
CMD ["java", "-jar", "/app/app.jar"]
```

---

## 🧠 Tips to Remember

- Always use a `.dockerignore` file to exclude unnecessary files
- Keep Dockerfile minimal and production-safe
- Use multi-stage builds to reduce final image size
- Build context matters — always `COPY` relative to current folder
- Test with `curl` or browser after running with `-p`
