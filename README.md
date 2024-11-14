# ssl_certficate_configuration_navi


Overview of SSL/TLS and Certbot
SSL (Secure Sockets Layer) and its successor TLS (Transport Layer Security) are protocols that encrypt the connection between your web server and a client (browser). This ensures that any data exchanged between them, like login credentials or personal information, is kept secure from eavesdroppers. Installing an SSL certificate on your server enables HTTPS, which is the secure version of HTTP.

Certbot is a free tool provided by the Electronic Frontier Foundation (EFF) that automates the process of obtaining and renewing SSL certificates, especially with Let's Encrypt, a popular certificate authority.

Step 1: Install Certbot and Nginx Plugin
Theory: Certbot needs to be installed on your system because it handles the process of obtaining an SSL certificate for your domain. The python3-certbot-nginx plugin allows Certbot to interact with Nginx, automatically configuring it to use the new SSL certificate without manual edits to the configuration files.

Command Explanation:

sudo apt install certbot python3-certbot-nginx: This command installs both Certbot and the Nginx plugin.
sudo: Runs the command as an administrator.
apt install: Installs the specified packages.
certbot: The main Certbot tool.
python3-certbot-nginx: The Nginx plugin for Certbot.
Step 2: Adjust the Firewall
Theory: When you install SSL, your server will start serving content over HTTPS (port 443) instead of HTTP (port 80). Many Linux servers use firewalls (like UFW - Uncomplicated Firewall) to control access to different services and ports. To ensure users can reach your server over both HTTP and HTTPS, you need to configure the firewall to allow traffic on these ports.

Command Explanation:

sudo ufw allow 'Nginx Full': This command tells UFW to allow both HTTP (80) and HTTPS (443) traffic for Nginx.
sudo ufw status: Checks the status of your firewall to confirm that the rule has been applied successfully.
Step 3: Obtain an SSL Certificate with Certbot
Theory: Certbot will communicate with Let's Encrypt to issue an SSL certificate for your domain. For this step to work, your domain must be pointed to the server’s IP address; otherwise, Let’s Encrypt won’t verify that you own the domain, and the SSL certificate cannot be issued.

Certbot verifies your domain ownership, generates a certificate, and configures Nginx to use the new certificate. After the configuration, your site will be accessible over HTTPS.

Command Explanation:

sudo certbot --nginx -d example.com -d www.example.com:
sudo: Runs the command as an administrator.
certbot: Launches the Certbot tool.
--nginx: Specifies that Certbot should use the Nginx plugin to configure the server.
-d: Specifies the domain(s) for which you’re requesting the SSL certificate. You can include multiple -d flags to cover different subdomains.
Once you run this command, Certbot will:

Verify Domain Ownership: Certbot communicates with Let’s Encrypt to prove that you own/control the domain.
Issue Certificate: After verification, Let’s Encrypt issues an SSL certificate.
Configure Nginx: The Nginx plugin automatically modifies your Nginx configuration to use the new SSL certificate.
Summary
With these steps, you’re:

Installing necessary tools (Certbot and its Nginx plugin).
Allowing HTTP/HTTPS traffic through the firewall.
Obtaining an SSL certificate and configuring your web server to use HTTPS.
Certbot also sets up automatic renewals, meaning your SSL certificate will renew itself before expiration, keeping your site secure without further manual intervention.
