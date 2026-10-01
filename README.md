This parameter intend to fix an issue on Debian 13.7 with protonvpn-cli 1.0.5

When trying to connect througt the VPN, Proton keeps asking for a root access on networkmanager

To apply the fix 
- run while in root or sudoer (add *sudo*)
```
nano /etc/polkit-1/rules.d/49-networkmanager-network-control.rules
```
- add the file | Copy the rule
- Set the name of the current user between the ""
```
polkit.addRule(function(action, subject) {
    if (subject.user == "YOURCURRENTUSER" &&
        (action.id == "org.freedesktop.NetworkManager.network-control" ||
         action.id == "org.freedesktop.NetworkManager.settings.modify.own")) {
        return polkit.Result.YES;
    }
});
```
- restart polkit 
```
systemctl restart polkit
```
