# Race Sentinel
<p align="center">
<a href="https://travis-ci.org/racecrypto/sentinel" alt="Build Status">
<img src="https://travis-ci.org/racecrypto/sentinel.svg?branch=master"/>
</a>
<a href="https://discord.racecrypto.com" alt="Discord">
<img src="https://img.shields.io/discord/402827967111233546.svg"/>
  </a>
<a href="https://twitter.racecrypto.com" alt="Twitter">
<img src="https://img.shields.io/twitter/follow/race_crypto.svg?style=social&label=Follow"/>
</a>
</p>
<p align="center">
  <a href="https://www.racecrypto.com">https://www.racecrypto.com</a> | <a href="https://explorer.racecrypto.com">Block Explorer</a> | <a href="https://ann.racecrypto.com">Announcement</a> | <a href="https://discord.racecrypto.com">Discord</a> | <a href="https://twitter.racecrypto.com">Twitter</a>
</p>

## About 
An all-powerful toolset & watchdog daemon for Race.

Sentinel is an autonomous agent for persisting, processing and automating Race V12.1 governance objects and tasks, and for expanded functions in the upcoming Race releases.

Sentinel is implemented as a Python application that binds to a local version 12.1 raced instance on each Race Masternode.

This guide covers installing Sentinel onto an existing 12.1 Masternode in Ubuntu 14.04 / 16.04.

## Installation

### 1. Install Prerequisites

Make sure Python version 2.7.x or above is installed:

    python --version

Update system packages and ensure virtualenv is installed:

    $ sudo apt-get update
    $ sudo apt-get -y install python-virtualenv

### 2. Install Sentinel

Clone the Sentinel repo and install Python dependencies.

    $ git clone https://github.com/racecrypto/sentinel.git && cd sentinel
    $ virtualenv ./venv
    $ ./venv/bin/pip install -r requirements.txt

### 3. Set up Cron

Set up a crontab entry to call Sentinel every minute:

    $ crontab -e

In the crontab editor, add the lines below, replacing '/home/YOURUSERNAME/sentinel' to the path where you cloned sentinel to:

    * * * * * cd /home/YOURUSERNAME/sentinel && ./venv/bin/python bin/sentinel.py >/dev/null 2>&1

### 4. Test the Configuration

Test the config by runnings all tests from the sentinel folder you cloned into

    $ ./venv/bin/py.test ./test

With all tests passing and crontab setup, Sentinel will stay in sync with dashd and the installation is complete

## Configuration

An alternative (non-default) path to the `race.conf` file can be specified in `sentinel.conf`:

    race_conf=/path/to/race.conf

## Troubleshooting

To view debug output, set the `SENTINEL_DEBUG` environment variable to anything non-zero, then run the script manually:

    $ SENTINEL_DEBUG=1 ./venv/bin/python bin/sentinel.py

### License

Released under the MIT license, under the same terms as Race itself. See [LICENSE](LICENSE) for more info.
