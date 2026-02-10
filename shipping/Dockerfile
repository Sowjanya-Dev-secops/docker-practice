FROM node:20.19.6-alpine3.21 AS build
WORKDIR /opt/server
#current directory
COPY package.json . 
COPY *.js .
RUN npm install

FROM node:20.19.6-alpine3.21 
WORKDIR /opt/server
RUN addgroup -S roboshop && adduser -S roboshop -G roboshop && \
    chown roboshop:roboshop /opt/server
EXPOSE 8080
LABEL com.project="roboshop" \
      component="shipping" \
      created_by="sowjanya"
ENV CART_ENDPOINT="cart:8080" \
    DB_HOST="mysql"
COPY --from=build --chown=roboshop:roboshop /opt/server /opt/server
USER roboshop
CMD ["server.js"]
ENTRYPOINT ["node"]


# FROM maven:3.9.11
# EXPOSE 8080
# WORKDIR /opt/server
# COPY pom.xml .
# COPY src ./src
# RUN mvn clean package
# RUN mv target/shipping-1.0.jar shipping.jar 
# ENV CART_ENDPOINT="cart:8080" \
#     DB_HOST="mysql"
# CMD ["java","-jar","shipping.jar"]