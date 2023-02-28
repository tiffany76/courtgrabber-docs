## Getting started with the Courtgrabber CLI

The following user guide walks you through how to use Courtgrabber from the command line. If you would like to learn more about the Courtgrabber REST API, please refer to its [reference documentation](./api_reference.md). 

The Courtgrabber CLI requires minimal set-up and uses only a few simple commands. First, let's define a few key terms.

<dl>
  <dt>Command-line interface (CLI)</dt>
  <dd>Also known as your computer's <strong>terminal</strong>, the command-line interface is a tool for communicating with your computer via text. Instead of navigating with a mouse or selecting a program based on its icon, you can interact with your machine using only keyboard commands.</dd>

  <dt>Command prompt</dt>
  <dd>The command prompt is the text at the beginning of each command line in a CLI. On a Mac, it usually looks something like <code>user ~ $</code>. The prompt tells you which directory, or folder, you are currently working in.</dd>

  <dt>Reservation request</dt>
  <dd>A reservation request is a pending message to the tennis club's reservation software that includes the date, start time, duration, court number, host player's name, ball machine necessity, and if required, the second player's name. Upon creation, Courtgrabber assigns each reservation request a unique ID. The request remains pending until Courtgrabber secures the reservation. Once the reservation time elapses, the request is automatically deleted.</dd>

  <dt>Desired date</dt>
  <dd>The desired date is the day you want to play tennis. Courtgrabber accepts dates as YYYY-MM-DD, such as 2022-12-09.</dd>

  <dt>Desired start time</dt>
  <dd>The desired start time is when you want to start playing. Courtgrabber lets you list multiple start times in order of preference, in case your first choice is unavailable. The format is HHMM in 24 hour time with each choice separated by a comma (e.g. 1300,1330,1400).</dd>

  <dt>Duration</dt>
  <dd>Duration is the length of time you want to play. The options are 30, 60, or 90 minutes.</dd>

  <dt>Court numbers</dt>
  <dd>The court number corresponds to the tennis club's number. You can choose which court you want to reserve by entering a list of numbers, comma-separated in order of preference (e.g. 4,5,6).</dd>

  <dt>Host player</dt>
  <dd>The host player is the person responsible for the reservation.</dd>

  <dt>Reserve ball machine</dt>
  <dd>You can reserve a ball machine along with your court.</dd>

  <dt>Add a second player</dt>
  <dd>If you are not reserving a ball machine, you must add a second player.</dd>

## Using the Courtgrabber CLI

