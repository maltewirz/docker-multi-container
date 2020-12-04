
# Database:

docker run \
    --name mongodb \
    --rm \
    -d \
    -p 27017:27017 \
    mongo

# Backend
docker build -t goals-node ./backend

docker run \
    --name goals-backend \
    --rm \
    -d \
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

