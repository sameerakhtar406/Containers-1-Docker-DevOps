# Containers-1-Docker-DevOps

# 🐳 Simple Docker Nginx Web Server

A foundational DevOps project demonstrating how to deploy a static HTML website using Docker, Nginx, and Alpine Linux. 

This project serves as a practical introduction to containerization, port routing, and Linux volume mounting.

## 📂 Project Structure

* `index.html`: The static web page content.
* `README.md`: Project documentation and theory.

# How to Run Locally

*1. Clone the repository and navigate into it:*
Make sure your terminal is in the exact same directory as the `index.html` file.

*2. Start the Docker container:*
Run the following command to deploy the web server:
sudo docker run -d -p 8080:80 -v $(pwd)/index.html:/usr/share/nginx/html/index.html --name my-web-server nginx:alpine 

*3. View the website:*
Open your web browser and navigate to: http://localhost:8080

*4. Clean up:*
When you are done, stop and remove the container to free up the port and name:
sudo docker rm -f my-web-server

🧠 The CS & Linux Theory: Breaking Down the Command

Here is exactly what that long docker run command did under the hood at the Linux Kernel level:

sudo: Invokes superuser privileges. Docker talks directly to the Linux Kernel to allocate resources, which requires root permissions.

-d (Detached Mode): Tells Linux to run this container as a Daemon (a background process). It frees up your terminal prompt immediately.

-p 8080:80 (Port Forwarding): Binds port 8080 of your host Linux OS to port 80 inside the container. The kernel routes any traffic hitting your machine at 8080       into the isolated network namespace of the container.

-v $(pwd)/index.html:... (Volume Mount): $(pwd) prints your Present Working Directory. This command tells the Linux Virtual File System (VFS) to point the container's internal folder directly to the file on your hard drive.

nginx:alpine: Nginx is the web server software. Alpine is a security-focused, ultra-lightweight Linux distribution that is only about 5MB in size.

📚 Glossary: What Everything Means

To fully understand the stack, here is a breakdown of every technology and concept used in this project:

Docker: A platform that packages software and its dependencies into standardized units called containers, ensuring the software runs exactly the same regardless of the host machine.

Container: A lightweight, standalone, and executable package of software that includes everything needed to run an application (code, runtime, system tools, system libraries, and settings). It runs in an isolated space on the host operating system.

Image: A read-only template with instructions for creating a Docker container. In this project, nginx:alpine is the image we downloaded to create our my-web-server container.

Nginx: An extremely popular, high-performance open-source web server. Its primary job is to listen for HTTP requests from a browser and send back the correct files (like our index.html).

Alpine Linux: A minimalist Linux operating system designed for security, simplicity, and resource efficiency. Using an Alpine-based image keeps the container footprint incredibly small, reducing download times and attack surfaces.

Host Machine: The physical (or virtual) computer that is running the Docker Engine—in this case, your personal computer.

Bind Mount: A Docker feature that links a specific file or directory on the host machine to a specific location inside the container. It allows the container to read and write data directly to the host's filesystem.

Daemon: A computer program that runs as a background process, rather than being under the direct control of an interactive user. Both Docker itself and our Nginx web server run as daemons.

