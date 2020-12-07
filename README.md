

# network
docker network create goals-net
# Database:

docker run \
    --name mongodb \
    -v data:/data/db \
    --rm \
    -d \
    --network goals-net \
    -e MONGO_INITDB_ROOT_USERNAME=dude \
    -e MONGO_INITDB_ROOT_PASSWORD=secret \
    mongo

# Backend
docker build -t goals-node ./backend

docker run \
    --name goals-backend \
    -e MONGODB_USERNAME=dude \
    -e MONGODB_PASSWORD=secret \
    -v logs:/app/logs \
    -v /Users/admin/Documents/docker-multi-container/backend/:/app \
    -v /app/node_modules \
    --rm \
    -d \
    --network goals-net \
    -p 80:80 \
    goals-node

# Frontend
docker build -t goals-react ./frontend

docker run \
    --name goals-frontend \
    --rm \
    -v /Users/admin/Documents/docker-multi-container/frontend/src:/app/src \
    -d \
    -it \
    -p 3000:3000 \
    goals-react
