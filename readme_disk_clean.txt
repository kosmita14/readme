sudo find /home/ -type f -size +50M -exec ls -lh {} \;
sudo ukuu --clean-cache
sudo n rm 7.0.0
sudo apt autoremove

