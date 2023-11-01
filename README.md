# MetaMask Rescuer

When you set up the CTF node in MetaMask and find that it's stuck on a loading screen due to a node failure, you can rescue MetaMask by following these steps, avoiding the need for a reinstallation.

## Prerequisites

- Docker

## Steps

1. Obtain the CTF Node URL, for example: `http://dai-plus-plus.challenges.paradigm.xyz:8545/6a4160a4-681e-4003-b2a4-9f2ddc6cd5e6/main`
    - If you've lost this, go to the Chrome extensions page, open `developer mode`, click into the MetaMask extension Details, find inspect views section, and click on `background.html`.
    - And then click on the Network tab, and you'll see MetaMask continuously trying to connect to the node. Click on any connection, and on the right side, under the Headers tab, you'll find the Request URL.
2. Modify your local `/etc/hosts` file by redirecting the Node's domain to 127.0.0.1, as shown in the example:

    ```
    127.0.0.1 dai-plus-plus.challenges.paradigm.xyz
    ```

3. Clone or download this Repository.

4. Replace the {UUID} in nginx.conf, and modify it as shown in the example:

    ```
    server {
      ...

      location /6a4160a4-681e-4003-b2a4-9f2ddc6cd5e6/main {
        ...
      }
    }
    ```

5. Run `docker compose up`, and when it's done, you'll see connections coming in, indicating that you've successfully redirected MetaMask's connection to the local Anvil.

6. Go to MetaMask, and you should be able to change the Network settings as needed.
