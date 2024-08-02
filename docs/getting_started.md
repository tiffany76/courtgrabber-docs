# Getting Started

The Courtgrabber CLI requires minimal set up and only a few commands to get started.

## Key terminology

First, let's define a few key terms.

<dl>
  <dt>Command-line interface (CLI)</dt>
  <dd>Also known as your computer's <strong>terminal</strong>, the command-line interface is a tool for communicating with your computer using text. Instead of navigating with a mouse or selecting a program based on its icon, you can interact with your machine using only keyboard commands.</dd>

  <dt>Command prompt</dt>
  <dd>The command prompt is the text at the beginning of each command line in a CLI. On a Mac, it usually looks something like <code>user ~ $</code>. The prompt tells you which directory, or folder, you are currently working in.</dd>

  <dt>Reservation request</dt>
  <dd>A reservation request is a pending message to the tennis club's reservation software that includes the date, start time, duration, court number, host player's name, ball machine necessity, and if required, the second player's name. Upon creation, Courtgrabber assigns each reservation request a unique ID. The request remains pending until Courtgrabber secures the reservation. Once the reservation time elapses, the request is automatically deleted.</dd>

  <dt>Desired date</dt>
  <dd>The desired date is the day you want to play tennis. Courtgrabber accepts dates as YYYY-MM-DD, such as <code>2022-12-09</code>.</dd>

  <dt>Desired start time</dt>
  <dd>The desired start time is when you want to start playing. Courtgrabber lets you list multiple start times in order of preference, in case your first choice is unavailable. The format is HHMM in 24-hour time with each choice separated by a comma (for example, <code>1300,1330,1400</code>). Start times must be on the hour (:00) or half hour (:30).</dd>

  <dt>Duration</dt>
  <dd>Duration is the length of time you want to play. The options are 30, 60, or 90 minutes.</dd>

  <dt>Court numbers</dt>
  <dd>The court number corresponds to the tennis club's numbering system. You can choose which court you want to reserve by entering a list of numbers, comma-separated in order of preference (for example, <code>4,5,6</code>).</dd>

  <dt>Host player</dt>
  <dd>The host player is the person responsible for the reservation.</dd>

  <dt>Reserve ball machine</dt>
  <dd>You can reserve a ball machine along with your court.</dd>

  <dt>Add a second player</dt>
  <dd>If you are not reserving a ball machine, you must add a second player.</dd>
</dl>

## Installation

Now that you know the key terminology, it's time to install Courtgrabber and start requesting tennis courts. 

### Request access

Contact your tennis club's Courtgrabber liaison to request access to the private repository. Once you've accessed and installed Courtgrabber the first time, you won't need to request access again. 

### Open the command-line interface

You must open your terminal to install and use Courtgrabber.

1. On your Mac computer, press the `command` or `⌘` key and the space bar at the same time.
2. In the search box that appears, start typing `terminal` and press `Enter` once the Terminal program appears.

You now see a mostly empty box with a command prompt. 

*Figure 1: Opening the command-line interface.*
![Opening the command-line interface.](/images/opening_the_cli.gif "Opening the command-line interface.")

### Install Courtgrabber

Follow these five steps to install the Courtgrabber CLI on your computer.

!!! note 
    The Courtgrabber CLI is currently supported on MacOS only.

1. Visit https://github.com/ycombinator/courtgrabber/releases/latest.
2. Click on the download link `courtgrabber-cli-darwin-amd64` in the Assets section at the bottom of the page.
3. Make sure your computer can run the new file by going to your command prompt and entering `chmod 755 ~/Downloads/courtgrabber-cli-darwin-amd64`.
4. To confirm the installation worked, enter `~/Downloads/courtgrabber-cli-darwin-amd64 help`. You should see the Courtgrabber help menu.
5. To rename and move the downloaded file, enter `mv ~/Downloads/courtgrabber-cli-darwin-amd64 /usr/local/bin/courtgrabber`.

You can now begin using Courtgrabber. See the [user guide](./user_guide.md) for detailed instructions.