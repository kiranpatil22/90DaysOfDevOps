# Create users
sudo useradd tokyo

sudo useradd berlin

sudo useradd professor

sudo useradd nairobi

# Create groups

sudo groupadd developers

sudo groupadd admins

sudo groupadd project-team

# Assign users to groups

sudo usermod -aG developers tokyo

sudo usermod -aG developers berlin

sudo usermod -aG admins,project-team professor

sudo usermod -aG project-team nairobi

# Create directories

sudo mkdir -p /project

sudo mkdir -p /project/admin

# Set ownership

sudo chown professor:project-team /project

sudo chown professor:admins /project/admin

# Set permissions
sudo chmod 770 /project

sudo chmod 770 /project/admin
