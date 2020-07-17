# Changelog for yt-dl-utilities

Richard B. Romig, Email: [rick.romig@gmail.com]()

### 17 July 2020

**yt-dl-install**

- Added a function to determine if the distribution is based on Ubuntu 20.04 LTS. Since Ubuntu 20.04 has removed python 2 support, youtube-dl, as downloaded from yt-dl.org no longer works. If the distribution is based on Ubuntu 20.04, the script will display an error message and exit.

- Removed references to youtube-dl version numbers.

**yt-dl-remove**

- Removed `exists` function. Script now checks if `/usr/local/bin/youtube-dl` exists using the `-f` test.

- Updated the `rm_cfg` function to display results for the removal of each configuratin file.

- Removed references to youtube-dl version numbers.

### 16 July 2020

**z-ytdlupdate**

- Renamed the variables used to trim the log file.
  
  ```bash
  # Old code
  LINES=$(wc -l /var/log/ytdlup.log | awk '{ print $1 }')
  (( LINES > 30 )) && sed -i '1d' /var/log/ytdlup.log
  LINE1=$(sed -n '1p' /var/log/ytdlup.log | grep 'Updated')
  [ -n "$LINE1" ] &&  sed -i '1d' /var/log/ytdlup.log
  # New code
  LOG_LEN=$(wc -l "$LOG_FILE" | awk '{ print $1 }')
  (( LOG_LEN > 30 )) && sed -i '1d' "$LOG_FILE"
  LINE_ONE=$(sed -n '1p' "$LOG_FILE" | grep 'Updated')
  [ -n "$LINE_ONE" ] && sed -i '1d' "$LOG_FILE"
  ```

### 18 June 2020

**z-ytldupdate**

- Replaced the if statement with single line commands to remove earlier entries from the log file if the number of lines exceeded 30 lines, since only the first line was actually being removed from the file.  If, after running the update, the first line indicates that youtube-dl was upated, the next line will also be deleted as it is part of that entry.
  
  ```bash
  # Old code
  LINES=$(wc -l /var/log/ytdlup.log | awk '{ print $1 }')
  if (( LINES > 30 )); then
    tail -n 30 /var/log/ytdlup.log > /var/log/ytdlup.tmp
    mv /var/log/ytdlup.tmp /var/log/ytdlup.log
  fi
  # New code
  LINES=$(wc -l /var/log/ytdlup.log | awk '{ print $1 }')
  (( LINES > 30 )) && sed -i '1d' /var/log/ytdlup.log
  LINE1=$(sed -n '1p' /var/log/ytdlup.log | grep 'Updated')
  [ -n "$LINE1" ] &&  sed -i '1d' /var/log/ytdlup.log
  ```

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
