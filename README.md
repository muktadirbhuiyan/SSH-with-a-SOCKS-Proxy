# SSH-with-a-SOCKS-Proxy
To set up your local PC to access the Swagger URL through your EC2 instance so that requests appear to come from the EC2 instance, you can use SSH tunneling to create a SOCKS proxy. Here are the steps to accomplish this

## Step 1: Connect to your EC2 instance using SSH with a SOCKS Proxy
1. Open a terminal on your local machine.

2. Run the following command to create a SOCKS proxy through your EC2 instance:

`ssh -i /path/to/your-key.pem -D 9090 ec2-user@your-ec2-public-ip`

- Replace `/path/to/your-key.pem` with the path to your EC2 key pair.
- Replace ec2-user with your EC2 username (e.g., ubuntu for Ubuntu instances).
- Replace your-ec2-public-ip with the public IP address of your EC2 instance.
- The -D 9090 option tells SSH to create a SOCKS proxy on port 9090 on your local machine.

3. Keep this terminal open to maintain the SOCKS proxy.

## Step 2: Configure Your Browser to Use the SOCKS Proxy
1. Open your browser and configure it to use the SOCKS proxy on `localhost:9090.`

* In Firefox: Go to Settings > Network Settings > Settings (under Network Settings), select Manual proxy configuration, and enter localhost and 9090 as the SOCKS Host. Choose SOCKS v5.
* In Chrome (if Chrome doesn’t support SOCKS natively on your OS):
Use a Chrome extension like SwitchyOmega or FoxyProxy to set up the proxy.
2. Test the proxy by going to https://whatismyipaddress.com/ or a similar site. It should display the public IP address of your EC2 instance.

## Step 3: Access the desired URL
Now that your browser traffic is being routed through the EC2 instance, navigate to:


[Markdown Live Preview](https://api.com/api/enterprise/swagger/index.html)

Since the request appears to come from the EC2 instance, it should recognize the API Key as valid.

### Additional Notes
- Ensure your EC2 instance is configured correctly with the necessary permissions and IP whitelisting to access the API.
- Keep the SSH connection open to maintain the proxy; closing it will stop the proxy.
- This method allows all requests from your browser to be routed via the EC2 instance, so when you make API calls in the Swagger interface, they should be routed through the EC2 instance.
