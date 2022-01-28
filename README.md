# wm-silnite
Custom plugin for [Watchman Monitoring](https://www.watchmanmonitoring.com) to provide results of [silnite](https://eclecticlight.co/lockrattler-systhist/) by the [Eclectic Light Company](https://eclecticlight.co).

Alerting if specific Apple security updates have not been installed, or are available for installation.

## Requires 
[silnite](https://eclecticlight.co/lockrattler-systhist/) by the [Eclectic Light Company](https://eclecticlight.co) to be installed.

### Note from Eclectic Light Company developer:
```silnite uses the Swift standard frameworks. These are installed at a system level in later versions of Mojave (10.14.4 and later) and in Catalina (10.15). Those using earlier versions of Mojave (10.14.3 and before), Sierra or High Sierra may need to download and install Swift Runtime Support for Command Tools from https://support.apple.com/kb/DL1998```

## As of version .7.0.1:
Adds compatibility for silnite 6, which in turn adds compatibility with Apple Silicon and macOS 12. 
Get silnite version 6 from Eclectic Light: https://eclecticlight.co/lockrattler-systhist/


## As of version .6.4.0:

**Preference Pane**
* _Frequency to check for updates_
  * Sets how often a full run will be done. More time between full checks will help speed up regular Watchman Monitoring reporting.

* _Unable to check for updates attempts_
  * If `silnite` is unable to check for updates due to a connection failure, an informational warning will be generated (no tickets/emails) in your Watchman Monitoring dashboard. If the number of attempts exceeds this number, an alert (ticket/email) will be generated.

![screenshot_1069](https://user-images.githubusercontent.com/17754199/64067360-fe427780-cbec-11e9-9725-9d68cdffc0ec.png)

**Terminal/Command Line Options**
* Force a one-time full run ignoring the frequency count: `sudo defaults write /Library/MonitoringClient/PluginSupport/_wm_silnite_settings.plist First_Run -bool true`
* Set the "Frequency to check for updates" count (set _NUM_ to the number): `sudo defaults write /Library/MonitoringClient/PluginSupport/_wm_silnite_settings.plist Run_Count _NUM_`
* Set the "Unable to check for updates attempts" count (set _NUM_ to the number): `sudo defaults write /Library/MonitoringClient/PluginSupport/_wm_silnite_settings.plist Warn_Updates_Attempts _NUM_`

**Emails daily/ticket created (exit 2) if...**
* `silnite` reports updates are available `UpdateWaiting = 1`

This means...
* MRT could be out-of-date
* Gatekeeper could be out-of-date
* XProtect could be out-of-date
* Other updates from `softwareupdate` are available and will be listed

**If unable to check for updates, shows informational warning (exit 20)**
Includes report of installed versions:
* MRT 
* Gatekeeper
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
