
Signal
======

What is [Signal]?

[According to Wikipedia:][signal-wikipedia]

> Signal is an encrypted instant messaging and voice calling application
> for Android and iOS. It uses end-to-end encryption to secure all
> communications to other Signal users. Signal can be used to send and receive
> encrypted instant messages, group messages, attachments and media messages.
> Users can independently verify the identity of their messaging correspondents
> by comparing key fingerprints out-of-band. During calls, users can check the
> integrity of the data channel by checking if two words match on both ends of
> the call.
> 
> Signal is developed by Open Whisper Systems. The clients are published as free
> and open-source software under the GPLv3 license.

How to install Signal in Qubes
------------------------------

**CAUTION:** Before proceeding, please carefully read [On Digital Signatures and Key Verification][qubes-verifying-signatures].
This website cannot guarantee that any PGP key you download from the Internet is authentic.
Always obtain a trusted key fingerprint via other channels, and always check any key you download against your trusted copy of the fingerprint.

1. (Optional)Create a TemplateVM (Debian, 11 is used as an example)

       [user@dom0 ~]$ sudo qubesctl --skip-dom0 --targets=debian-11 --show-output state.sls update.qubes-vm

2. Open a terminal in Debian 11 (Or your previously chosen template)

       [user@dom0 ~]$ qvm-run -a debian-11 gnome-terminal
       
3. Use these commands in your terminal (If you chose a different distribution, such as buster, substitute that for xenial in the 4th command)

       (Optional)[user@debian-11 ~]$ sudo apt-get install curl
       (for better signal notifications)[user@debian-11 ~]$ sudo apt-get install dunst
       [user@debian-11 ~]$ curl --proxy 127.0.0.1:8082 -s https://updates.signal.org/desktop/apt/keys.asc | gpg --dearmor | sudo tee -a /usr/share/keyrings/signal-desktop-keyring.gpg > /dev/null
       [user@debian-11 ~]$ echo 'deb [arch=amd64 signed-by=/usr/share/keyrings/signal-desktop-keyring.gpg] https://updates.signal.org/desktop/apt xenial main' | sudo tee -a /etc/apt/sources.list.d/signal-xenial.list
       [user@debian-11 ~]$ sudo apt update && sudo apt full-upgrade && sudo apt install --no-install-recommends signal-desktop

5. Shutdown the TemplateVM (substitute your template name if needed) :

        [user@dom0 ~]$ qvm-shutdown debian-11
        
6. Create an AppVM based on this TemplateVM
7. With your mouse select the `Q` menu -> `Domain: "AppVM Name"` -> `"AppVM Name": Qube Settings` -> `Applications`
(or in Qubes Manager`"AppVM Name"` -> `Settings` -> `Applications`). Select `Signal` from the left `Available` column, move it to the right `Selected` column by clicking the `>` button and then `OK` to apply the changes and close the window.

-----

[qubes-verifying-signatures]: https://www.qubes-os.org/security/verifying-signatures/
[Signal]: https://whispersystems.org/
[signal-wikipedia]: https://en.wikipedia.org/wiki/Signal_(software)
[shortcut]: https://support.whispersystems.org/hc/en-us/articles/216839277-Where-is-Signal-Desktop-on-my-computer-
[shortcut-desktop]: https://www.qubes-os.org/doc/managing-appvm-shortcuts/#tocAnchor-1-1-1
[message]: https://groups.google.com/d/msg/qubes-users/rMMgeR-KLbU/XXOFri26BAAJ
[mailing list]: https://www.qubes-os.org/support/
