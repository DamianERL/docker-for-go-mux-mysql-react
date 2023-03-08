FROM node:15.13-alpine
WORKDIR  /app
COPY . /app
RUN npm install
RUN npm run build
CMD ["npm", "start"]