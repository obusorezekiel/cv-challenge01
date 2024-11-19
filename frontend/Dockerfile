# Use the latest official Node.js image as a base
FROM node:latest

WORKDIR /app

COPY . .

RUN npm install

EXPOSE 5173


CMD ["npm", "run", "dev", "--", "--host"]