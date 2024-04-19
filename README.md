# Razer Blade 14 (2023) linux audio fix
This repository includes details on how to fix Speakers (ALC298) not working in Linux on the new Razer Blade 14 (2023)

# Fixing audio

1. Install **alsa-tools** using
   * Ubuntu 
        ```bash
        sudo apt get update
        sudo apt install alsa-tools
        ```
    * Arch 
        ```bash
        sudo pacman -Syu
        sudo pacman -S alsa-tools
        ```
2. Download the **rb_audio.sh** script 
3. Change permissions of the script
    ```bash
    sudo chmod +x ~/Downloads/rb_audio.sh
    ```
4. Run the script
    ```bash
    sudo bash ~/Downloads/rb_audio.sh

# To run the script everytime on startup

1. Copy the file to **/usr/bin/** folder
   ```bash
   sudo cp ~/Downloads/rb_audio.sh /usr/bin/
   ```
2. Create a new service file in **/etc/systemd/system/** folder
    ```bash
    sudo nano /etc/systemd/system/rb_audio.service
    ```
3. Add the following in the file
    ```bash
    [Unit]
    Description=Razer Blade 14 audio fix 

    [Service]
    ExecStart=/usr/bin/rb_audio.sh

    [Install]
    WantedBy=multi-user.target 
    ```
4. Change permissions and enable the service using
    ```bash
    sudo chmod 755 /usr/bin/rb_audio.sh
    sudo systemctl enable rb_audio.service
    ```
5. Restart and test speakers

Credits to [jamir](https://bugzilla.kernel.org/show_bug.cgi?id=207423) for his work
