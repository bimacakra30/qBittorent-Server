# qBittorrent
How To Install WebUI (For Server) test on Ubuntu 22.04

# Now you can install qBittorrent using the following command.
   ```
   sudo apt install qbittorrent-nox -y
   ```
qBittorrent-nox is the default go-to for headless clients designed to run through a Web interface accessible on the default localhost location at http://localhost:8080. The Web UI access is secured by default, the default account username is (admin), and the password is (adminadmin).
   
1. First, create (qbittorrent-nox) user and group so the service can run as an unprivileged user.
   ```
   sudo adduser --system --group qbittorrent-nox
   ```
   ![image](https://github.com/user-attachments/assets/272541c4-a120-4d15-a3c9-41f7d1da489d)
   
   If you were wondering what (–system) means, you created a system user instead of a typical user.
2. Next, add your username to the qbittorrent-nox user group.
   "sudo adduser your-username qbittorrent-nox"
   An example is my username, “bara” so the command would be.
   ```
   sudo adduser bara qbittorrent-nox
   ```
3. Second, create a systemd service file for qbittorrent-nox.
   ```
   sudo nano /etc/systemd/system/qbittorrent-nox.service
   ```
4. Thirdly, you must copy and paste the following lines into the file.
   ```
   [Unit]
   Description=qBittorrent Command Line Client
   After=network.target

   [Service]
   Type=forking
   User=qbittorrent-nox
   Group=qbittorrent-nox
   UMask=007
   ExecStart=/usr/bin/qbittorrent-nox -d --webui-port=8080
   Restart=on-failure

   [Install]
   WantedBy=multi-user.target
   ```
   Hint you can change the WebUI-port=8080 to another port if you wish. Save the file (CTRL+O), then exit (CTRL+X)
5. Now, reload your systemd daemon for changes to be active with the daemon-reload command.
   ```
   sudo systemctl daemon-reload
   ```
6. Now you can start qBittorrent-nox with the following command.
   ```
   sudo systemctl start qbittorrent-nox
   ```
7. If you want qBittorrent-nox to be started on boot, use the following.
   ```
   sudo systemctl enable qbittorrent-nox
   ```
8. Before you continue, it would be ideal for checking the status to ensure everything is working correctly.
    ```
    systemctl status qbittorrent-nox
    ```
    ![image](https://github.com/user-attachments/assets/d9eb7508-0386-469f-9342-fa45414b8efc)


# Accessing qBittorrent Web UI on Ubuntu Server
qBittorrent can be accessed through your favorite Internet Browser on its Web UI from your local network. To do this type, the server’s internal IP address is followed by the port number (8080), for example, 192.168.55.156:8080, or use if hosted locally, use the localhost address 127.0.0.1:8080 then you should see the following page.
Example :
![image](https://github.com/user-attachments/assets/6574b2cf-b608-4236-9ca5-30ef28d9af3f)

The default username is (admin), and the default password is (adminadmin).


# How To Remove qBittorent
If you would like to remove qBittorrent, this is an easy process. First, you must remove the custom PPA if you have installed this as per the above tutorial.
1. Remove the PPA that you imported with the following command.
   ```
   sudo rm /etc/apt/sources.list.d/qbittorrent.list
   ```
2. Next, remove qBittorrent using the command below.
   ```
   sudo apt autoremove qbittorrent --purge
   ```
3. Users that have installed qBittorrent-nox use the following command.
   ```
   sudo apt autoremove qbittorrent-nox --purge
   ```
And that is it; repeat the tutorial to re-install qBittorrent if you wish it back on your system.
