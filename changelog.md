# Changelog for yt-dl-utilities
Richard B. Romig, Email: <rick.romig@gmail.com>

#### 09 October 2019
1. Created a new repository and copied the scripts from the Bashscripts repositiory.

## Earlier history:
### 20 September 2019
1. **yt-dl-install v1.2.0**
  * Moved variable declarations to the top of the script (below header and license).
  * Fixed minor spelling errors.

2. **yt-dl-remove v1.2.0**
  * Moved variable declarations to the top of the script (below header and license).
  * Fixed minor spelling errors.

### 7 September 2019
1. **yt-dl-install v1.1.1**
  * Cleaned up comments and variable names.

### 19 July 2019
1. **yt-dl-install**
  * Added comments to explain pertinent sections of the script.

2. **yt-dl-remove**
  * Created a script to remove youtube-dl from the system without installing the newest version. It will remove the version from the distribution repositories, the version downloaded from <https://yt-dl.org>, or both. When removing the yt-dl.org version, will also remove configuration files, if they exist, and the log file created by z-ytdlup.sh (created by yt-dl-install).

### 18 July 2019
1. **yt-dl-update**
  * Created a short script to update youtube-dl which can be set up in crontab to be run as a cron job or copied as root into `/etc/cron.weekly` (or cron.monthly) to be run with anacron.

### 17 July 2019
1. **yt-dl-install**
  * Removed `sudo apt remove -yyq youtube-dl` from the code removing the repository version of youtube-dl because `apt purge` removes the package along with any configuration files that might exist.

### 16 July 2019
1. **yt-dl-install**
  * Added `sudo apt purge -yyq youtube-dl` to the code to remove the repository version of youtube-dl because simply removing the package did not keep it from being found by the `dpkg -l` command.

### 15 July 2019
1. **yt-dl-install**
  * Changed the method to using `dpkg -l` to see if youtube-dl has been installed from the repository rather than checking for the file in `/usr/bin`.
```
# Old code:
if [ -f /usr/bin/youtube-dl ]; then
# New code:
if dpkg -l | grep -qw youtube-dl
then
```
  * Removed the option for the user to choose whether or not to update. If youtube-dl is installed, the script will automatically run the update command.
  * Added error checking to the curl download of youtube-dl If the download is successful, the script will display the result and assign the appropriate permissions to the file. If the download fails, an error message with an exit code will be displayed.

