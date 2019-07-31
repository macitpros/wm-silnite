# wm-silnite
Used to report on the results of silnite by the Eclectic Light Company


Requires [silnite](https://eclecticlight.co/lockrattler-systhist/) by the Eclectic Light Company to be installed.

Note from Eclectic Light Company developer:
```
silnite uses the Swift standard frameworks. These are installed at a system level in later versions of Mojave (10.14.4 and later) and in Catalina (10.15). Those using earlier versions of Mojave (10.14.3 and before), Sierra or High Sierra may need to download and install Swift Runtime Support for Command Tools from https://support.apple.com/kb/DL1998
```

Custom plugin for [Watchman Monitoring](https://www.watchmanmonitoring.com) to provide results from silnite. Alerting if specific Apple security updates have not been installed, or are available for installation.

As of version .01:

Emails daily/ticket created (exit 2) if...
* MRT is out of date
* Gatekeeper is out of date
* XProtect is out of date

(still needs testing, code is there) Sends one-time alerts (exit 200) if...
* SIP Disabled
* XProtect Disabled

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
THE SOFTWARE.
