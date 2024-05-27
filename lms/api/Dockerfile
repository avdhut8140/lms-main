# Docker file nodejs azure app services
FROM node:16
# Create app directory
RUN mkdir /backend
WORKDIR /backend
# Install app dependencies
COPY  . /backend

RUN npm install
RUN npx prisma generate
RUN npm run build
# Expose port
EXPOSE 8080
# Start app
CMD ["node","build/index.js"]

