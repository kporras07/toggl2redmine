# Toggle 2 Redmine

This dandy Redmine plugin imports time entries from Toggl to Redmine using
REST API service calls for both Toggl and Redmine.

Additionally, the plugin groups similar Toggl time entries into a single Redmine
entry. So, even if you start and stop your timer for a particular task multiple
times on Toggl, at the end of day, when you import the time entries to Redmine,
they are grouped by the issue ID and the description, which keeps Redmine clean.

## Disclaimer

This plugin has been made and tested with love and care. However, the makers
of this plugin are in no way responsible for any damages - direct or indirect -
caused by the use of this plugin. In short, use it at your own risk.

## Installation

* Copy the plugin directory into the `plugins` directory of Redmine.
* Run database migrations.
  * You can read more about
[plugin installation](http://www.redmine.org/projects/redmine/wiki/Plugins) on redmine.org
```bash
    RAILS_ENV=production bundle exec rake redmine:plugins:migrate
```
  * This creates a _Toggl API Key_ field on the user profile.
* Your database **must** support [transactions](https://en.wikipedia.org/wiki/Database_transaction).
  * Without transaction support, users might end up importing duplicate
    time entries.

## Usage

### One-time Setup

* Go to the _My Account_ page on Redmine (`/my/account`).
* Paste in your _Toggl API Key_ and save your profile.
  * You can find this in your Toggl _profile settings_ page.
* Update your time zone on Toggl and Redmine - this makes your time reports
  show correctly according to your timezone.
  * *Important:* Confirm with your Redmine administrator whether you need to
    update your timezone. Some organizations use Redmine without configuring
    timezones to avoid certain timezone-related bugs in Redmine.

### Regular Usage

* Login to Toggl and log your time when you're working.
* Make sure your task description is in one of the following formats:
```
#1919 Feed the bunny wabbit.
Tracker #1919 Feed the bunny wabbit.
```
  * You can use the Toggl browser extension to make this easier.
  * `#1919` is the Redmine issue ID.
  * `Feed the bunny wabbit` is the comment.
* When you're done working for the day, visit the _My Timesheet_ page on Redmine
  and click on the _Toggl_ tab on Redmine (`/toggl2redmine`).
  * Most of the options on this page have useful tooltips. If you are confused
    about what something does, simply hover over the item to see if it has an
    informational tooltip.
  * You should see the time you've already logged on Redmine (if any) under the
    heading _Time logged on Redmine_.
  * You should see the time you've logged on Toggl for the day under the
    heading _Time logged on Toggl_.
  * If you want to import entries from some other date, you can change the
    _Date_ filter and any other options as per your requirements.
  * If you change any options, make sure you press _Apply_ for them to
    take effect.
* Now, in the Toggl report, check the entries you want to import into Redmine.
  * For each entry, you can modify the comments, activity and time as per your
    requirements.
* Once you've reviewed everything, click on the _Import to Redmine_ button
  towards the bottom of the page.
  * After you import the data, you cannot undo it, so BE CAREFUL.
* You will see a success (or failure) message next to each item.
  * Entries which imported successfully will be marked in green.
  * Entries which failed to import will be marked in red.

### Advanced options

#### Default Activity

You can specify a _Default activity_ in the options form. This activity will
be pre-populated in your Toggl report, making it easier to import data.

#### Toggl Workspace

If you use multiple workspaces on Toggl, you can choose the workspace from
which you want to import data using the _Toggl Workspace_ field in the options
form.

#### Date

As mentioned before, the _Date_ option allows you to import time entries from
past dates.

#### Duration rounding

You can use this option to round your time entries as per your requirements.
Let's say, the option to round to the nearest 10 minutes. There are 3 ways in
which you can round your time entries.

* *Round Up:* 1h 26m becomes 1h 30m.
* *Round Down:* 1h 26m becomes 1h 20m.
* *Round Off:* 1h 26m becomes 1h 30m whereas 1h 24m becomes 1h 20m.

To disable rounding, you can choose the *Don't round* option.

# Acknowledgements

* Thanks [Evolving Web](https://evolvingweb.ca/) for funding the initial
  development of this plugin.
* Thanks [Jigar Mehta](https://github.com/jigarius) (that's me) for spending
  many evenings and weekends to make this plugin possible.
