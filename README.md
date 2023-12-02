# Running the Website
our website requires the browser to be started with a security  flag to run correctly 

**NOTE: ALL CHROME INSTANCES MUST BE CLOSED BEFOREHAND!!!**

## Windows

- close any open chrome windows

- navigate to `chrome.exe` (e.g, `C:\Program Files\Google\Chrome\Application`)

- open command line  in this location (in file explorer, right click -> Open in Terminal)

- run the following command: `.\chrome --allow-file-access-from-files` 

- this will open a new chrome window with the flag set. Without closing this window, double click the `index.html` file to open in chrome

## macOS

- close any open chrome windows

- navigate to `Applications` folder

- open terminal in this location (right click -> open folder in terminal)

- run the following command: `open -a "Google Chrome" --args --allow-file-access-from-files`

- this will open a new chrome window with the flag set. Without closing this window, double click the `index.html` file to open in chrome


# File Structure

- open the compiled `index.html` file located in the root project directory using the instructions above. 

- original source files are provided in the `source-files` folder for reference. do not attempt to directly open these files in the browser as they are not compiled.
