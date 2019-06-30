1. Download ngrok
https://ngrok.com/download

2. Unzip
unzip ~/Downloads/ngrok.zip

After unzip -> file executable (exec): ngrok

3. Register a ngrok account. After login -> get <YOUR_AUTH_TOKEN>

4. Add authtoken (Connect your account)
./ngrok authtoken <YOUR_AUTH_TOKEN>

This command to write auth token config to /Users/kevinduy/.ngrok2/ngrok.yml

5. Run
- c1:
    with homestead: ngrok http 192.168.10.10:80 -host-header=myapp.dev

    with server: ngrok http 127.0.0.1:80 -host-header=tomato.localhost

- c2:
    ngrok http -host-header=rewrite tomato.localhost:80