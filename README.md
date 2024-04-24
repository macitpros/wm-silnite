# wm-silnite
Custom plugin for [Watchman Monitoring](https://www.watchmanmonitoring.com) to provide results of [silnite](https://eclecticlight.co/lockrattler-systhist/) by the [Eclectic Light Company](https://eclecticlight.co).

Alerting if specific Apple security updates have not been installed, or are available for installation.

## Requires 
[silnite](https://eclecticlight.co/lockrattler-systhist/) by the [Eclectic Light Company](https://eclecticlight.co) to be installed.

### Note from Eclectic Light Company developer:
```silnite uses the Swift standard frameworks. These are installed at a system level in later versions of Mojave (10.14.4 and later) and in Catalina (10.15). Those using earlier versions of Mojave (10.14.3 and before), Sierra or High Sierra may need to download and install Swift Runtime Support for Command Tools from https://support.apple.com/kb/DL1998```

## As of version .9.7.1.0
* New message for unable to check for updates will say: `Unable to check for updates (curl empty)` and exit as informational
	* This message means the plugin ran when offline and was unable to `curl` the information from gdmf.apple.com (empty result)
	<img width="951" alt="Capture_2024-04-23_12-31-43_PM" src="https://github.com/macitpros/wm-silnite/assets/17754199/03249627-058a-40a9-b0e7-b1739e88f959">
* All clear now includes the current OS version in result
<img width="964" alt="Capture_2024-04-23_12-33-24_PM" src="https://github.com/macitpros/wm-silnite/assets/17754199/a411f7d7-673e-4b0c-a3a1-bc11ab1c0956">

## As of version .9.7.0.0
* Uses curl to pull down current OS version information from https://gdmf.apple.com/v2/pmv
	* Shout out to Ross Matsuda of https://www.sudoade.com/author/ross/ for the excellent write up on how to get the latest OS version updates
* Uses `curl` result to determine if the current OS matches on alerting for ticket/email (`exit 2`)
* Will run OS version check during every run
* Configuration Data related to XProtect/MRT/etc will continue to run according to schedule
* Results for Configuration data will be an informational result (no ticket/email) in the Watchman Monitoring dashboard (`exit 20`)

## As of version .9.6.0.0
* Requires silnite 10 to be installed
* Creates a text file with results of a full run at `/Library/MonitoringClient/PluginSupport/_wm_silnite_results.txt`
* Will run an hourly _light_ run based off results file
* Full run of `silnite` results will still be based off _Frequency to check for updates_... results file will be updated at that time
* Fixes stale plugin results (now that data is sent during every run)
* Added Run Count Information to Plugin results
* Removes Gatekeeper Version reporting (results removed from silnite 10)
* Adds XProtect Remediator Version reporting

<img width="935" alt="Capture_2023-11-09_08-27-55_AM" src="https://github.com/macitpros/wm-silnite/assets/17754199/89c1996f-3648-47bb-8cd7-0a5ea225e18c">

## As of version .9.5.9:
* Uses `/Library/Preferences/com.apple.SoftwareUpdate.plist/Library/Preferences/com.apple.SoftwareUpdate.plist` for gathering list of recommended updates (stops using `softwareupdate -l`).
* Adjusts if a plist setting file is missing an expected value.
* Creates a default settings plist on new installation.
* Changes default reporting frequency to 8 from 12 (more frequently)

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
* Need to make adjustments to prevent overwriting existing settings file
* Once update checking is working, a fresh run should begin, currently not the case.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
THE SOFTWARE.
