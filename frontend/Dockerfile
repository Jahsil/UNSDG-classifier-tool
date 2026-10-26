FROM node:22-alpine AS builder

WORKDIR /app

COPY frontend/package*.json ./
RUN npm ci

COPY frontend/ ./

COPY backend/data/sdg_targets/ /backend/data/sdg_targets/
COPY sdg_goal_imgs/ /sdg_goal_imgs/

ARG NEXT_PUBLIC_API_BASE_URL=/
ENV NEXT_PUBLIC_API_BASE_URL=${NEXT_PUBLIC_API_BASE_URL}

RUN npm run build

FROM nginx:1.27-alpine

COPY --from=builder /app/out/ /usr/share/nginx/html/
COPY frontend/nginx.conf /etc/nginx/conf.d/default.conf

EXPOSE 80