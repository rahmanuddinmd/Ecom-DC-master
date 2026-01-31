# Kastro's Application - Microservice E-commerce

This is a microservice-based e-commerce application that uses Docker and Docker Compose for containerization and orchestration.

## Architecture

The application consists of 5 microservices:

1. **Main Service** (Port 5001): The main landing page and navigation hub
2. **Product Catalog** (Port 5002): Displays products available for purchase
3. **Shopping Cart** (Port 5003): Manages the user's shopping cart
4. **User Profile** (Port 5004): Handles user information and preferences
5. **Order Management** (Port 5005): Processes and tracks orders

A reverse proxy routes traffic from port 80 to the appropriate microservice.

## Part 1: Setting up individual microservices

### Step 1: Clone the repository

```bash
git clone https://github.com/yourusername/kastros-application.git
cd kastros-application
```

### Step 2: Build Docker images for each service

```bash
# Build Main Service
cd main-service
docker build -t kastro-main-service .
cd ..

# Build Product Catalog Service
cd product-service
docker build -t kastro-product-service .
cd ..

# Build Shopping Cart Service
cd cart-service
docker build -t kastro-cart-service .
cd ..

# Build User Profile Service
cd user-service
docker build -t kastro-user-service .
cd ..

# Build Order Management Service
cd order-service
docker build -t kastro-order-service .
cd ..
```

### Step 3: Run individual containers (optional, for testing)

```bash
# Run Main Service
docker run -d -p 5001:80 --name kastro-main kastro-main-service

# Run Product Catalog Service
docker run -d -p 5002:80 --name kastro-product kastro-product-service

# Run Shopping Cart Service
docker run -d -p 5003:80 --name kastro-cart kastro-cart-service

# Run User Profile Service
docker run -d -p 5004:80 --name kastro-user kastro-user-service

# Run Order Management Service
docker run -d -p 5005:80 --name kastro-order kastro-order-service
```

## Part 2: Deploying with Docker Compose

### Step 1: Set up Docker and Docker Compose on EC2

Make sure Docker and Docker Compose are installed on your EC2 instance:

```bash
# Update system packages
sudo apt-get update

# Install Docker
sudo apt-get install -y docker.io

# Start Docker service
sudo systemctl start docker
sudo systemctl enable docker

# Add current user to docker group (optional)
sudo usermod -aG docker ${USER}

# Install Docker Compose
sudo curl -L "https://github.com/docker/compose/releases/download/v2.20.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
```

### Step 2: Deploy with Docker Compose

```bash
# Navigate to project directory
cd kastros-application

# Start all services with Docker Compose
sudo docker-compose up -d
```

### Step 3: Verify the deployment

After deployment, you can access the application at:

- Main application: http://your-ec2-ip/ (Port 80)
- Individual services:
  - Main Service: http://your-ec2-ip:5001
  - Product Catalog: http://your-ec2-ip:5002
  - Shopping Cart: http://your-ec2-ip:5003
  - User Profile: http://your-ec2-ip:5004
  - Order Management: http://your-ec2-ip:5005

### Step 4: Stopping the services

To stop all services:

```bash
sudo docker-compose down
```