# IBSNG Radius Server

## Overview

IBSNG is a robust Radius Server designed for easy installation and configuration. This project provides a free version of the server that can be quickly set up on a CentOS 7 system. It is intended for users with root privileges.

## Prerequisites

- **Operating System:** CentOS 7
- **User Privileges:** You must be logged in as the `root` user.

## Installation Instructions

Follow the steps below to install and configure the IBSNG Radius Server on your CentOS 7 system.

### Step 1: Install Required Packages

Open your terminal and run the following command to install the required software packages:

```bash
yum install httpd php postgresql postgresql-server postgresql-python git perl firewalld -y
```

### Step 2: Initialize PostgreSQL Database

Next, initialize the PostgreSQL database:

```bash
postgresql-setup initdb
systemctl start postgresql
```

### Step 3: Set Up the Database and User

Create the database and user required for IBSNG:

```bash
su postgres
createdb IBSng
createuser ibs
createlang plpgsql IBSng
exit
```

### Step 4: Clone the IBSng Repository

Clone your IBSng repository from GitHub:

```bash
git clone https://github.com/imafaz/IBSng.git
mv IBSng /usr/local
```

### Step 5: Run the Initialization Script

Navigate to the scripts directory and change permissions for the initialization script:

```bash
cd /usr/local/IBSng/scripts
chmod 777 init.py
./init.py
```

### Step 6: Configure the Firewall

Enable and start the firewall service, and allow the necessary ports:

```bash
systemctl enable firewalld
systemctl start firewalld
firewall-cmd --add-port=80/tcp --permanent
firewall-cmd --add-port=1812/tcp --permanent
firewall-cmd --add-port=1813/tcp --permanent
firewall-cmd --reload
```

## Conclusion

You have successfully installed the IBSNG Radius Server on your CentOS 7 system. For further customization and configuration, refer to the official documentation or explore the repository.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Support

If you encounter any issues or have questions, feel free to open an issue in this repository.