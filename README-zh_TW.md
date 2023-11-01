# MetaMask Rescuer

當你在 MetaMask 設定 CTF node 後，發現因為 node 失效導致 MetaMask 一直卡在載入的畫面時，你可以根據以下的步驟解救 MetaMask，就不需要重新安裝。

# 必要環境

- Docker

# Steps

1. 取得 CTF Node URL，例如: `http://dai-plus-plus.challenges.paradigm.xyz:8545/6a4160a4-681e-4003-b2a4-9f2ddc6cd5e6/main`
    - 如果已遺失，可前往 Chrome extensions 畫面，打開 developer mode 後，點進 MetaMask extension Details，找到 inspect views，點擊其中的 background.html
    - 點擊 Network tab，會看到 MetaMask 一直在嘗試連線 Node，接著點擊任一連線後，點擊右邊的 Headers tab，其中的 `Request URL` 就是了

2. 修改本機 `/etc/hosts`，將 Node 的 domain 指向 127.0.0.1，如下範例：

    ```
    127.0.0.1 dai-plus-plus.challenges.paradigm.xyz
    ```

3. 下載本 Repository

4. 置換掉 `nginx.conf` 中的 `{UUID}`，修改後如下範例：

    ```
    server {
      ...

      location /6a4160a4-681e-4003-b2a4-9f2ddc6cd5e6/main {
        ...
      }
    }
    ```

5. 執行 `docker compose up`，當執行完會發現已經有連線進來了，那就是成功將 MetaMask 的連線導向本機的 Anvil

6. 前往 MetaMask，應可正常修改 Network 了
