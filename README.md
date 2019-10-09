# yt-dl-utilities
Utilities to install, remove, and update youtube-ld on Debian/Ubuntu

### yt-dl-install
1. Installs the newest available version of youtube-dl from the [youtube-dl project](https://ytdl-org.github.io/youtube-dl/index.html), using the instructions given on the youtube-dl download page.
2. Although youtube-dl is included in the Debian and Ubuntu repositories, it is often well out of date and infrequently updated. The apt package manager usually installs youtube-dl in `/usr/bin/` while the project's download instructions suggest installing it in `/usr/local/bin/`.
3. If the script finds that youtube-dl has been installed by the package manager, it removes the package using `apt purge`. Then it checks to see if youtube-dl is installed (presumably from the youtube-dl project). If installed, the script displays the version number and attempts to update it. Otherwise, the newest version of youtube-dl is installed from yt-dl.org.
4. Once youtube-dl is installed, you can update it from a terminal with the command `sudo youtube-dl -U` since the yt-dl.org version should be the only version installed. Alternatively, the script can be used to update it.
5. During the yt-dl.org instillation of youtube-dl, the script copies a small script (if it exists in your ~/bin directory) to automatically update youtube-dl on a daily basis using anacron. The z-ytdlupdate script is set up to write the date and the output of the `youtube-dl -U` command to a log file in `/var/log`. The size is limited to the last 25 update attempts.
6. Entering `yt-dl-install -i` or `yt-dl-install --info` in the terminal displays information about the script.

### yt-dl-remove
1. Completely removes youtube-dl from the system whether it is the distribution repository version or the version downloaded from <https://yt-dl.org>. If both are installed, both will be removed.
2. If the `~/.config/youtube-dl/conf` or `/etc/youtube-dl.conf` configuration files exist, they will be removed. Be sure to make backup copies if you think you might need them.
3. If `z-ytdlupdate` exists in `/etc/cron.daily`, `/etc/cron.weekly`, or `/etc/cron.monthly` directories, it will be removed.
3. If the log file created by the automatic updates (`/var/log/ytdsup.log`) exists, it too will be removed.
4.  Entering `yt-dl-remove -i` or `yt-dl-remove --info` in the terminal displays information about the script.

### yt-dl-update
1. Once youtube-dl has been installed by yt-dl-install, setting up yt-dl-update as a cron or anacron job can help keep youtube-dl up to date. You can set up a cron job using crontab. Alternatively, you can, as root (sudo) copy the script to `/etc/cron.daily`, `/etc/cron.weekly` or `/etc/cron.monthly` to be run by anacron.
```
sudo cp /path/to/yt-dl-update /etc/cron.daily
```
2. This script will update youtube-dl without leaving a log file.

### z-ytdlupdate
1. This youtube-dl update script is specifically written to be run as an anacron or cron job. If the script is in `~/bin` when yt-dl-install is run, it will be copied to `/etc/cron.daily` to be run as an anacron script.
2. To change the frequncy of the update, move the script to `/etc/cron.weekly` or `/etc/cron.monthly`
3. This script creates a log file in `/var/log` which is limited to up to 25 entries, depending on how often youtube-dl is updated.

### Feedback:

Feel free to contact me with comments and suggestions for FnLoC. Also feel free to share any code or ideas that will help me improve this program. I can be reached through my blog, Twitter, and email.

* [GitHub](https://github.com/RickRomig/yt-dl-utilities.git)
* [Rick's Tech Stuff](https://ricktech.wordpress.com)
* [Twitter (@ludditegeek)](https://twitter.com/ludditegeek)
* Email: <rick.romig@gmail.com> or <rb_romig@twc.com>

Richard Romig
25 April 2019

### DISCLAIMER

THIS SOFTWARE IS PROVIDED "AS IS" AND ANY EXPRESSED OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE ARE DISCLAIMED. IN NO EVENT SHALL I BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS AND SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.
