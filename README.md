# wm-silnite
Custom plugin for [Watchman Monitoring](https://www.watchmanmonitoring.com) to provide results of [silnite](https://eclecticlight.co/lockrattler-systhist/) by the [Eclectic Light Company](https://eclecticlight.co).

Alerting if specific Apple security updates have not been installed, or are available for installation.

## Requires 
[silnite](https://eclecticlight.co/lockrattler-systhist/) by the [Eclectic Light Company](https://eclecticlight.co) to be installed.

### Note from Eclectic Light Company developer:
```silnite uses the Swift standard frameworks. These are installed at a system level in later versions of Mojave (10.14.4 and later) and in Catalina (10.15). Those using earlier versions of Mojave (10.14.3 and before), Sierra or High Sierra may need to download and install Swift Runtime Support for Command Tools from https://support.apple.com/kb/DL1998```


## As of version .6.4.0:

**Preference Pane**
* Frequency to check for updates
Sets how often a full run will be done. Less often helps with reducing bandwith and speeds up regular reporting.

* Unable to check for updates attempts
If silnite is unable to check for updates due to connection failure, an information warning will be generated (no tickets/emails). An alert (email/ticket) will be generated after the set number of failed attempts has passed.

![screenshot_1069](https://user-images.githubusercontent.com/17754199/64067360-fe427780-cbec-11e9-9725-9d68cdffc0ec.png)

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

**Known Issues**
* Need to make adjustments to prevent overwriting existing settings file
* Once update checking is working, a fresh run should begin, currently not the case.

![wmscreenshot](https://user-images.githubusercontent.com/17754199/63029161-ae865100-be75-11e9-9f38-b70a42c363b3.png)

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
THE SOFTWARE.
