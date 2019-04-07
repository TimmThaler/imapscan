# Mark spam with isbg and SpamAssassin

*Docker container that uses [isbg](https://github.com/dc55028/isbg) to filter out spam from a remote IMAP server.*


## Configuration
There are 2 volumes, their content is initialized during container startup:

* /var/spamassassin : holds the SpamAssassin data files, to keep them between container resets.
* /root/accounts : holds the IMAP accounts configuration.

The container runs a learning process on startup, so do not leave a configuration with a huge email directory active if you want the container to start in a reasonnable time.

## Starting the Docker container

1) Clone or download this repository to your computer.
2) Build your *image*: `docker build -t MyImageName:MyTag .`
3) Start the *container*: `docker run -d --name ContainerName -v PathTo/spamassassin:/var/spamassassin -v PathTo/accounts:/root/accounts MyImageName:MyTag`
4) Configure your IMAP accounts: Adjust the `accounts_imap.txt` and `imap_accounts_learn.txt` in the **/root/accounts** volume.
They are tab-separated files, and the first line has the field names.
In both files, the *junk* field is where the Spam folder is, and the last field is the directory you want to scan, either to learn spam or to scan for spam.
