FROM node:14.15.1 AS deps
# RUN apk add --no-cache libc6-compat
# Create app directory
WORKDIR /usr/src/app
COPY package.json ./
COPY yarn.lock ./
RUN yarn install --frozen-lockfile

# Install app dependencies
FROM node:14.15.1 AS builder
WORKDIR /usr/src/app
# Bundle app source
COPY . .
COPY --from=deps /usr/src/app/node_modules ./node_modules
RUN yarn
RUN rm -rf dist
#RUN rm -rf node_modules

# Build app
RUN yarn build:babel

EXPOSE 8080

CMD [ "yarn", "start" ]