Now that you know the key terminology, it's time to install Courtgrabber and start requesting tennis courts. The steps below explain how to use the command line to install Courtgrabber, login to the service, create a reservation request, list your requests, cancel a request, and logout. You will also learn how to find help if you get stuck.

  * [Opening the command-line interface](#opening-the-command-line-interface)
  * [Installing Courtgrabber](#installing-courtgrabber)
  * [Logging into Courtgrabber](#logging-into-courtgrabber)
  * [Creating a court reservation request](#creating-a-court-reservation-request)
  * [Listing all reservation requests](#listing-all-reservation-requests)
  * [Canceling a pending reservation request](#canceling-a-pending-reservation-request)
  * [Logging out of Courtgrabber](#logging-out-of-courtgrabber)
  * [Getting help with Courtgrabber](#getting-help-with-courtgrabber)

### Opening the command-line interface

You need to open your terminal to use Courtgrabber.

1. On your Mac computer, press the `command` or `⌘` key and the space bar at the same time.
2. In the search box that appears, start typing `terminal` and press `Enter` once the Terminal program appears.

You now see a mostly empty box with a command prompt. 

*Figure 1: Opening the command-line interface.*
![Opening the command-line interface.](/docs/images/opening_the_cli.gif "Opening the command-line interface.")

### Installing Courtgrabber

Follow these five steps to install the Courtgrabber CLI on your computer.

> **NOTE**: The Courtgrabber CLI is currently supported only on MacOS.

1. Visit https://github.com/ycombinator/courtgrabber/releases/latest.
2. Click on the download link `courtgrabber-cli-darwin-amd64` in the Assets section at the bottom of the page.
3. Make sure your computer can run the new file by going to your command line and entering `chmod 755 ~/Downloads/courtgrabber-cli-darwin-amd64`.
4. To confirm the installation worked, run `~/Downloads/courtgrabber-cli-darwin-amd64 help`. You should see the Courtgrabber help menu.
5. To rename and move the downloaded file, run `mv ~/Downloads/courtgrabber-cli-darwin-amd64 /usr/local/bin/courtgrabber`.

You can now begin using Courtgrabber!

### Logging into Courtgrabber

You can use your tennis club account to log into the Courtgrabber program.

1. With your terminal window open to the command prompt, type `courtgrabber login` and press `Enter`. The screen will prompt you for your tennis club email address.
2. Enter your club email address and press `Enter`.
3. At the next prompt, enter your club password.

You see a `Login Successful` message.

*Figure 2: Logging into Courtgrabber.*
![Logging into Courtgrabber.](/docs/images/logging_into_courtgrabber.png "Logging into Courtgrabber.")

### Creating a court reservation request

Courtgrabber makes it easy to request a court reservation: just follow the prompts! If you have questions about any of the prompts, refer to the [definitions of key terms](#getting-started-with-the-courtgrabber-cli).

1. After you have logged into Courtgrabber, type `courtgrabber add` at the command prompt and press `Enter`. The screen prompts you for required information.
2. Type your desired date as `YYYY-MM-DD` and press `Enter`.
3. Type your desired start times, in order of preference, in `HHMM` 24-hour format separated by commas and then press `Enter`.
4. Using your up and down arrow keys, select your desired duration and press `Enter`.
5. Type your desired court numbers, in order of preference and separated by commas, then press `Enter`.
6. Using your up and down arrow keys, select the name of the host player and press `Enter`.
7. Using the arrow keys, select `y` if you would like to reserve a ball machine. Otherwise, select `n`. Press `Enter`.
8. Use the arrow keys to select whether or not you will have a second player and press `Enter.`

> **NOTE**: If you are not using a ball machine, you must include a second player to reserve a court.

The CLI displays a message with the Reservation Request ID.

*Figure 3: Creating a court reservation request.*
![Creating a court reservation request.](/docs/images/creating_a_court_reservation_request.gif "Creating a court reservation request.")

### Listing all reservation requests

You can view all active reservation requests using one simple command.

1. While logged in, type `courtgrabber list` at the command prompt and press `Enter`.

You see a table displaying all of your pending requests in chronological order.

*Figure 4: Listing all reservation requests.*
![Listing all reservation requests.](/docs/images/listing_all_reservation_requests.png "Listing all reservation requests.")

### Canceling a pending reservation request

While a request is still pending, you can cancel it from the Courtgrabber CLI. 

> **NOTE**: Once a reservation is made, you must cancel it through your tennis club's reservation system.

1. While logged in, type `courtgrabber cancel` at the command prompt and press `Enter`.
2. Using the up and down arrow keys, scroll through the list of your pending requests until you come to the one you wish to cancel. Press `Enter`. The CLI asks you to confirm that you want to cancel the reservation.
3. Use the arrow keys to select `y` for yes, and then press `Enter`.

You see a `Reservation request {id} cancelled` message.

*Figure 5: Canceling a pending reservation request.*
![Canceling a pending reservation request.](/docs/images/canceling_a_pending_reservation_request.gif "Canceling a pending reservation request.")

### Logging out of Courtgrabber

For the security of your account, you should logout and quit your terminal session when you are finished using Courtgrabber.

1. At the command prompt, type `courtgrabber logout` and press `Enter`.
Courtgrabber asks you to confirm that you want to logout.
2. Type `y` for yes, and then press `Enter`.
You see a `Logout Successful` message.
3. Once again at the command prompt, type `exit` and press `Enter`. 

Your terminal session is closed, and you can safely close the CLI window.

*Figure 6: Logging out of Courtgrabber.*
![Logging out of Courtgrabber.](/docs/images/logging_out_of_courtgrabber.gif "Logging out of Courtgrabber.")

### Getting help with Courtgrabber

If you forget which command to use, you can always ask Courtgrabber for help.

1. At the command line, type `courtgrabber help` and press `Enter`.

Courtgrabber displays its help screen, which includes a list of available commands.

*Figure 7: Getting help with Courtgrabber.*
![Getting help with Courtgrabber.](/docs/images/getting_help_with_courtgrabber.png "Getting help with Courtgrabber.")
