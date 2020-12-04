
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
    -d \
    -it \
    -p 3000:3000 \
    goals-react

# network
docker network create goals-net