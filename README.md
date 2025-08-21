# wm-silnite
Custom plugin for [Watchman Monitoring](https://www.watchmanmonitoring.com) to provide results if an OS update is available.

Alerting if specific Apple security updates have not been installed, or are available for installation.

## As of version .9.9.2.0
* No longer relies on `silnite` for any reporting.
* Uses [Sofa](https://sofa.macadmins.io/getting-started.html) to determine if updates are available.
*	[Based on this example](https://github.com/macadmins/sofa/blob/main/tool-scripts/macOSVersionCheck-EA.sh).
* Simplified output to the dashboard.
* Includes latest release date.
* Informational warning (no ticket/email) if update was released within the last 8 days.
* Alert (ticket/email) if update is pending and it has been longer than 8 days after release.
* Preference Pane/Settings removed.

### Informational Example (less than 8 days from release)
<img width="586" height="235" alt="Image" src="https://github.com/user-attachments/assets/a1974674-25a0-4058-abd2-88cb1074052c" />

### Alert Example (greater than 8 days after release)
<img width="593" height="243" alt="Image" src="https://github.com/user-attachments/assets/298f087d-928a-4797-8a20-56ca676c0b13" />

## As of version .9.8.0.0
* Removes the use of `silnite` binary and only relies on information curled from Apple.
* No longer reports MRT, XProtect, or XProtect Remediator information.
* No longer checks if SIP or XProtect is disabled.

## As of version .9.7.0.0
* Uses curl to pull down current OS version information from https://gdmf.apple.com/v2/pmv.
	* Shout out to Ross Matsuda of https://www.sudoade.com/author/ross/ for the excellent write up on how to get the latest OS version updates.
* Uses `curl` result to determine if the current OS matches on alerting for ticket/email (`exit 2`).
* Will run OS version check during every run.
* Configuration Data related to XProtect/MRT/etc will continue to run according to schedule.
* Results for Configuration data will be an informational result (no ticket/email) in the Watchman Monitoring dashboard (`exit 20`).

# No Longer Valid ¬

## As of version .9.6.0.0
* Requires silnite 10 to be installed
* Creates a text file with results of a full run at `/Library/MonitoringClient/PluginSupport/_wm_silnite_results.txt`
* Will run an hourly _light_ run based off results file.
* Full run of `silnite` results will still be based off _Frequency to check for updates_... results file will be updated at that time.
* Fixes stale plugin results (now that data is sent during every run).
* Added Run Count Information to Plugin results.
* Removes Gatekeeper Version reporting (results removed from silnite 10).
* Adds XProtect Remediator Version reporting.

<img width="935" alt="Capture_2023-11-09_08-27-55_AM" src="https://github.com/macitpros/wm-silnite/assets/17754199/89c1996f-3648-47bb-8cd7-0a5ea225e18c">

## As of version .9.5.9:
* Uses `/Library/Preferences/com.apple.SoftwareUpdate.plist/Library/Preferences/com.apple.SoftwareUpdate.plist` for gathering list of recommended updates (stops using `softwareupdate -l`).
* Adjusts if a plist setting file is missing an expected value.
* Creates a default settings plist on new installation.
* Changes default reporting frequency to 8 from 12 (more frequently).

## As of version .9.0.1:
* Simply a version bump to match current `silnite` binary version number
* Requires silnite 9 to be installed
* Get silnite version 9 from Eclectic Light: https://eclecticlight.co/lockrattler-systhist/

## As of version .7.0.1:
* Adds compatibility for silnite 6, which in turn adds compatibility with Apple Silicon and macOS 12. 
* Get silnite version 6 from Eclectic Light: https://eclecticlight.co/lockrattler-systhist/
* This version is NOT compatible with older versions of silnite. Requires silnite 6 to be installed.



## As of version .6.4.0:

**Preference Pane**
* _Frequency to check for updates_
  * Sets how often a full run will be done. More time between full checks will help speed up regular Watchman Monitoring reporting.

* _Unable to check for updates attempts_
  * If `silnite` is unable to check for updates due to a connection failure, an informational warning will be generated (no tickets/emails) in your Watchman Monitoring dashboard. If the number of attempts exceeds this number, an alert (ticket/email) will be generated.

![screenshot_1069](https://user-images.githubusercontent.com/17754199/64067360-fe427780-cbec-11e9-9725-9d68cdffc0ec.png)

**Terminal/Command Line Options**
* Force a one-time full run ignoring the frequency count: `sudo defaults write /Library/MonitoringClient/PluginSupport/_wm_silnite_settings.plist First_Run -bool true`
* Set the "Frequency to check for updates" count (set _NUM_ to the number): `sudo defaults write /Library/MonitoringClient/PluginSupport/_wm_silnite_settings.plist Check_For_Updates _NUM_`
* Set the "Unable to check for updates attempts" count (set _NUM_ to the number): `sudo defaults write /Library/MonitoringClient/PluginSupport/_wm_silnite_settings.plist Warn_Updates_Attempts _NUM_`

**Emails daily/ticket created (exit 2) if...**
* `silnite` reports updates are available `UpdateWaiting = 1`

This means...
* MRT could be out-of-date
* XProtect Remediator could be out-of-date
* XProtect could be out-of-date
* Other updates from `softwareupdate` are available and will be listed

**If unable to check for updates, shows informational warning (exit 20)**
Includes report of installed versions:
* MRT 
* XProtect Remediator
* XProtect


**(initial testing complete, still needs more testing) Sends one-time alerts (exit 200) if...**
* SIP Disabled
* XProtect Disabled

![wmscreenshot](https://user-images.githubusercontent.com/17754199/63029161-ae865100-be75-11e9-9f38-b70a42c363b3.png)

**Known Issues**
* None

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
THE SOFTWARE.
