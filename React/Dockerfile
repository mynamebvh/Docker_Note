FROM node:16-alpine AS builder
LABEL maintainer="Hoang Bui <mynamebvh@gmail.com>"

ENV NODE_ENV production
# Add a work directory
WORKDIR /app
# Cache and Install dependencies
COPY package.json .
COPY yarn.lock .
RUN yarn install --production
# Copy app files
COPY . .
# Build the app
RUN yarn build

# Bundle static assets with nginx
FROM nginx:1.21.0-alpine as production
ENV NODE_ENV production

RUN touch /var/run/nginx.pid && \
    mkdir -p /var/cache/nginx && \
    chown -R nginx:nginx /var/cache/nginx /var/run/nginx.pid

USER nginx
# Copy built assets from builder
COPY --chown=nginx:nginx --from=builder /app/build /usr/share/nginx/html
# Add your nginx.conf
COPY --chown=nginx:nginx nginx.conf /etc/nginx/conf.d/default.conf

# Expose port
EXPOSE 80
# Start nginx
CMD ["nginx", "-g", "daemon off;"]