FROM node:16.10-alpine AS build

WORKDIR /app

EXPOSE 4200

COPY AosoFront/package.json AosoFront/package-lock.json ./

#COPY --from=build dist/DevOpsFront /usr/share/nginx/html
RUN npm uninstall -g @angular/cli
RUN npm cache verify
RUN npm config rm proxy
RUN npm config rm https-proxy
RUN npm install -g npm@8.13.2 -g @angular/cli
RUN npm install

COPY ./AosoFront .

#RUN npm run build

RUN ng build --prod
CMD ng serve

FROM nginx:latest
RUN rm -rf RUN rm -rf /etc/nginx/nginx.conf
COPY /nginx/nginx.conf /etc/nginx/nginx.conf
COPY --from=build /app/dist/DevOpsFront /usr/share/nginx/html
ENTRYPOINT ["nginx", "-g", "daemon off;"]
# FROM node:16.10-alpine AS build
# WORKDIR /app
# EXPOSE 4200
# COPY AosoFront/package.json AosoFront/package-lock.json ./
# #COPY --from=build dist/DevOpsFront /usr/share/nginx/html
# RUN npm install -g npm@8.11.0 -g @angular/cli 
# RUN npm install
# COPY ./AosoFront .
# #RUN npm run build
# RUN ng build --prod
# CMD ng serve

# FROM nginx:latest
# RUN rm -rf RUN rm -rf /etc/nginx/nginx.conf
# COPY /nginx/nginx.conf /etc/nginx/nginx.conf
# COPY --from=build /app/dist/AosoFront /usr/share/nginx/html
# ENTRYPOINT ["nginx", "-g", "daemon off;"]
