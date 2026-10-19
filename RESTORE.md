# Restore procedure

## 1. OS and layout (ReaR drive)
1. Attach the ReaR drive (label REAR-000) and boot from it.
2. Choose "Recover <hostname>" and log in as root.
3. Run: rear -v recover
4. The target disk must be the same size as the original or larger. Confirm the layout prompts.
5. Reboot, then check: lsblk -f ; cat /etc/fstab ; vgs ; lvs
   The data volume comes back empty and formatted.

## 2. Data
1. Attach the data drive (label DATABACKUP).
2. Point inventory.ini at the restored machine.
3. ansible-playbook 05-restore-data.yml -e confirm_restore=true
4. Watch: systemctl status datarestore ; tail -f /var/log/datarestore.log
5. Unmount when done: umount /mnt/databackup