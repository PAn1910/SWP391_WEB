# Sử dụng base image Maven để build file WAR tự động trên cloud
FROM maven:3.8.5-openjdk-17 AS build
WORKDIR /app
COPY . .
RUN mvn clean package -DskipTests

# Chạy ứng dụng trên máy chủ Apache Tomcat 9 (ĐÃ ĐỔI BASE IMAGE)
FROM tomcat:9.0-jre17-temurin
RUN rm -rf /usr/local/tomcat/webapps/*
COPY --from=build /app/target/*.war /usr/local/tomcat/webapps/ROOT.war

# Cấu hình cổng động theo Render
EXPOSE 8080
CMD ["catalina.sh", "run"]